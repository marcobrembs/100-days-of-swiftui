//
//  ContentView.swift
//  Navigation
//
//  Created by Marco Studium on 02.04.24.
//

import SwiftUI

@Observable

// How to save NavigationStack paths using Codable
class PathStore {
    var path: NavigationPath {
        didSet {
            save()
        }
    }
    
    private let savePath = URL.documentsDirectory.appending(path: "SavedPath")
    
    init() {
        if let data = try? Data(contentsOf: savePath) {
            if let decoded = try? JSONDecoder().decode(NavigationPath.CodableRepresentation.self, from: data) {
                path = NavigationPath(decoded)
                return
            }
        }
        
        path = NavigationPath()
    }
    
    func save() {
        guard let representation = path.codable else { return }
        
        do {
            let data = try JSONEncoder().encode(representation)
            try data.write(to: savePath)
        } catch {
            print("Failed to save navigation data")
        }
    }
}

struct DetailView: View {
    var number: Int
    
    var body: some View {
        NavigationLink("Go to Random Number", value: Int.random(in: 1...1000))
            .navigationTitle(("Number: \(number)"))
//            .toolbar {
//                Button("Home") {
//                    path = NavigationPath()
//                }
//            }
    }
}

struct ContentView: View {
//    @State private var path = [Int]()
    
//    @State private var path = NavigationPath()
    
    @State private var pathStore = PathStore()
    
    var body: some View {
//        // Programmatic navigation with NavigationStack
//        NavigationStack(path: $path) {
//            VStack {
//                Button("Show 32") {
//                    path = [32]
//                }
//                Button("Show 64") {
//                    path.append(64)
//                }
//                Button("Show 32 then 64") {
//                    path = [32, 64]
//                }
//            }
//            .navigationDestination(for: Int.self) { selection in
//                Text("You selected \(selection)")
//            }
//        }
//        
//        
//
//        // Navigating to different data types using NavigationPath
//        NavigationStack(path: $path) {
//            List {
//                ForEach(0..<5) { i in
//                    NavigationLink("Select Number: \(i)", value: i)
//                }
//                ForEach(0..<5) { i in
//                    NavigationLink("Select String: \(i)", value: String(i))
//                }
//            }
//            .toolbar {
//                Button("Push 556") {
//                    path.append(556)
//                }
//                
//                Button("Push hello") {
//                    path.append("Hello")
//                }
//            }
//            .navigationDestination(for: Int.self) { selection in
//                Text("You selected number \(selection)")
//            }
//            .navigationDestination(for: String.self) { selection in
//                Text("You selected string \(selection)")
//                
//            }
//        }
        // How to make a NavigationStack return to its root view programmatatically
        NavigationStack(path: $pathStore.path) {
            DetailView(number: 0)
                .navigationDestination(for: Int.self) { i in
                    DetailView(number: i)
                }
        }
    }
}

#Preview {
    ContentView()
}
