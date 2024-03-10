// GuessTheFlag
// Overview


import SwiftUI

struct ContentView: View {
    
    let rows: Int = 3
    let columns: Int = 3
    
    @State private var showingAlert = false
    
    var body: some View {
        VStack {
            // using stacks to arrange views
            ForEach(0..<3) { row in
                HStack {
                    ForEach(0..<3) { column in
                        Text("\(row * self.columns + columns)")
                    }
                }
            }
        }
        ZStack {
            // colors and frames
            Color(red: 1, green: 0.8, blue: 0)
            VStack(spacing: 0) {
                Color.red
                Color.blue
            }
            Text("Your content")
                .foregroundStyle(.secondary)
                .padding(50)
                .background(.ultraThinMaterial)
        }
        .ignoresSafeArea()
        LinearGradient(colors: [.white, .black], startPoint: .top, endPoint: .bottom)
        LinearGradient(stops: [
            .init(color: .white, location: 0.45),
            .init(color: .black, location: 0.55)
        ], startPoint: .top, endPoint: .bottom)
        RadialGradient(colors: [.blue, .black], center: .center, startRadius: 20, endRadius: 200)
        AngularGradient(colors: [.red, .yellow, .green, .blue, .purple, .red], center: .center)
        Text("Your content")
            .frame(maxWidth: .infinity, maxHeight: .infinity)
            .foregroundStyle(.white)
            .background(.black.gradient)
        VStack {
            // Buttons
            Button("Button 1") { }
                .buttonStyle(.bordered)
            
            Button("Button 2", role: .destructive) { }
                .buttonStyle(.bordered)
            
            Button("Button 3") { }
                .buttonStyle(.borderedProminent)
            
            Button("Button 4", role: .destructive) { }
                .buttonStyle(.borderedProminent)
        }
        Button {
            print("Button was tapped")
        } label: {
            Text("Tap me!")
                .padding()
                .foregroundStyle(.white)
                .background(.red)
        }
        Image("Singapore")
        // Images
        Image(systemName: "pencil")
            .font(.largeTitle)
        Button {
            print("Button was tapped")
        } label: {
            Label("Edit", systemImage: "pencil")
                .padding()
                .foregroundStyle(.white)
                .background(.red)
        }
        
        Button("Show alert") {
            showingAlert = true
        }
        .alert("Important message", isPresented: $showingAlert) {
            Button("Delete", role: .destructive) { }
            Button("Cancel", role: .cancel) { }
        } message: {
            Text("Please read this.")
        }
    }
    
    func executeDelete() {
        print("Now deleting...")
    }

}
        

#Preview {
    ContentView()
}
