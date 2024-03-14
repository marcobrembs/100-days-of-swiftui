//
//  ContentView.swift
//  ViewsAndModifiers
//
//  Created by Marco Studium on 13.03.24.
//

import SwiftUI

struct CapsuleText: View {
    var text: String
    
    var body: some View {
        Text(text)
            .font(.largeTitle)
            .padding()
            .background(.blue)
            .clipShape(.capsule)
    }
}

struct Title: ViewModifier {
    func body(content: Content) -> some View {
        content
            .font(.largeTitle)
            .foregroundStyle(.white)
            .padding()
            .background(.blue)
            .clipShape(.rect(cornerRadius: 10))
    }
}

extension View {
    func titleStyle() -> some View {
        modifier(Title())
    }
}

struct Watermark: ViewModifier {
    var text: String
    
    func body(content: Content) -> some View {
        ZStack(alignment: .bottomTrailing) {
            content
            
            Text(text)
                .font(.caption)
                .foregroundStyle(.white)
                .padding(5)
                .background(.black)
        }
    }
}

extension View {
    func watermarked(with text: String) -> some View {
        modifier(Watermark(text: text))
    }
}

struct GridStack<Content: View>: View {
    let rows: Int
    let columns: Int
    @ViewBuilder let content: (Int, Int) -> Content
    
    var body: some View {
        VStack {
            ForEach(0..<rows, id: \.self) { row in
                HStack {
                    ForEach(0..<columns, id: \.self) { column in
                        content(row, column)
                    }
                }
            }
        }
    }
}

struct ContentView: View {
    
    @State private var useRedText = false
    
    var motto1: some View {
        Text("Draco dormiens")
    }
    
    let motto2 = Text("numquam titillandus")
    
    @ViewBuilder var spells: some View {
        Group {
            Text("Lumos")
            Text("Obliviate")
        }
    }

    
    var body: some View {
        
        Button("Hello world") {
            print(type(of: self.body))
        }
        .frame(maxWidth: 200, maxHeight: 200)
        .background(.red)
        
        Text("Hello again")
            .padding()
            .background(.blue)
            .padding()
            .background(.green)
            .padding()
            .background(.yellow)
            .padding()
            .background(.orange)
        
        // ternary operator
        Button("Hello again again") {
            useRedText.toggle()
        }
        .foregroundStyle(useRedText ? .red : .blue)
        
        VStack {
            Text("Apple")
                .font(.largeTitle)
            Text("Google")
            Text("Microsoft")
        }.font(.title)
        
        motto1
        motto2
            .foregroundStyle(.red)
        
        VStack(spacing: 10) {
            CapsuleText(text: "First")
                .foregroundColor(.white)
            CapsuleText(text: "Second")
                .foregroundColor(.yellow)
        }
        
        Text("Hello Paul")
            .modifier(Title())
        
        Text("Hello Emmi")
            .titleStyle()
        
        Color.blue
            .frame(width: 200, height: 100)
            .watermarked(with: "Hacking with Swift")
        
        GridStack(rows: 4, columns: 4) { row, col in
            Image(systemName: "\(row * 4 + col).circle")
            Text("R\(row) C\(col)")
        }
    }
}

#Preview {
    ContentView()
}
