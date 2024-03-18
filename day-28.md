//  BetterRest

import CoreML
import SwiftUI

struct ContentView: View {
    
    @State private var wakeUp = defaultWakeTime
    @State private var sleepAmount = 8.0
    @State private var coffeeAmount = 1
    
    static var defaultWakeTime: Date {
        var components = DateComponents()
        components.hour = 7
        components.minute = 0
        return Calendar.current.date(from: components) ?? .now
    }
    
    private var calcuateBedTime: some View {
        do {
            let config = MLModelConfiguration()
            let model = try SleepCalculator(configuration: config)
            
            let components = Calendar.current.dateComponents([.hour, .minute], from: wakeUp)
            let hour = (components.hour ?? 0) * 60 * 60
            let minute = (components.minute ?? 0) * 60
            
            let prediction = try model.prediction(wake: Int64(hour + minute), estimatedSleep: sleepAmount, coffee: Int64(coffeeAmount))
            
            let sleepTime = wakeUp - prediction.actualSleep
            
            return Text("Bed time: \(sleepTime, format: .dateTime.hour().minute())")
        }
        catch {
            return Text("There was a problem calculating your bedtime")
        }
    }
    
    var body: some View {
        NavigationStack {
            Form {
                Section("When do you want to wake up?") {
                    DatePicker("Please enter a time", selection: $wakeUp, displayedComponents: .hourAndMinute)
                }
                Section("Desired amount of sleep") {
                    Stepper("You want to sleep \(sleepAmount.formatted()) hours", value: $sleepAmount, in: 4...12, step: 0.25)
                }
                Section("Daily coffe amount picker") {
                    Picker(selection: $coffeeAmount, label: Text("How much coffee do you drink?")) {
                        ForEach(1..<21) {number in
                            Text("\(number)")
                        }
                    }.pickerStyle(.navigationLink)
                }
                calcuateBedTime
                    .font(.headline)
            }
            .navigationTitle("BetterRest")
        }
    }
    
}

#Preview {
    ContentView()
}
