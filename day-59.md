//
//  iExpenseSwiftDataApp.swift
//  iExpenseSwiftData
//
//  Created by Marco Studium on 20.04.24.
//

import SwiftUI

@main
struct iExpenseSwiftDataApp: App {
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
        .modelContainer(for: ExpenseItem.self)
    }
}

//
//  ContentView.swift
//  iExpenseSwiftData
//
//  Created by Marco Studium on 20.04.24.
//

import SwiftData
import SwiftUI

struct ContentView: View {
    @Environment(\.modelContext) var modelContext
    @Query var expenses: [ExpenseItem]
    
//  @State private var expenses = [ExpenseItem]()
    @State private var showingAddExpense = false
    @State private var expenseType = "Personal"
    
    @State private var sortOrder = [
        SortDescriptor(\ExpenseItem.name),
        SortDescriptor(\ExpenseItem.amount)
    ]
    
    @State private var showBusinessExpense = false
    
    var body: some View {
        NavigationStack {
            ExpensesView(expenseType: showBusinessExpense ? "Business" : "Personal", sortOrder: sortOrder)
                .navigationTitle("Expenses")
                .navigationBarTitleDisplayMode(.large)
                .navigationDestination(for: ExpenseItem.self) { expense in
                }
                .toolbar {
                    Button(showBusinessExpense ? "Personal" : "Business") {
                        showBusinessExpense.toggle()
                    }
                    Menu("Sort", systemImage: "arrow.up.arrow.down") {
                        Picker("Sort", selection: $sortOrder) {
                            Text("Sort by name")
                                .tag([
                                    SortDescriptor(\ExpenseItem.name),
                                    SortDescriptor(\ExpenseItem.amount)
                                ])
                            Text("Sort by amount")
                                .tag([
                                    SortDescriptor(\ExpenseItem.amount),
                                    SortDescriptor(\ExpenseItem.name)
                                ])
                        }
                    }
                    NavigationLink(destination: AddExpenseView()) {
                        Button("Add Expense",systemImage: "plus") {
                            //                            try? modelContext.delete(model: ExpenseItem.self)
                            showingAddExpense = true
                        }
                    }
                }
        }
    }
}

#Preview {
    ContentView()
}

//
//  ExpensesView.swift
//  iExpenseSwiftData
//
//  Created by Marco Studium on 21.04.24.
//

import SwiftData
import SwiftUI

struct ExpensesView: View {
    @Environment(\.modelContext) var modelContext
    @Query var expenses: [ExpenseItem]
    
    @State private var sortOrder = [
        SortDescriptor(\ExpenseItem.name),
        SortDescriptor(\ExpenseItem.amount)
    ]
    
    var body: some View {
        List {
            ForEach(expenses) { expense in
                HStack {
                    VStack(alignment: .leading) {
                        Text(expense.name)
                            .font(.headline)
                        
                        Text(expense.type)
                    }
                    Spacer()
                    
                    Text(expense.amount, format: .currency(code: Locale.current.currency?.identifier ?? "EUR"))
                }
                .foregroundStyle((expense.amount < 10) ? .green :  (expense.amount < 100) ? .yellow : .red)
            }
            .onDelete(perform: removeExpenses)
        }
//        .onAppear(perform: addSample)
    }
    
//    func addSample() {
//        let expense1 = ExpenseItem(name: "Lunch", type: "Personal", amount: 14.00)
//        modelContext.insert(expense1)
//    }
    
    func removeExpenses(at offsets: IndexSet) {
        for offset in offsets {
            let expense = expenses[offset]
            modelContext.delete(expense)
        }
    }
    
    init(expenseType: String, sortOrder: [SortDescriptor<ExpenseItem>]) {
        _expenses = Query(filter: #Predicate<ExpenseItem> { expense in
            expense.type == expenseType
        }, sort: sortOrder)
    }
}

#Preview {
    ExpensesView(expenseType: "Personal", sortOrder: [SortDescriptor(\ExpenseItem.name)])
}

//
//  AddExpenseView.swift
//  iExpenseSwiftData
//
//  Created by Marco Studium on 21.04.24.
//

import SwiftData
import SwiftUI

struct AddExpenseView: View {
    @Environment(\.dismiss) var dismiss
    @Environment(\.modelContext) var modelContext
    @Query var expenses: [ExpenseItem]
    
    @State private var name = "Expense Name"
    @State private var type = "Personal"
    @State private var amount = 0.0
    
    let types = ["Business", "Personal"]
    
    var body: some View {
        NavigationStack {
            Form {
//                TextField("Name", text: $name)
                
                Picker("Type", selection: $type) {
                    ForEach(types, id: \.self) {
                        Text($0)
                    }
                }
                
                TextField("Amount", value: $amount, format: .currency(code: Locale.current.currency?.identifier ?? "USD"))
                    .keyboardType(.decimalPad)
            }
            .navigationTitle($name)
            .navigationBarTitleDisplayMode(.inline)
            .toolbar {
                ToolbarItem(placement: .confirmationAction) {
                    Button("Save") {
                        let expense = ExpenseItem(name: name, type: type, amount: amount)
                        modelContext.insert(expense)
                        dismiss()
                    }
                }
                ToolbarItem(placement: .cancellationAction) {
                    Button("Cancel") {
                        dismiss()
                    }
                    .navigationBarBackButtonHidden(true)
                }
            }
        }
    }
}

//#Preview {
//    AddExpenseView(dismiss: <#T##arg#>, modelContext: <#T##arg#>, expenses: <#T##[ExpenseItem]#>)
//}

//
//  ExpenseItem.swift
//  iExpenseSwiftData
//
//  Created by Marco Studium on 20.04.24.
//

import Foundation
import SwiftData

@Model
class ExpenseItem/*: Identifiable*/ {
//    var id = UUID()
    var name: String
    var type: String
    var amount: Double
    
    init(id: UUID = UUID(), name: String, type: String, amount: Double) {
//        self.id = id
        self.name = name
        self.type = type
        self.amount = amount
    }    
}
