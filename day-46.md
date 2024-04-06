// Challenge 1: Change project 7 (iExpense) so that it uses NavigationLink for adding new expenses rather than a sheet. 
(Tip: The dismiss() code works great here, but you might want to add the navigationBarBackButtonHidden() modifier so they have to explicitly choose Cancel.)

// ContentView
            .toolbar {
                NavigationLink(destination: AddView(expenses: expenses)) {
                    Button("Add Expense", systemImage: "plus") {
                        showingAddExpense = true
                    }
                }
            }

// AddView

            .toolbar {
                ToolbarItem(placement: .confirmationAction) {
                    Button("Save") {
                        let item = ExpenseItem(name: name, type: type, amount: amount)
                        expenses.items.append(item)
                        dismiss()
                    }
                }
                ToolbarItem(placement: .cancellationAction) {
                    Button("Cancel") {
                        dismiss()
                    }
                    .navigationBarBackButtonHidden(true)
                    

// Challenge 2: Try changing project 7 so that it lets users edit their issue name in the navigation title rather than a separate textfield.

        NavigationStack {
            Form {
//                TextField("Name", text: $name)
                
                Picker("Type", selection: $type) {
                    ForEach(types, id: \.self) {
                        Text($0)
                    }
                }
                
                TextField("Amount", value: $amount, format: .currency(code: Locale.current.currency?.identifier ?? "USD"))
                    .keyboardType(.decimalPad)
            }
            .navigationTitle($name)
            .navigationBarTitleDisplayMode(.inline)

// Challenge 3: Return to project 8 (Moonshot), and upgrade it to use NavigationLink(value:). This means adding Hashable conformance, and thinking carefully how to use navigationDestination().

//  Mission.swift

import Foundation

struct Mission: Codable, Identifiable, Hashable {
    struct CrewRole: Codable, Hashable {

//
//  OverviewGridView.swift
//  Moonshot
//
//  Created by Marco Studium on 01.04.24.
//

import SwiftUI

struct OverviewGridView: View {
    let astronauts: [String: Astronaut]
    let missions: [Mission]
    
    let columns = [
        GridItem(.adaptive(minimum: 150))
    ]
    var body: some View {
        ScrollView {
            LazyVGrid(columns: columns) {
                ForEach(missions) { mission in
                    NavigationLink(value: mission) {
                        VStack {
                            Image(mission.image)
                                .resizable()
                                .scaledToFit()
                                .frame(width: 100, height: 100)
                                .padding()
                            
                            VStack {
                                Text(mission.displayName)
                                    .font(.headline)
                                    .foregroundStyle(.white)
                                
                                Text(mission.formattedLaunchDate)
                                    .font(.caption)
                                    .foregroundStyle(.white.opacity(0.5))
                            }
                            .padding(.vertical)
                            .frame(maxWidth: .infinity)
                            .background(.lightBackground)
                            
                        }
                        .clipShape(.rect(cornerRadius: 10))
                        .overlay(
                            RoundedRectangle(cornerRadius: 10)
                                .stroke(.lightBackground)
                        )
                    }
                    .navigationDestination(for: Mission.self) { mission in
                        MissionView(mission: mission, astronauts: astronauts)
                    }
                }
            }
            .padding([.horizontal, .bottom])
        }
    }
}

#Preview {
    OverviewGridView(astronauts: Bundle.main.decode("astronauts.json"), missions: Bundle.main.decode("missions.json"))
        .preferredColorScheme(.dark)
}

//
//  OverviewListView.swift
//  Moonshot
//
//  Created by Marco Studium on 01.04.24.
//

import SwiftUI

struct OverviewListView: View {
    let astronauts: [String: Astronaut]
    let missions: [Mission]
    
    var body: some View {
        List(missions) { mission in
            NavigationLink(value: mission) {
                HStack(alignment: .center) {
                    Image(mission.image)
                        .resizable()
                        .scaledToFit()
                        .frame(width: 50, height: 50)
                        .padding()
                    
                    VStack(alignment: .leading) {
                        Text(mission.displayName)
                            .font(.headline)
                            .foregroundStyle(.white)
                        
                        Text(mission.formattedLaunchDate)
                            .font(.caption)
                    }
                }
                .navigationDestination(for: Mission.self) { mission in
                    MissionView(mission: mission, astronauts: astronauts)
                }
            }
            .listRowBackground(Color.darkBackground)
        }
        .listStyle(.plain)
    }
}

#Preview {
    OverviewListView(astronauts: Bundle.main.decode("astronauts.json"), missions: Bundle.main.decode("missions.json"))
        .preferredColorScheme(.dark)
}

