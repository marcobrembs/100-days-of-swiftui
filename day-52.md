// Challenge 1: Improve the validation to make sure a string of pure whitespace is invalid.

//
//  Order.swift
//  CupcakeCorner
//
//  Created by Marco Studium on 09.04.24.
//

    var hasValidAddress: Bool {
        if name.isEmpty || streetAddress.isEmpty || city.isEmpty || zip.isEmpty {
            return false
        } else if name.trimmingCharacters(in: .whitespaces).isEmpty || streetAddress.trimmingCharacters(in: .whitespaces).isEmpty || city.trimmingCharacters(in: .whitespaces).isEmpty || zip.trimmingCharacters(in: .whitespaces).isEmpty {
            return false
        }
        else {
            return true
        }
    }


// Challenge 2: If our call to placeOrder() fails – for example if there is no internet connection – show an informative alert for the user.

//
//  CheckoutView.swift
//  CupcakeCorner
//
//  Created by Marco Studium on 09.04.24.
//

import SwiftUI

struct CheckoutView: View {
    var order: Order
    
    @State private var confirmationMessage = ""
    @State private var showingConfirmation = false
    
    @State private var alertMessage = ""
    @State private var showingAlert = false
    
    var body: some View {
        ScrollView {
            VStack {
                AsyncImage(url: URL(string: "https://hws.dev/img/cupcakes@3x.jpg"), scale: 3) { image in
                    image
                        .resizable()
                        .scaledToFit()
                } placeholder: {
                    ProgressView()
                }
                .frame(height: 233)
                
                Text("Your total cost is \(order.cost, format: .currency(code: "USD"))")
                    .font(.title)
                
                Button("Place Order") {
                    Task {
                        await placeOrder()
                    }
                }
                .padding()
            }
        }
        .navigationTitle("Check out")
        .navigationBarTitleDisplayMode(.inline)
        .scrollBounceBehavior(.basedOnSize)
        .alert("Thank you!", isPresented: $showingConfirmation) {
            Button("OK") { }
        } message: {
            Text(confirmationMessage)
        }
        .alert("Error", isPresented: $showingAlert) {
            Button("OK") { }
        } message: {
            Text(alertMessage)
        }
    }
    
    func placeOrder() async {
        guard let encoded = try? JSONEncoder().encode(order) else {
            print("Failed to encode order")
            return
        }
            let url = URL(string: "https://reqres.in/api/cupcakes")!
            var request = URLRequest(url: url)
            request.setValue("application/json", forHTTPHeaderField: "Content-Type")
            request.httpMethod = "POST"
            
        do {
            let (data, _) = try await URLSession.shared.upload(for: request, from: encoded)
            
            let decodedOrder = try JSONDecoder().decode(Order.self, from: data)
            confirmationMessage = "Your order for \(decodedOrder.quantity)x\(Order.types[decodedOrder.type].lowercased()) cupcakes is on its way!"
            showingConfirmation = true
        } catch {
            print("Check out failed: \(error.localizedDescription)")
            showingAlert = true
            alertMessage = "There was an error with placing your order. Please check your internet connection and try again."
        }
    }
}

#Preview {
    CheckoutView(order: Order())
}


// Challenge 3: For a more challenging task, try updating the Order class so it saves data such as the user's delivery address to UserDefaults.

//
//  Order.swift
//  CupcakeCorner
//
//  Created by Marco Studium on 09.04.24.
//

 var name = "" {
        didSet {
            UserDefaults.standard.set(name, forKey: "name")
        }
    }
    
    var streetAddress = "" {
        didSet {
            UserDefaults.standard.set(streetAddress, forKey: "streetAddress")
        }
    }
    
    var city = "" {
        didSet {
            UserDefaults.standard.set(city, forKey: "city")
        }
    }
    
    var zip = "" {
        didSet {
            UserDefaults.standard.set(zip, forKey: "zip")
        }
    }
    
    init() {
        if let savedName = UserDefaults.standard.string(forKey: "name") {
            self.name = savedName
        }
        if let savedStreetAddress = UserDefaults.standard.string(forKey: "streetAddress") {
            self.streetAddress = savedStreetAddress
        }
        if let savedCity = UserDefaults.standard.string(forKey: "city") {
            self.city = savedCity
        }
        if let savedZip = UserDefaults.standard.string(forKey: "zip") {
            self.zip = savedZip
        }
    }
