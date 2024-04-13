//
//  BookwormApp.swift
//  Bookworm
//
//  Created by Marco Studium on 13.04.24.
//

import SwiftUI
import SwiftData

@main
struct BookwormApp: App {
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
        .modelContainer(for: Student.self)
    }
}

//
//  Student.swift
//  Bookworm
//
//  Created by Marco Studium on 13.04.24.
//

import Foundation
import SwiftData

@Model
class Student {
    var id: UUID
    var name: String
    
    init(id: UUID, name: String) {
        self.id = id
        self.name = name
    }
}

//
//  ContentView.swift
//  Bookworm
//
//  Created by Marco Studium on 13.04.24.
//

import SwiftUI
import SwiftData
// Creating a custom component with @Binding
// Accepting multi-line text input with TextEditor
// Introduction to SwiftData and SwiftUI

struct pushButton: View {
    let title: String
    @Binding var isOn: Bool
    
    var onColors = [Color.red, Color.yellow]
    var offColors = [Color(white: 0.6), Color(white: 0.4)]
    
    var body: some View {
        Button(title) {
            isOn.toggle()
        }
        .padding()
        .background(LinearGradient(colors: isOn ? onColors : offColors, startPoint: .top, endPoint: .bottom))
        .foregroundStyle(.white)
        .clipShape(.capsule)
        .shadow(radius: isOn ? 0 : 5)
    }
}

struct ContentView: View {
    @State private var rememberMe = false
    
    @AppStorage("notes") private var notes = ""
    
    @Environment(\.modelContext) var modelContext
    @Query var students: [Student]
    
    var body: some View {
        VStack {
            pushButton(title: "RememberMe", isOn: $rememberMe)
            Text(rememberMe ? "On" : "Off")
        }
        NavigationStack {
            TextEditor(text: $notes)
                .navigationTitle("Notes Text Editor")
                .padding()
        }
        NavigationStack {
            TextField("Enter your text", text: $notes, axis: .vertical )
                .textFieldStyle(.roundedBorder)
                .navigationTitle("Notes Text Field")
                .padding()
        }
        
        NavigationStack {
            List(students) { student in
                Text(student.name)
            }
            .navigationTitle("Classroom")
            .toolbar {
                Button("Add") {
                    let firstNames = ["Ginny", "Harry", "Hermione", "Luna", "Ron"]
                    let lastNames = ["Granger", "Lovegood", "Potter", "Weasly"]
                    
                    let chosenFirstName = firstNames.randomElement()!
                    let chosenLastName = lastNames.randomElement()!
                    
                    let student = Student(id: UUID(), name: "\(chosenFirstName) \(chosenLastName)")
                    
                    modelContext.insert(student)
                }
            }
        }
    }
}

#Preview {
    ContentView()
}


