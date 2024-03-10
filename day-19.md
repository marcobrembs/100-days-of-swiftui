//  WeConvert

import SwiftUI

struct ContentView: View {
    @State private var inputNumber = 0.0
    
    private let LengthUnit = ["meters", "kilometers", "feet", "yard", "miles"]
    @State private var selectedInputUnit = "meters"
    @State private var selectedOutputUnit = "meters"
            
    var outputNumberMeter: Double {
        // convert selected input unit to meters
        if selectedInputUnit == "kilometers" {
            return inputNumber * 1000
        } else if selectedInputUnit == "feet" {
            return inputNumber * 0.3048
        } else if selectedInputUnit == "yard" {
            return inputNumber * 0.9144
        } else if selectedInputUnit == "miles" {
            return inputNumber * 1_609.344
        } else {
            return inputNumber
        }
    }
    
    var outputNumber: Double {
        // convert meters to selected output unit
        if selectedOutputUnit == "kilometers" {
            return outputNumberMeter / 1000
        } else if selectedOutputUnit == "feet" {
            return outputNumberMeter / 0.3048
        } else if selectedOutputUnit == "yard" {
            return outputNumberMeter / 0.9144
        } else if selectedOutputUnit == "miles" {
            return outputNumberMeter / 1_609.344
        } else {
            return outputNumberMeter
        }
    }
    
    var body: some View {
        NavigationStack {
            Form {
                Section("Your input unit") {
                    TextField("0,00", value: $inputNumber, format: .number).keyboardType(.decimalPad)
                    Picker("Input unit", selection: $selectedInputUnit) {
                        ForEach(LengthUnit, id: \.self) { unit in
                            Text(unit)
                        }
                    }
                }
                
                Section("Your output unit") {
                    Text(outputNumber, format: .number)
                    Picker("Output unit", selection: $selectedOutputUnit) {
                        ForEach(LengthUnit, id: \.self) { unit in
                            Text(unit)
                        }
                    }
                }
                
            } .navigationTitle("WeConvert")
        }
    }
}

#Preview {
    ContentView()
}
