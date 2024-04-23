//
//  ContentView.swift
//  Instafilter
//
//  Created by Marco Studium on 23.04.24.
//

import SwiftUI

// How property wrappers become structs
// Resonding to state changes using onChange()
struct ContentView: View {
    @State private var blurAmount = 0.0
    
    var body: some View {
        VStack {
            Text("Hello, world")
                .blur(radius: blurAmount)
            
            Slider(value: $blurAmount, in: 0...20)
                .onChange(of: blurAmount) {
                    print("Blur changed")
                }
        }
    }
}

// Showing multiple options with confirmationDialog()
struct ContentView: View {
    @State private var showingConfirmation = false
    @State private var backgroundColor = Color.white
    var body: some View {
        Button("Hello world") {
            showingConfirmation.toggle()
        }
        .frame(width: 300, height: 300)
        .background(backgroundColor)
        .confirmationDialog("Change background", isPresented: $showingConfirmation) {
            Button("Red") { backgroundColor = .red }
            Button("Green") { backgroundColor = .green }
            Button("Blue") { backgroundColor = .blue }
            Button("Cancel", role: .cancel) { }
        } message: {
            Text("Select a new color.")
        }
    }
}

#Preview {
    ContentView()
}
