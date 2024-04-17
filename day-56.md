// Challenge 1
// Right now it’s possible to select no title, author, or genre for books, which causes a problem for the detail view. 
// Please fix this, either by forcing defaults, validating the form, or showing a default picture for unknown genres – you can choose.

//
//  AddBookView.swift
//  Bookworm
//
//  Created by Marco Studium on 13.04.24.
//

import SwiftUI
import SwiftData

struct AddBookView: View {
    @Environment(\.modelContext) var modelContext
    @Environment(\.dismiss) var dismiss
    
    @State private var title = ""
    @State private var author = ""
    @State private var rating = 3
    @State private var genre = "Fantasy"
    @State private var review = ""
    
    let genres = ["Fantasy", "Horror", "Kids", "Mystery", "Poetry", "Romance", "Thriller"]
    
    var body: some View {
        NavigationStack {
            Form {
                Section {
                    TextField("Name of book", text: $title)
                    TextField("Author´s name", text: $author)
                    
                    Picker("Genre", selection: $genre) {
                        ForEach(genres, id: \.self) {
                            Text($0)
                        }
                    }
                }
                Section("Write a review") {
                    TextEditor(text: $review)
                    RatingView(rating: $rating)
                }
                
                Section {
                    Button("Save") {
                        let newBook = Book(title: title, author: author, genre: genre, review: review, rating: rating, date: Date.now)
                        modelContext.insert(newBook)
                        dismiss()
                    }
                }
                .disabled(hasValidFields() == false)
            }
            .navigationTitle("Add Book")
        }
    }
    func hasValidFields() -> Bool {
        if title.isEmpty || author.isEmpty {
            return false
        } else if title.trimmingCharacters(in: .whitespaces).isEmpty || author.trimmingCharacters(in: .whitespaces).isEmpty {
            return false
        } else {
            return true
        }
    }
}

#Preview {
    AddBookView()
}


// Challenge 2
// Modify ContentView so that books rated as 1 star are highlighted somehow, such as having their name shown in red.

                        HStack {
                            EmojiRatingView(rating: book.rating)
                                .font(.largeTitle)
                            
                            VStack(alignment: .leading) {
                                Text(book.title)
                                    .font(.headline)
                                Text(book.author)
                                    .foregroundStyle(.secondary)
                            }
                            .foregroundStyle(book.rating == 1 ? .red : .primary)
                        }


// Challenge 3
// Add a new “date” attribute to the Book class, assigning Date.now to it so it gets the current date and time, then format that nicely somewhere in DetailView.

//
//  Book.swift
//  Bookworm
//
//  Created by Marco Studium on 13.04.24.
//

import Foundation
import SwiftData

@Model

class Book {
    
    var title: String
    var author: String
    var genre: String
    var review: String
    var rating: Int
    let date = Date.now
    
    init(title: String, author: String, genre: String, review: String, rating: Int, date: Date) {
        self.title = title
        self.author = author
        self.genre = genre
        self.review = review
        self.rating = rating
        self.date = date
    }
}
