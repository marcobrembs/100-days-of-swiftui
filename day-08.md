// default values for parameters

var characters = ["Lana", "Pam", "Ray", "Sterling"]
print(characters.count)
characters.removeAll(keepingCapacity: true)
// default value for parameter keepingCapacity
// remove the items, but leave the array able to hold 4 items
print(characters.count)


// handle errors in functions

enum PasswordError: Error {
    case short, obvious
}

func checkPassword(_ password: String) throws -> String {
    if password.count < 5 {
        throw PasswordError.short
    }
    if password == "12345" {
        throw PasswordError.obvious
    }
    // throw -> can throw an error but is not a must
    
    if password.count < 8 {
        return "OK"
    } else if password.count < 10 {
        return "Good"
    } else {
        return "Excellent"
    }
}

// Step 1: start a block of code that might throw errors by saying do {
// Step 2: call one or more throwing functions by saying try
// Step 3: catch block to handle any errors that come back

let string = "12345"

do {
    let result = try checkPassword(string)
    print("Password rating: \(result)")
} catch PasswordError.short {
    print("Please use a longer password")
} catch PasswordError.obvious {
    print("I have the same combination on my luggage")
} catch {
    print("There was an error")
}


// Checkpoint 4
// write a function to calculate the square root of a number from 1 to 10,000
// show error "out of bounds" if the number is not in that range
// show error "no root" if the square root cannot be found as an integer
// only consider integer square roots


enum CalculationError: Error {
    case outOfBounds, noRoot
}

func squareRoot(_ number: Int) throws -> Int {
    if number < 1 || number > 10_000 {
        throw CalculationError.outOfBounds
    }
    for i in 1...100 {
        if number == i * i {
            return i
        }
    }
    throw CalculationError.noRoot
}

let integer = 16

do {
    let result = try squareRoot(integer)
    print("The square root of \(integer) is \(result).")
} catch CalculationError.outOfBounds {
    print("The number \(integer) is too low or too high. Please choose a number between 1 and 10.000.")
} catch CalculationError.noRoot {
    print("The square root of number \(integer) cannot be calculated.")
} catch {
    print("Error")
}
