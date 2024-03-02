How to create a variables and constants?

Coding Convention Camelcase
Example: playerName

Prefer constants over variables whenever possible

How to create strings

How to store whole numbers

How to store decimal numbers


**Playground**

import Cocoa

var greeting = "Hello, playground"

var name = "Ted"
name = "Keeley"
name = "Rebecca"
print(name)

let character = "Roy"

var playerName = "Jamie"
print(playerName)

playerName = "Nathan"
print(playerName)

playerName = "Dani"
print(playerName)

print(playerName.count)
// When just reading data, you don´t need ()

print(playerName.uppercased())
// When doing something with the data, you need the ()

let score = 100_000_00

let higherScore = score + 2

let double = 3.0


var counter = 5
counter += 10
// compound assignment operator

let number = 120
print(number.isMultiple(of: 3))
print(120.isMultiple(of: 3))

let double1 = 12.1
var double2 = 4.3765
let int = 3

double2 *= 2.2
