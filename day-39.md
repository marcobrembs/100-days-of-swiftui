//
//  ContentView.swift
//  Moonshot
//
//  Created by Marco Studium on 30.03.24.
//

import SwiftUI

struct customText: View {
    let text: String
    
    var body: some View {
        Text(text)
    }
    
    init(text: String) {
        print("Creating a new CustomText")
        self.text = text
    }
}

struct User: Codable {
    let name: String
    let address: Address
}

struct Address: Codable {
    let street: String
    let city: String
}

struct ContentView: View {
    let layout = [
        GridItem(.adaptive(minimum: 80, maximum: 120)),
    ]
    
    var body: some View {
        VStack {
            // Resizing images to fit the available space
            Image(.example)
                .resizable()
                .scaledToFit()
                .containerRelativeFrame(.horizontal) { size, axis in
                    size * 0.8
                }
        }
        .padding()
        
                // How ScrollView lets us work with scrolling data
                ScrollView {
                    LazyVStack(spacing: 10) {
                        ForEach(0..<100) {
                            customText(text: "Item \($0)")
                                .font(.title)
                        }
                    }
                    .frame(maxWidth: .infinity)
                }
        
        NavigationStack {
            NavigationLink {
                Text("Detail View")
            } label: {
                VStack {
                    Text("This is the label")
                    Text("So is this")
                    Image(systemName: "face.smiling")
                }
                .font(.largeTitle)
            }
            .navigationTitle("SwiftUI")
        }
        
        // Pushing new views onto the stack using NavigationLink
        NavigationStack {
            List(0..<100) { row in
                NavigationLink("Row \(row)") {
                    Text("Detail \(row)")
                }
            }
        }
        
        // Working with hierarchical Codable data
        Button("Decode JSON") {
            let input = """
            {
                "name": "Taylor Swift"
                "address": {
                    "street": "555, Taylor Swift Avenue",
                    "city": "Nashville"
                }
            }
            """
            
            let data = Data(input.utf8)
            let decoder = JSONDecoder()
            
            if let user = try? decoder.decode(User.self, from: data) {
                print(user.address.street)
            }
        }

        // How to lay out views in a scrolling grid
        ScrollView(.horizontal) {
            LazyHGrid(rows: layout) {
                ForEach(0..<1000) {
                    Text("Item \($0)")
                }
            }
        }
        
    }
}

#Preview {
    ContentView()
}
