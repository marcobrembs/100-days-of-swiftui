//
//  ContentView.swift
//  Flashzilla
//
//  Created by Marco Brembs on 27.05.24.
//

import SwiftUI

func withOptionalAnimation<Result>(_ animation: Animation? = .default, _ body: () throws -> Result) rethrows -> Result {
    if UIAccessibility.isReduceMotionEnabled {
        return try body()
    } else {
        return try withAnimation(animation, body)
    }
}

struct ContentView: View {
    
    //How to use gestures in SwiftUI
    // Disabling user interactivity with allowsHitTesting()
    // Triggering events repeatedly using a time
    // How to be notified when your SwiftUI app moves to the background
    // Supporting specific accessibility needs with SwiftUI
    
    @State private var offset = CGSize.zero
    @State private var isDragging = false
    
    let timer = Timer.publish(every: 1, tolerance: 0.5, on: .main, in: .common).autoconnect()
    @State private var counter = 0
    
    @Environment(\.scenePhase) var scenePhase
    
    @Environment(\.accessibilityDifferentiateWithoutColor) var accessibilityDifferentiateWithoutColor
    
    @Environment(\.accessibilityReduceMotion) var accessibilityReduceMotion
    @State private var scale = 1.0
    
    @Environment(\.accessibilityReduceTransparency) var accessibilityReduceTransparency
    
    var body: some View {
        //        let dragGesture = DragGesture()
        //            .onChanged { value in
        //                offset = value.translation
        //            }
        //            .onEnded { _ in
        //                withAnimation {
        //                    offset = .zero
        //                    isDragging = false
        //                }
        //            }
        //
        //        let pressGesture = LongPressGesture()
        //            .onEnded { value in
        //                withAnimation {
        //                    isDragging = true
        //                }
        //            }
        //
        //        let combined = pressGesture.sequenced(before: dragGesture)
        //
        //        Circle()
        //            .fill(.red)
        //            .frame(width: 64, height: 64)
        //            .scaleEffect(isDragging ? 1.5 : 1)
        //            .offset(offset)
        //            .gesture(combined)
        //
        //        VStack {
        //            Text("Hello")
        //
        //            Spacer()
        //                .frame(height: 100)
        //
        //            Text("World")
        //        }
        //        .contentShape(.rect)
        //        .onTapGesture {
        //            print("VStack tapped")
        //        }
        //
        //
        //        Text("Hello, world!")
        //            .onReceive(timer) { time in
        //                if counter == 5 {
        //                    timer.upstream.connect().cancel()
        //                } else {
        //                    print("The time is now \(time)")
        //                }
        //
        //                counter += 1
        //            }
        //    }
        //
        //    func cancelTimer() {
        //        timer.upstream.connect().cancel()
        //    }
        //
        //        Text("Hello, world!")
        //            .onChange(of: scenePhase) { oldPhase, newPhase in
        //                if newPhase == .active {
        //                    print("Active")
        //                } else if newPhase == .inactive {
        //                    print("Inactive")
        //                } else if newPhase == .background {
        //                    print("Background")
        //                }
        //            }
        
        HStack {
            if accessibilityDifferentiateWithoutColor {
                Image(systemName: "checkmark.circle")
            }
            
            Text("Success")
        }
        .padding()
        .background(accessibilityDifferentiateWithoutColor ? .black : .green)
        .foregroundStyle(.white)
        .clipShape(.capsule)
        
        Button("Hello, world!") {
            withOptionalAnimation {
                scale *= 1.5
            }
        }
        .scaleEffect(scale)
        
        Text("Hello, world")
            .padding()
            .background(accessibilityReduceTransparency ? .black : .black.opacity(0.5))
            .foregroundStyle(.white)
            .clipShape(.capsule)
        
    }
}
#Preview {
    ContentView()
}
