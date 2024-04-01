//
//  ContentView.swift
//  Moonshot
//
//  Created by Marco Studium on 30.03.24.
//

import SwiftUI

struct ContentView: View {
    let astronauts: [String: Astronaut] = Bundle.main.decode("astronauts.json")
    let missions: [Mission] = Bundle.main.decode("missions.json")
    
    let columns = [
        GridItem(.adaptive(minimum: 150))
    ]
    
    @State private var showingGrid = true
    
    var body: some View {
        NavigationStack {
            Group {
                if showingGrid {
                    OverviewGridView(astronauts: astronauts, missions: missions)
                } else {
                    OverviewListView(astronauts: astronauts, missions: missions)
                }
            }
            .navigationTitle("Moonshot")
            .background(.darkBackground)
            .preferredColorScheme(.dark)
            .toolbar {
                Button {
                    showingGrid.toggle()
                } label: {
                    if showingGrid {
                        Label("Grid", systemImage: "list.star")
                    } else {
                        Label("List", systemImage: "square.grid.2x2")
                    }
                }
            }
        }
    }
    
    func enableListView() {
        print("Hello")
    }
}

#Preview {
    ContentView()
}
