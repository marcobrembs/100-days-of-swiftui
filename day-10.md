//// Structs
//
//struct Album {
//    let title: String
//    let artist: String
//    let year: Int
//
//    func printSummary() {
//        print("\(title) \(year) by \(artist)")
//    }
//}
//
//let red = Album(title: "Red", artist: "Taylor Swift", year: 2012)
//let wings = Album(title: "Wings", artist: "BTS", year: 2016)
//
//print(red.title)
//print(wings.title)
//
//red.printSummary()
//wings.printSummary()
//
//struct Employee {
//    let name: String
//    var vacationRemaining = 14
//    // constants and variables inside a struct are called properties of the struct
//    
//    mutating func takeVacation(days: Int) {
//        // function inside a struct are called methods
//        if vacationRemaining > days {
//            vacationRemaining -= days
//            print("I´m going on vacation!")
//            print("Days remaining: \(vacationRemaining)")
//        } else {
//            print("Oops! There aren´t enough days remaining.")
//        }
//    }
//}
//
//var archer = Employee.init(name: "Sterling Archer", vacationRemaining: 14)
//// name: "Sterling Archer", vacationRemaining: 14 -> Initializer (Init) for the struct
//// constant or variables created from our own struct is called (unique) instance
//archer.takeVacation(days: 5)
//print(archer.vacationRemaining)
//
//let kane = Employee(name: "Lana Kane")
//let poovey = Employee(name: "Pam Poovey", vacationRemaining: 35)
//print(poovey.vacationRemaining)

// Computed property

//struct Employee {
//    let name: String
//    var vacationAllocated = 14
//    var vacationTaken = 0
//
//    var vacationRemaining: Int {
//        get {
//            vacationAllocated - vacationTaken
//        }
//        
//        set {
//            vacationAllocated = vacationTaken + newValue
//        }
//    }
//}
//
//
//var archer = Employee(name: "Sterling Archer", vacationAllocated: 14)
//archer.vacationTaken += 4
//archer.vacationRemaining = 5
//print(archer.vacationAllocated)
//
//
//// Take action when a property changes
//
//struct Game {
//    var score = 0 {
//        didSet {
//            print("Score is now \(score)")
//            // print score whenever the score changes
//        }
//    }
//}
//
//var game = Game()
//game.score += 10
//game.score += 3
//game.score += 1
//
//struct App {
//    var contacts = [String]() {
//        willSet {
//            print("Current value is \(contacts)")
//            print("New value will be: \(newValue)")
//        }
//        
//        didSet {
//            print("There are now \(contacts.count) contacts")
//            print("Old value was: \(oldValue)")
//        }
//    }
//}
//
//var app = App()
//app.contacts.append("Adrian E")
//app.contacts.append("Allen W")
//app.contacts.append("Ish S")


// Custom initializers

struct Player {
    let name: String
    let number: Int
    
    init(name: String) {
        // no func keyword
        // no explicit return type
        self.name = name
        // self.name -> the name property that belongs to my Player instance
        number = Int.random(in: 1...99)
    }
    // by the time the initializer finishes, all properties must have a (default) value!
}

let player = Player(name: "Megan R")
print(player.number)
