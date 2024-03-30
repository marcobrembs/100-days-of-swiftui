// Challenge 1: Use the user’s preferred currency, rather than always using US dollars.

Text(item.amount, format: .currency(code: Locale.current.currency?.identifier ?? "USD"))

// Challenge 2: Modify the expense amounts in ContentView to contain some styling depending on their value
– expenses under $10 should have one style, expenses under $100 another, and expenses over $100 a third style. 
What those styles are depend on you.

.foregroundStyle((item.amount < 10) ? .green : (item.amount < 100) ? .yellow : .red)

// Challenge 3: For a bigger challenge, try splitting the expenses list into two sections: one for personal expenses, and one for business expenses. 
This is tricky for a few reasons, not least because it means being careful about how items are deleted!

//
//  ContentView.swift
//  iExpense
//
//  Created by Marco Studium on 25.03.24.
//

import SwiftUI

struct ExpenseItem: Identifiable, Codable {
    var id = UUID()
    let name: String
    let type: String
    let amount: Double
}

@Observable
class Expenses {
    var items = [ExpenseItem]() {
        didSet {
            if let encoded = try? JSONEncoder().encode(items) {
                UserDefaults.standard.set(encoded, forKey: "Items")
            }
        }
    }
    
    var personalExpenses: [ExpenseItem] {
         items.filter { $0.type == "Personal" }
     }
    
    var businessExpenses: [ExpenseItem] {
        items.filter { $0.type == "Business" }
    }
    
    init() {
        if let savedItems = UserDefaults.standard.data(forKey: "Items") {
            if let decodedItems = try? JSONDecoder().decode([ExpenseItem].self, from: savedItems) {
                items = decodedItems
                return
            }
        }
    }
}

struct ExpenseSection: View {
    let title: String
    let expenses: [ExpenseItem]
    let removeItems: (IndexSet) -> Void
    
    var body: some View {
        Section(title) {
            ForEach(expenses) { item in
                HStack {
                    VStack(alignment: .leading) {
                        Text(item.name)
                            .font(.headline)
                        
                        Text(item.type)
                    }
                    Spacer()
                    
                    Text(item.amount, format: .currency(code: Locale.current.currency?.identifier ?? "USD"))
                }
                .foregroundStyle((item.amount < 10) ? .green : (item.amount < 100) ? .yellow : .red)
            }
            .onDelete(perform: removeItems)
        }
    }
}

struct ContentView: View {
    @State private var expenses = Expenses()
    @State private var showingAddExpense = false
    
    var body: some View {
        NavigationStack {
            List {
                ExpenseSection(title: "Personal", expenses: expenses.personalExpenses, removeItems: removeItems)
                
                ExpenseSection(title: "Business", expenses: expenses.businessExpenses, removeItems: removeItems)
            }
            .navigationTitle("iExpense")
            .toolbar {
                Button("Add Expense", systemImage: "plus") {
                    showingAddExpense = true
                }
            }
            .sheet(isPresented: $showingAddExpense) {
                AddView(expenses: expenses)
            }
        }
    }
    
    func removeItems(at offsets: IndexSet) {
        expenses.items.remove(atOffsets: offsets)
    }
}

#Preview {
    ContentView()
}
