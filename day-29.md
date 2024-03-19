//
//  ContentView.swift
//  WordScramble
//
//  Created by Marco Studium on 19.03.24.
//

import SwiftUI

struct ContentView: View {
    let people = ["Finn", "Leia", "Luke", "Rey"]
    
    var body: some View {
        List {
            Section("Section 1") {
                Text("Static Row 1")
                Text("Static Row 2")
            }
            Section("Section 2") {
                ForEach(0..<5) {
                    Text("Dynammic Row \($0)")
                }
            }
            Section("Section 3") {
                Text("Static Row 3")
                Text("Static Row 4")
            }
        }
        .listStyle(.grouped)
        
        List (0..<5) {
            Text("Dynamic Row \($0)")
        }
        List (people, id: \.self) {
            Text($0)
        }
        List {
            Text("Static Row")
        
            ForEach(people, id: \.self) {
                Text($0)
            }
            Text("Static Row")
        }
    }
    func testBundles() {
        if let fileURL = Bundle.main.url(forResource: "somefile", withExtension: "txt") {
            if let fileContents = try? String(contentsOf: fileURL) {
                // we loaded the file into a string
            }
        }
    }
    func testStrings() {
        let input = """
a
b
c
"""
        let letters = input.components(separatedBy: "\n")
        let letter = letters.randomElement()
        let trimmed = letter?.trimmingCharacters(in: .whitespacesAndNewlines)
    }
}

func testStrings2() {
    let word = "swift"
    let checker = UITextChecker()
    
    let range = NSRange(location: 0, length: word.utf16.count)
    let misspelledRange = checker.rangeOfMisspelledWord(in: word, range: range, startingAt: 0, wrap: false, language: "en")
    
    let allGood = misspelledRange.location == NSNotFound
}

#Preview {
    ContentView()
}
