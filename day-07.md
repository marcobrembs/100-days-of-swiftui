// functions

func showWelcome() {
    print("Welcome to my app")
    print("This prints out a new conversation")
}

showWelcome()
// function´s call site

let number = 139

if number.isMultiple(of: 2) {
    print("Even")
} else {
    print("Odd")
}

func printTimesTables(number: Int, end: Int) {
    // number & end are parameters -> placeholders
    for i in 1...12 {
        print("\(i) * \(number) is \(i * number)")
    }
}

printTimesTables(number: 5, end: 20)
// number: 5 and end: 20 are arguments -> actual values


// return values from functions

import Cocoa

let root = sqrt(169)
print(root)

func rollDice() -> Int {
    return Int.random(in: 1...6)
}

let result = rollDice()
print(result)


func sameString(string1: String, string2: String) {
    if string1.sorted() == string2.sorted() {
        print("These strings are the same")
    } else {
        print("These strings are different")
    }
}
sameString(string1: "abcd", string2: "cdab")

func areLettersIdentical(string1: String, string2: String) -> Bool {
    let first = string1.sorted()
    let second = string2.sorted()
    return first == second
}
print(areLettersIdentical(string1: "abcd", string2: "cdab"))

func areLettersIdenticalAlternative(string1: String, string2: String) -> Bool {
    string1.sorted() == string2.sorted()
    // expression -> code can be boiled down to a single value like true, false, "Hello" or 19
    // return statement can be removed if only one line of code inside the function and the one line actually returns the data
}
areLettersIdenticalAlternative(string1: "abcd", string2: "cdab")

func pythagoras(a: Double, b: Double) -> Double {
    sqrt(a * a + b * b)
}
let c = pythagoras(a: 3, b: 4)
print(c)


// return multiple values from functions
// tuples

func getUser() -> (firstName: String, lastName: String) {
    (firstName: "Taylor", lastName: "Swift")
}
let (firstName, _) = getUser()
print("Name: \(firstName)")


// customize parameter labels

let lyric = "I see a red door"
print(lyric.hasPrefix("I see"))

func isUpperCase(_ string: String) -> Bool {
    // _ -> no external name
    string == string.uppercased()
}
let string = "HELLO, WORLD"
let result1 = isUpperCase(string)

func printTimesTable2(for number: Int) {
    // for -> external parameter name
    // number -> internal parameter name
    for i in 1...12 {
        print("\(i) x \(number) is \(i * number)")
    }
}
printTimesTable2(for: 5)
