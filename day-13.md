// create and use protocols

protocol Vehicle { // list of bare requirements
    var name: String { get } // read only
    var currentPassengers: Int { get set } // read and write
    func estimateTime(for distance: Int) -> Int
    func travel(distance: Int)
}

protocol CanBeElectric {
    
}

struct Car: Vehicle, CanBeElectric { // adopt / conform the protocol
    let name = "Car"
    var currentPassengers = 1
    
    func estimateTime(for distance: Int) -> Int {
        distance / 50
    }
    
    func travel(distance: Int) {
        print("I´m driving \(distance)km")
    }
    
    func openSunroof() {
        print("It´s a nice day")
    }
}

struct Bicycle: Vehicle {
    let name = "Bicycle"
    var currentPassengers = 1
    
    func estimateTime(for distance: Int) -> Int {
        distance / 10
    }
    
    func travel(distance: Int) {
        print("I´m cicyling \(distance)km")
    }
}

func commute(distance: Int, using vehicle: Vehicle) {
    if vehicle.estimateTime(for: distance) > 100 {
        print("That´s too slow! I´ll try a different vehicle")
    } else {
        vehicle.travel(distance: distance)
    }
}

func getTravelEstimates(using vehicles: [Vehicle], distance: Int) {
    for vehicle in vehicles {
        let estimate = vehicle.estimateTime(for: distance)
        print("\(vehicle.name): \(estimate) hours to travel \(distance)km")
    }
}

let car = Car()
commute(distance: 100, using: car)

let bike = Bicycle()
commute(distance: 50, using: bike)

getTravelEstimates(using: [car, bike], distance: 150)


// opaque return types

protocol View { }

func getRandomNumber() -> some Equatable {
    Double.random(in: 1...6)
}

func getRandomBool() -> some Equatable {
    Bool.random()
}

print(getRandomNumber() == getRandomNumber())


// create and use extensions

import Cocoa

var quote = "   The truth is rarely pure and never simple    "
// var trimmed = quote.trimmingCharacters(in: .whitespacesAndNewlines)

extension String {
    func trimmed() -> String { // option 1
        self.trimmingCharacters(in: .whitespacesAndNewlines)
    }
    
    mutating func trim() { // option 2
        self = self.trimmed()
    }
    
    var lines: [String] {
        self.components(separatedBy: .newlines)
    }
}

var trimmed = quote.trimmed() // option 1

quote.trim() // option 2

let lyrics = """
But I keep cruising
Can´t stop, won´t stop moving
It´s like I got this music in my mind
Saying it´s gonna be alright
"""

print(lyrics.lines.count)

struct Book {
    let title: String
    let pageCount: Int
    let readingHours: Int
}

extension Book {
    init(title: String, pageCount: Int) { // custom initializer inside an extension
        self.title = title
        self.pageCount = pageCount
        self.readingHours = pageCount / 50
    }
}

let lotr = Book(title: "Lord of the Rings", pageCount: 1178, readingHours: 24)


// create and use protocol extensions

extension Collection {
    // Collection includes dictionaries, arrays, struct etc.
    var isNotEmpty: Bool {
        isEmpty == false
    }
}
let guests = ["Mario", "Luigi", "Preach"]

if guests.isNotEmpty {
    print ("Guest count: \(guests.count)")
}

protocol Person {
    var name: String { get }
    func sayHello()
}

extension Person {
    func sayHello() {
        print("Hi, I´m \(name)")
    }
}

struct Employee: Person {
    let name: String
}

let taylor = Employee(name: "Taylor Swift")
taylor.sayHello()


// Checkpoint 8
//Make a protocol that describes a building.
//Your protocol should require the following:
//A property storing how many rooms it has.
//A property storing the cost as an integer.
//A property storing the name of the estate agent selling the building.
//A method for printing the sales summary of the building.
//Create two structs, House and Office, that conform to it


protocol Building {
    var roomCount: Int { get }
    var rentCost: Int { get }
    var estateAgent: String { get }
    func salesSummary()
}

struct House: Building {
    var name = "House"
    var roomCount: Int {
        seats/2
    }
    var seats: Int
    var rentCost: Int
    var estateAgent: String
    
    func salesSummary() {
        print("The \(name) building has \(seats) seats in \(roomCount) rooms, costs \(rentCost) and can be viewed by calling the real estate agent \(estateAgent).")
    }
}

struct Office: Building {
    var name = "Office"
    var roomCount: Int
    var rentCost: Int
    var estateAgent: String
    
    func salesSummary() {
        print("The \(name) building has \(roomCount) rooms, costs \(rentCost) and can be viewed by calling the real estate agent \(estateAgent).")
    }
}

extension Office {
    init(roomCount: Int, estateAgent: String) {
        self.roomCount = roomCount
        self.rentCost = roomCount * 5_000
        self.estateAgent = estateAgent
    }
}

let house = House(seats: 8, rentCost: 1_200, estateAgent: "Taylor Swift Agency")
house.salesSummary()

let office = Office(roomCount: 4, estateAgent: "Eminem Agency")
office.salesSummary()
