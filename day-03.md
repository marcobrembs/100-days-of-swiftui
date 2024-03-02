// Arrays

var beatles = ["John", "Paul"]
beatles.append("Allen")
print(beatles)

var scores = Array<Int>()
scores.append(100)
scores.append(80)
scores.append(85)
print(scores)

var albums = ["Folklore"]
albums.append("Fearless")
albums.append("Red")

print(albums.count)
albums.remove(at: 0)
print(albums)
let bondMovies = ["Casino Royale", "Spectre", "No Time to Die"]
print(bondMovies.contains("Frozen"))

let cities = ["London", "Tokyo", "Rome", "Budapest"]
print(cities.sorted())

let presidents = ["Bush", "Obama", "Trump", "Biden"]
let reversedPresidents = presidents.reversed()
print(reversedPresidents)

var employee = ["Taylor Swift", "Singer", "Nashville"]
print(employee[0])
employee.remove(at: 1)
print(employee)


// Dictionaries

let employee2 = [
    "name": "Taylor Swift",
    "job": "Singer",
    "location": "Nashville"
]

print(employee2["name", default: "Unknown"])
print(employee2["status", default: "Unknown"])
print(employee2["manager", default: "Unknown"])

// String (keys & values) dictionary


let hasGraduadet = [
    "Eric": false,
    "Maeve": true,
    "Otis": false
]

// String (key) & Boolean (value) dictionary


let olympics = [
    2012: "London",
    2016: "Rio de Janeiro",
    2021: "Tokyo"
]

print(olympics[2012, default: "Unknown"])

// Integer (key) & String (value) dictionary

var heights = [String: Int]()
// Empty dictionary
heights["Marco"] = 175
heights["Paul"] = 180

var archEnemies = [String: String]()
archEnemies["Batman"] = "The Joker"
archEnemies["Superman"] = "Lex Luther"
archEnemies["Batman"] = "Penguin"
// Overwrite previous value for the key Batman
print(archEnemies)
print(archEnemies.count)


// Sets
// Similar to arrays but with two differences:
// 1. don´t remember the order you add things
// 2. don´t allow duplicates

var actors = Set<String>()
actors.insert("Denzel Washington")
actors.insert("Tom Cruise")
actors.insert("Nicolas Cage")
print(actors)
// no duplicates allowed > unique
// highly efficient to store large value of data > fast data lookup
print(actors.count)
print(actors.contains("Tom Cruise"))

// Enum (enumerations)
// range of particular options

enum Weekday {
    case monday
    case tuesday
    case wednesday
    case thursday
    case friday
}

var day = Weekday.monday
day = Weekday.tuesday
day = Weekday.friday

enum Month {
    case january, february, march
}
// shorter way to write all possible options

var month = Month.january
day = .friday
print(day)
