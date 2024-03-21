//
//  ContentView.swift
//  Animations
//
//  Created by Marco Studium on 21.03.24.
//

import SwiftUI

struct ContentView: View {
    
    @State private var animationAmount = 0.0
    
    var body: some View {
        //              Implicit animations
                Button("Tap me") {
        //            animationAmount += 1
                }
                .padding(50)
                .background(.red)
                .foregroundStyle(.white)
                .clipShape(.circle)
        //        .scaleEffect(animationAmount)
        //        .blur(radius: (animationAmount - 1) * 3)
                .overlay(
                    Circle()
                        .stroke(.red)
                        .scaleEffect(animationAmount)
                        .opacity(2 - animationAmount)
                        .animation(
                            .easeInOut(duration: 1)
                                .repeatForever(autoreverses: false),
                            value: animationAmount
                        )
                    )
                .onAppear {
                    animationAmount = 2
                }
        
                print(animationAmount)
        //      animating bindings
                return VStack {
                    Stepper("Scale amount", value: $animationAmount.animation(
                        .easeInOut(duration: 1)
                            .repeatCount(3, autoreverses: true)
                    ), in: 1...10)
        
                    Spacer()
        
                    Button("Tap me") {
                        animationAmount += 1
                    }
                    .padding(40)
                    .background(.red)
                    .foregroundStyle(.white)
                    .clipShape(.circle)
                    .scaleEffect(animationAmount)
                }
        
        Button("Tap me") {
            // explicit animations
            withAnimation(.spring(duration: 1, bounce: 0.5)) {
                animationAmount += 360
            }
        }
        .padding(50)
        .background(.red)
        .foregroundStyle(.white)
        .clipShape(.circle)
        .rotation3DEffect(
            .degrees(animationAmount), axis: (x: 1, y: 1, z: 0)
        )
    }
}

#Preview {
    ContentView()
}
