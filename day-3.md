How to store truth with booleans

How to join strings together

**Playground**

let goodDogs = true

var gameOver = false
print(gameOver)
gameOver.toggle()
print(gameOver)

print(120.isMultiple(of: 3))

var isAuthenticated = true
isAuthenticated = !isAuthenticated
print(isAuthenticated)
isAuthenticated = !isAuthenticated
print(isAuthenticated)

let firstPart = "Hello, "
let secondPart = "world"
let greeting = firstPart + secondPart
print(greeting)

let people = "Haters"
let action = "hate"
let lyric = people + " gonna " + action
// Concatenation

let name = "Taylor"
let age = 26
let message = "Hello, my name is \(name) and I am \(age) years old."
print(message)
// String interpolation: place data into strings

print("5 x 5 is \(5 * 5)")


let celsius = 3.0
var fahrenheit = celsius * 9.0 / 5.0 + 32.0
print("Celsius: \(celsius)°C")
print("Fahrenheit: \(fahrenheit)°F")
