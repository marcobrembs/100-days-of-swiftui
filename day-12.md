// create own classes

class Game {
    var score = 0 {
        didSet {
            print("Score is now \(score)")
        }
    }
}

var newGame = Game()
newGame.score += 10


// inheritance

class Employee {
    let hours: Int
    
    init(hours: Int) {
        self.hours = hours
    }
    
    func printSummary() {
        print("I work \(hours) hours per day")
    }
}

final class Developer: Employee {
// inherit from parent class Employee -> can use the property hours
    func work() {
        print("I´m writing code for \(hours) hours")
    }
    
    override func printSummary() {
        print("I´m a developer who will sometimes work \(hours) hours a day, but other times will spend hours arguing about whether code should be intented using tabs or spaces.")
    }
}

final class Manager: Employee {
    func work() {
        print("I´m going to meetings for \(hours) hours")
    }
}

let robert = Developer(hours: 8)
let joseph = Manager(hours: 10)
robert.work()
joseph.work()

let novall = Developer(hours: 8)
novall.printSummary()


// add initializers for classes

class Vehicle {
    let isElectric: Bool
    
    init(isElectric: Bool) {
        self.isElectric = isElectric
    }
}

class Car: Vehicle {
    let isConvertible: Bool
    
    init(isElectric: Bool, isConvertible: Bool) {
        self.isConvertible = isConvertible
        super.init(isElectric: isElectric)
    }
}

let teslaX = Car(isElectric: true, isConvertible: false)


// copy classes

// clases are reference types
// share common data across the app

class User {
    var username = "Anonymous"
    
    func copy() -> User {
        let user = User()
        user.username = username
        return user
    }
}

var user1 = User()
var user2 = user1.copy()
user2.username = "Taylor"

print(user1.username)
print(user2.username)


// create a deinitializer for a class

class User {
    let id: Int
    
    init(id: Int) {
        self.id = id
        print("User \(id): I´m alive")
    }
    
    deinit {
        print("User \(id): I´m dead")
    }
}

var users = [User]()

for i in 1...3 {
    let user = User(id: i)
    print("User \(user.id): I´m in control")
    users.append(user)
}

print("Loop is finished")
users.removeAll()
print("Array is clear")


 work with variables inside classes

class User {
    var name = "Paul"
}

var user = User()
user.name = "Taylor"
user = User()
print(user.name)


// Checkpoint 7
//Make a class hierarchy for animals.
//Start with Animal. Add a legs property for the number of legs an animal has.
//Make Dog a subclass of Animal, giving it a speak method that prints a dog barking string, but each subclass should print something different.
//Make Corgi and Poodle subclasses of Dog.
//Make Cat an Animal subclass. Add a speak method, with each subclass printing something different, and an is Tame Boolean, set with an initializer.
//Make Persian and Lion as subclasses of Cat.

class Animal {
    var legs: Int
    
    init(legs: Int) {
        self.legs = legs
    }
}

class Dog: Animal {
    func speak() {
        print("Dog with \(legs) legs speaks: Wuff wuff wuff")
    }
}

class Corgi: Dog {
    override func speak() {
        print("Corgi with \(legs) legs speaks: wuff wuff")
    }
}

class Poodle: Dog {
    override func speak() {
        print("Poodle with \(legs) legs speaks: wuff wuff")
    }
}

class Cat: Animal {
    var isTame: Bool
    
    func speak() {
        print("Cat with \(legs) legs speaks: Miau miau miau")
    }
    
    init(legs: Int, isTame: Bool) {
        self.isTame = isTame
        super.init(legs: legs)
    }
}

class Persian: Cat {
    override func speak() {
        print("Persian (isTame = \(isTame)) with \(legs) legs speaks: miau miau")
    }
}

class Lion: Cat {
    override func speak() {
        print("Lion (isTame = \(isTame)) with \(legs) legs speaks: miau miau")
    }
}

let dogsD = Dog(legs: 8)
dogsD.speak()
let catsL = Lion(legs: 4, isTame: true)
catsL.speak()
