//
//  ContentView.swift
//  iExpense
//
//  Created by Marco Studium on 25.03.24.
//

import Observation
import SwiftUI

@Observable
class User {
    var firstName = "Bilbo"
    var lastName = "Baggins"
}

struct SecondView: View {
    @Environment(\.dismiss) var dismiss
    let name: String
    
    var body: some View {
        Button("Dismiss") {
            dismiss()
        }
    }
}

struct User1: Codable {
    var firstName: String
    var lastName: String
}

struct ContentView: View {
    @State private var user = User()
    
    @State private var showingSheet = false
    
    @State private var numbers = [Int]()
    @State private var currentNumber = 1
    
    @AppStorage("tapCount") private var tapCount = 0
    
    @State private var user1 = User1(firstName: "Taylor", lastName: "Swift")
    
    var body: some View {
        VStack {
            Text("Your name is \(user.firstName) \(user.lastName)")
            
            TextField("First name", text: $user.firstName)
            TextField("Last name", text: $user.lastName)
        }
        .padding()
        
        Button("Show Sheet") {
            showingSheet.toggle()
        }
        .sheet(isPresented: $showingSheet) {
            SecondView(name: "Marco")
        }
        NavigationStack {
            VStack {
                List {
                    ForEach(numbers, id: \.self) {
                        Text("Row \($0)")
                    }
                    .onDelete(perform: removeRows)
                }
                Button("Add Number") {
                    numbers.append(currentNumber)
                    currentNumber += 1
                }
            }
            .toolbar {
                EditButton()
            }
        }
        
        Button("Tap Count \(tapCount)") {
            tapCount += 1
        }
        
        Button("Save User") {
            let encoder = JSONEncoder()
            
            if let data = try? encoder.encode(user1) {
                UserDefaults.standard.set(data, forKey: "UserData")
            }
        }
    }
    
    func removeRows(at offsets: IndexSet) {
        numbers.remove(atOffsets: offsets)
    }
}

#Preview {
    ContentView()
}
