// Challenge 1: use conditional modifier to change the total amount text to red if user selects a 0% tip

.foregroundStyle(tipPercentage == 0 ? .red : .primary)


// Challenge 2: replace the Image view used for flags with a new FlagImage() view that renders one flag image using the defined modifiers

public struct FlagImage: View {
    var imageName: String
    
    public var body: some View {
        Image(imageName)
            .clipShape(.capsule)
            .shadow(radius: 5)
    }
}

ForEach(0..<3) { number in
  Button {
    flagTapped(number)
  } label: {
    FlagImage(imageName: countries[number])
  }
}


// Challenge 3: create a custom ViewModifier (and accompanying View extension) that makes a view with a large blue title

struct Title: ViewModifier {
    func body(content: Content) -> some View {
        content
            .font(.largeTitle.bold())
            .foregroundStyle(.blue)
            .textCase(.uppercase)
    }
}

extension View {
    func titleStyle() -> some View {
        modifier(Title())
    }
}

Text("Guess the Flag")
  .modifier(Title())
