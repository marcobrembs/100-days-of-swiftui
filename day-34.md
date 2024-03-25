// GuessTheFlag

import SwiftUI

public struct FlagImage: View {
    var imageName: String
    
    public var body: some View {
        Image(imageName)
            .clipShape(.capsule)
            .shadow(radius: 5)
    }
}

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

struct ContentView: View {
    
    @State private var countries = ["Estonia", "France", "Germany", "Ireland", "Italy", "Nigeria", "Poland", "Spain", "UK", "Ukraine", "US"].shuffled()
    @State private var correctAnswer = Int.random(in: 0...2)
    
    @State private var showingScore = false
    @State private var scoreTitle = ""
    @State private var userScore = 0
    
    @State private var showingResult = false
    @State private var resultTitle = ""
    @State private var gameRounds = 0
    
    @State private var selectedFlag = -1
    
    
    var body: some View {
        ZStack {
            RadialGradient(stops: [
                .init(color: Color(red: 0.1, green: 0.2, blue: 0.45), location: 0.3),
                .init(color: Color(red: 0.76, green: 0.15, blue: 0.26), location: 0.3)
            ], center: .top, startRadius: 200, endRadius: 700)
                .ignoresSafeArea()
            
            VStack {

                Spacer()
                
                Text("Guess the Flag")
                    .modifier(Title())
                
                VStack(spacing: 15) {
                    VStack {
                        Text("Tap the flag of")
                            .foregroundStyle(.secondary)
                            .font(.subheadline.weight(.heavy))
                        
                        Text(countries[correctAnswer])
                            .font(.largeTitle.weight(.semibold))
                    }
                    
                    ForEach(0..<3) { number in
                        Button {
                            flagTapped(number)
                        } label: {
                            FlagImage(imageName: countries[number])
                                .rotation3DEffect(.degrees(selectedFlag == number ? 360 : 0), axis: (x:0, y: 1, z:0))
                                .opacity(selectedFlag == -1 || selectedFlag == number ? 1.0 : 0.25)
                                .scaleEffect(selectedFlag == -1 || selectedFlag == number ? 1 : 0.5)
                                .animation(.default, value: selectedFlag)
                        }
                        
                    }
                    
                }
                .frame(maxWidth: .infinity)
                .padding(.vertical, 20)
                .background(.regularMaterial)
                .clipShape(.rect(cornerRadius: 20))
                
                Spacer()
                Spacer()
                
                Text("Score: \(userScore)")
                    .foregroundStyle(.white)
                    .font(.title.bold())
                
                Spacer()
            }
            .padding()
            
        }
        .alert(scoreTitle, isPresented: $showingScore) {
            Button("Continue", action: askQuestion)
        } message: {
            Text("Your score is \(userScore)")
        }
        .alert(resultTitle, isPresented: $showingResult) {
            Button("Restart Game", action: restartGame)
        } message: {
            Text("You guessed \(userScore) out of 8 flags correctly")
        }
    }
    
    func flagTapped(_ number: Int) {
        selectedFlag = number
        if number == correctAnswer {
            scoreTitle = "Correct. That´s the flag of \(countries[number])"
            userScore = userScore + 1
        } else {
            scoreTitle = "Wrong. That´s the flag of \(countries[number])"
            userScore = userScore
        }
        gameRounds = gameRounds + 1
        showingScore = true
        
        if gameRounds == 8 {
            endGame()
            showingScore = false
        }
    }
    
    func askQuestion() {
        countries.shuffle()
        correctAnswer = Int.random(in: 0...2)
        selectedFlag = -1
    }
    
    func endGame() {
        if gameRounds == 8 {
            resultTitle = "Congratulations - you made it to the end!"
        }
        showingResult = true
        selectedFlag = -1
    }
    
    func restartGame() {
        gameRounds = 0
        userScore = 0
    }
    
}

#Preview {
    ContentView()
}
