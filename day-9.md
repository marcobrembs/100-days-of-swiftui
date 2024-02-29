// Closures
// assign functionality directly to a constant or variable

func greetUser() {
    print("Hi, there!")
}
greetUser()
var greetCopy: () -> Void = greetUser
greetCopy()

let sayHello = { (name: String) -> String in
    "Hi \(name)"
}
sayHello("Marco")

let team = ["Gloria", "Susanne", "Piper", "Tiffany", "Tasha"]
let teamSorted = team.sorted()
print(teamSorted)


// function
func captainFirstSorted(name1: String, name2:String) -> Bool {
    if name1 == "Susanne" {
        return true
    } else if name2 == "Susanne" {
        return false
    }
    return name1 < name2
}

//let captainFirstTeam = team.sorted(by: captainFirstSorted)
//print(captainFirstTeam)


// closure
let captainFirstTeam = team.sorted(by: { (name1: String, name2: String) -> Bool in
    if name1 == "Susanne" {
        return true
    } else if name2 == "Susanne" {
        return false
    }
    return name1 < name2
})
print(captainFirstTeam)

// trailing closures & shorthand syntax
let captainFirstTeamTwo = team.sorted {
    if $0 == "Susanne" {
        return true
    } else if $1 == "Susanne" {
        return false
    }
    return $0 < $1
}
print(captainFirstTeamTwo)

let reverseTeam = team.sorted { $0 > $1 }
print(reverseTeam)

let tOnly = team.filter { $0.hasPrefix("T")}
print(tOnly)

let uppercaseTeam = team.map { $0.uppercased() }
print(uppercaseTeam)


// accept functions as parameters

func makeArray(size: Int, using generator: () -> Int) -> [Int] {
    // using generator: () -> Int - Function that accepts no parameters but returns Int every time that we call it
    var numbers = [Int]()
    // creates empty array and save as variable numbers
    
    for _ in 0..<size {
        let newNumber = generator()
        numbers.append(newNumber)
    }
    
    return numbers
}

func doImportantWork(first: () -> Void, second: () -> Void, third: () -> Void) {
    print("About to start first work")
    first()
    print("About to start second work")
    second()
    print("About to start third work")
    third()
    print("Done!")
}

doImportantWork {
    print("This is the first work")
} second: {
    print("This is the second work")
} third: {
    print("This is the third work")
}


// Checkpoint 5
// Your input is this:
// let luckyNumbers = [7, 4, 38, 21, 16, 15, 12, 33, 31, 49]
// Your job is to:
// Filter out any numbers that are even
// Sort the array in ascending order
// Map them to strings in the format "7 is a lucky number"
// Print the resulting array, one item per line

let luckyNumbers = [7, 4, 38, 21, 16, 15, 12, 33, 31, 49]

let processNumbers = { (numbers: [Int]) -> () in
    let formattedStrings = numbers.filter { $0 % 2 != 0}
        .sorted()
        .map { "\($0) is a lucky number" }
    
    formattedStrings.forEach { print($0) }
}

processNumbers(luckyNumbers)
