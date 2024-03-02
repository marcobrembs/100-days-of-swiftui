// if statements

// Scoring

let speed = 88
let percentage = 85
let age = 18

if speed >= 88 {
    print("Where we are going, we don´t need roads")
}

if percentage < 85 {
    print("Sorry, you´ve failed the test")
}

if age >= 18 {
    print("You´re eligible to vote")
}

// strings

let ourName = "David Lister"
let friendName = "Arnold Rimmer"

if ourName < friendName {
    print("It´s \(ourName) vs \(friendName)")
}

if ourName > friendName {
    print("It´s \(friendName) vs \(ourName)")
}

var numbers = [1, 2, 3]
numbers.append(4)
if numbers.count > 3 {
    numbers.remove(at: 0)
}
print(numbers)

let country = "Canada"
if country == "Australia" {
    print("G'day!")
}

let name = "Taylor Swift"
if name != "Anonymous" {
    print("Welcome \(name)")
}

var username = "taylorswift13"
if username.isEmpty {
    username = "Anonymous"
}
// .isEmpty == true -> .isEmpty
print("Welcome \(username)")


let voterAge = 17
if voterAge > 18{
    print("You can definetly vote in the next election")
} else if voterAge > 16 {
    print("You can probably vote in the next election")
}
else {
    print("You cannot vote in the next election")
}

let temp = 23
if temp > 20 {
    if temp < 30 {
        print("It´s a nice day")
    }
}
if temp > 20 && temp < 30 {
    print("It´s a nice day")
}

let userAge = 14
let hasParentalConsent = true

if userAge >= 18 || hasParentalConsent {
    print("\(username) has permission to buy the app")
}

if userAge >= 18 && hasParentalConsent {
    print("\(username) has permission to buy the app")
}

enum TransportOption {
    case airplane, helicopter, car, bicycle, escooter
}
let transport = TransportOption.airplane
// When we set the value for transport we need to be explicit that we’re referring to TransportOption.airplane. Once that has happened, we don’t need to write TransportOption any more because Swift knows transport must be some kind of TransportOption.

if transport == .airplane || transport == .helicopter {
    print("Let´s fly")
} else if transport == .car {
    print("Time to get stuck in traffic")
} else if transport == .bicycle {
    print("I hope there is a bike path")
} else {
    print("I´m going to hire a sooter now")
}


// switch statements
// switch cases must be exhaustive

let place = "Metropolis"
switch place {
case "Gotham":
    print("You´re Batman")
case "Mega-City One":
    print("You´re Judge Dredd")
case "Wakanda":
    print("You´re Black Panther")
default:
    print("Who are you?")
}
// no other case blocks should be after default

let day = 5
print("My true love gave to me...")

switch day {
case 5:
    print("5 golden rings")
    fallthrough
case 4:
    print("4 calling birds")
    fallthrough
case 3:
    print("3 French hens")
    fallthrough
case 2:
    print("2 turtle doves")
    fallthrough
default:
    print("A partridge in a pear tree")
}

// ternary conditional operator
// W What we check
// T What to do if it´s true
// F What to do if it´s false

let candidateAge = 18
let canCadidate = candidateAge >= 18 ? "Yes" : "No"
print(canCadidate)

let hour = 23
print(hour < 12 ? "It´s before noon" : "It´s after nooon")


let names = ["Jamie", "Kaylee", "Mal"]
let crewCount = names.isEmpty ? "No one" : "\(names.count) people"
print(crewCount)

enum Theme {
    case light, dark
}

let theme = Theme.dark

let background = theme == .dark ? "black" : "white"
print(background)
