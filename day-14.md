// Optionals

let opposites = ["Mario": "Wario", "Luigi": "Waluigi"]
if let marioOpposite = opposites["Mario"] {
    print("Mario´s opposite is \(marioOpposite)")
}

var username: String? = nil

if let unwrappedName = username {
    print("We got a user: \(unwrappedName)")
} else {
    print("The optional was empty.")
}

func square(number: Int) -> Int {
    number * number
}

var number: Int? = nil
number = 3

if let number = number { 
    // creating a second (non-optional) temporary variable with the same name "number" which works only in the condition -> shadowing
    // before and after the condition, we work with the optional number
    print(square(number: number))
} else {
    print("There is no number defined yet.")
}
// unwrap the optional


// unwrap optionals with guard

func printSquare(of Number: Int?) {
    guard let number = number else {
        print("Missing input")
        return
    }
    
    print ("\(number) x \(number) is \(number * number)")
}

var myVar: Int? = 3

if let unwrapped = myVar {
    // Run if myVar has a value inside
}

guard let unwrapped = myVar else {
    // Run if myVar doesn´t have a value inside
}


// unwrap optionals with nil coalescing

let captains = [
    "Enterprise": "Picard",
    "Voyager": "Janeway",
    "Defiant": "Sisko"
]

let new = captains["Serenity"] ?? "N/A"
// new won´t be an optional string
print(new)

let tvShows = ["Archer", "Babylon 5", "Ted Lasso"]
let favorite = tvShows.randomElement() ?? "None"

struct Book {
    let title: String
    let author: String?
}

let book = Book(title: "Beowulf", author: nil)
let author = book.author ?? "Anonymous"
print(author)


let input = ""
let number2 = Int(input) ?? 0
print(number2)


// multiple optionals using optional chaining

let names = ["Arya", "Bran", "Robb", "Sansa"]
let chosen = names.randomElement()?.uppercased() ?? "No one"
print("Next in line: \(chosen)")

struct Book {
    let title: String
    let author: String?
}

var book: Book? = nil
let author = book?.author?.first?.uppercased() ?? "A"
print(author)


// handle function failure with optionals

enum UserError: Error {
    case badID, networkFailed
}

func getUser(id: Int) throws -> String {
    throw UserError.networkFailed
}

if let user = try? getUser(id: 23) {
    print("User: \(user)")
}

let user = (try? getUser(id: 23)) ?? "Anonymous"
print(user)


// Checkpoint 9

func numbers(_ numbers: [Int]?) -> Int { numbers?.randomElement() ?? Int.random(in: 1...100)}
print(numbers([]))
