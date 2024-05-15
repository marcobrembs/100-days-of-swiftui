// The check out view in Cupcake Corner uses an image and loading spinner that don’t add anything to the UI, so find a way to make the screenreader not read them out.

placeholder: {
  ProgressView()
  .accessibilityElement()
}

// Fix the list rows in iExpense so they read out the name and value in one single VoiceOver label, and their type in a hint.

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
                .accessibilityElement()
                .accessibilityLabel("\(item.name) for \(item.amount)")
                .accessibilityHint("\(item.type) expense")
            }

// Do a full accessibility review of Moonshot – what changes do you need to make so that it’s fully accessible?

// Moonshot project still needs to be updated for accessibility
