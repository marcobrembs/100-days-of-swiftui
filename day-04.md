// type inference
let surname = "Lasso"
let score = 0
 
// type annotation
let firstname: String = "Ted"
let halftimescore: Int = 1
var finalscore: Double = 0

let playerName: String = "Roy"
let luckyNumber: Int = 13
let pi: Double = 3.141
var isAuthenticated: Bool = false
var albums: [String] = ["Red", "Fearless"]
var user: [String: String] = ["id": "@twostraws"]
var books: Set<String> = Set([
    "The Bluest Eye",
    "Foundation",
    "Girl, Woman, Other"
])

enum UiStyle {
    case light, dark, system
}
var style: UiStyle = UiStyle.light
style = .dark

let username: String
// type annotation needed if no inital value assigned
// lots of complex logic
username = "@twostraws"
// lots more complex logic
print(username)

var harryPotter: [String] = ["Harry", "Ron", "Hermione", "Harry"]
print(harryPotter)
print(harryPotter.count)
// number of items

var harryPotterUnique: Set<String> = Set(harryPotter)
print(harryPotterUnique)
print(harryPotterUnique.count)
// number of unique items
