// // Project 1 - WeSplit

import SwiftUI

struct ContentView: View {
    @State private var checkAmount = 0.0
    @State private var numberOfPeople = 2
    @State private var tipPercentage = 20
    @FocusState private var amountIsFocused: Bool
    
    var grandTotal: Double {
        // calculate the grand total
        let tipSelection = Double(tipPercentage)
        
        let tipValue = checkAmount * tipSelection / 100
        let grandTotal = checkAmount + tipValue
        
        return grandTotal
    }
    
    var amountPerPerson: Double {
        // calculate the total per person
        let peopleCount = Double(numberOfPeople + 2)
        
        let amountPerPerson = grandTotal / peopleCount
        
        return amountPerPerson
    }
    
    
    var body: some View {
        NavigationStack {
            Form {
                Section {
                    TextField("Amount", value: $checkAmount, format: .currency(code: Locale.current.currency?.identifier ?? "USD"))
                        .keyboardType(.decimalPad)
                        .focused($amountIsFocused)
                    
                    Picker("Number of people", selection: $numberOfPeople) {
                        ForEach(2..<100) {
                            Text("\($0) people")
                        }
                    }
                }
                
                Section("How much do you want to tip?") {
                    Picker("Tip percentage", selection: $tipPercentage) {
                        ForEach(0..<101) {
                            Text($0, format: .percent)
                        }
                    }
                    .pickerStyle(.navigationLink)
                }
                
                Section("Amount including tip") {
                    Text(grandTotal, format: .currency(code: Locale.current.currency?.identifier ?? "USD"))
                }
                
                Section ("Amount per person"){
                    Text(amountPerPerson, format: .currency(code: Locale.current.currency?.identifier ?? "USD"))
                }
            }
            .navigationTitle("WeSplit")
            .toolbar {
                if amountIsFocused {
                    Button("Done") {
                        amountIsFocused = false
                    }
                }
            }
        }
    }
}

#Preview {
    ContentView()
}
