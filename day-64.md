//
//  ContentView.swift
//  Instafilter
//
//  Created by Marco Studium on 23.04.24.
//

import PhotosUI
import StoreKit
import SwiftUI

//// Loading photos from the user´s photo library
//
//struct ContentView: View {
//    @State private var pickerItems = [PhotosPickerItem]()
//    @State private var selectedImages = [Image]()
//    
//    var body: some View {
//        VStack {
//            PhotosPicker(selection: $pickerItems, maxSelectionCount: 5, matching: .any(of: [.images, .not(.screenshots)])) {
//                Label("Select a picture", systemImage: "photo")
//            }
//            
//            ScrollView {
//                ForEach(0..<selectedImages.count, id: \.self) { i in
//                    selectedImages[i]
//                        .resizable()
//                        .scaledToFit()
//                }
//            }
//        }
//        .onChange(of: pickerItems) {
//            Task {
//                selectedImages.removeAll()
//                
//                for item in pickerItems {
//                    if let loadedImage = try await item.loadTransferable(type: Image.self) {
//                        selectedImages.append(loadedImage)
//                    }
//                }
//            }
//        }
//    }
//}

//// How to let the user share content with ShareLink
//
//struct ContentView: View {
//    var body: some View {
//        let example = Image(.example)
//        
//        ShareLink(item: URL(string: "https://wwww.hackingwithswift.com")!, subject: Text("Learn Swift here"), message: Text("Check out the 100 Days of SwiftUI"))
//        ShareLink(item: URL(string: "https://www.hackingwithswift.com")!) {
//            Label("Spread the word about Swift", systemImage: "swift")
//        }
//        ShareLink(item: example, preview: SharePreview("Singapore Airport", image: example)) {
//            Label("Click to share", systemImage: "house")
//        }
//    }
//}

// How to ask the user to leave an App Store review
struct ContentView: View {
    @Environment(\.requestReview) var requestReview
    var body: some View {
        Button("Leave a review") {
            requestReview()
        }
    }
}

#Preview {
    ContentView()
}
