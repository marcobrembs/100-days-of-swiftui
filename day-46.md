// Challenge 1: Change project 7 (iExpense) so that it uses NavigationLink for adding new expenses rather than a sheet. 
(Tip: The dismiss() code works great here, but you might want to add the navigationBarBackButtonHidden() modifier so they have to explicitly choose Cancel.)

// ContentView
            .toolbar {
                NavigationLink(destination: AddView(expenses: expenses)) {
                    Button("Add Expense", systemImage: "plus") {
                        showingAddExpense = true
                    }
                }
            }

// AddView

            .toolbar {
                ToolbarItem(placement: .confirmationAction) {
                    Button("Save") {
                        let item = ExpenseItem(name: name, type: type, amount: amount)
                        expenses.items.append(item)
                        dismiss()
                    }
                }
                ToolbarItem(placement: .cancellationAction) {
                    Button("Cancel") {
                        dismiss()
                    }
                    .navigationBarBackButtonHidden(true)
                    

// Challenge 2: Try changing project 7 so that it lets users edit their issue name in the navigation title rather than a separate textfield.

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

// Challenge 3: Return to project 8 (Moonshot), and upgrade it to use NavigationLink(value:). This means adding Hashable conformance, and thinking carefully how to use navigationDestination().

...
