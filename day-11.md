// Access controls

struct BankAccount {
    private(set) var funds = 0
    
    mutating func deposit(amount: Int) {
        funds += amount
    }
    
    mutating func withdraw(amount: Int) -> Bool {
        if funds > amount {
            funds -= amount
            return true
        } else {
            return false
        }
    }
}

var account = BankAccount()
account.deposit(amount: 100)

let success = account.withdraw(amount: 200)

if success {
    print("Withdrew money successfully")
} else {
    print("Failed to get the money")
}

// private          Don´t let anything outside the struct use this
// fileprivate      Don´t let anyting outside the current file use this
// public           Let anyone, anywhere use this
// private(set)     Let anyone read this property, but only the internal methods can modify it


// Static properties and methods

struct School {
    static var studentCount = 0
    // static means the variable (or function) belong to the struct itself and not to the individual instance of the School
    
    static func add(student: String) {
        print("\(student) has joined the course")
        studentCount += 1

    }
}

School.add(student: "Taylor Swift")
print(School.studentCount)

// self     The current value of a struct   55, "Hello", true
// Self     The current type of a struct    Int, String, Bool

struct AppData {
    static let version = "1.3 beta 2"
    static let saveFilename = "settings.json"
    static let homeURL = "https://www.hackingwithswift.com"
}
// use case 1: organize common data in apps

struct Employee {
    let username: String
    let password: String
    
    static let example = Employee(username: "cfederighi", password: "h4irf0rce0ne")
}
// use case 2: create examples of my struct

// Checkpoint 6
// create struct to store information about a car: model, number of seats & current gear
// add method to change gears up and down
// include access control
// don´t allow invalid gears

struct Car {
    let carModel: String
    let numberOfSeats: Int
    private(set) var currentGear = 1 {
        didSet { currentGear = min(max(currentGear, 1), 10) }
    }
    
    enum GearDirection {
        case up, down, neutral
    }
    
    mutating func changeGear(_ direction: GearDirection ) {
        switch direction {
        case .up : currentGear += 1
            if currentGear > 10 { currentGear = 10 }
        case .down : currentGear -= 1
            if currentGear < 1 { currentGear = 1 }
        case.neutral : currentGear = 1
        }
        print("The car model \(carModel) is in gear \(currentGear)")
    }
}

var audi = Car(carModel: "Audi", numberOfSeats: 4, currentGear: 2)
audi.changeGear(.up)
audi.changeGear(.down)
audi.changeGear(.up)
audi.changeGear(.neutral)

var vw = Car(carModel: "VW", numberOfSeats: 5, currentGear: 3)
vw.changeGear(.up)
