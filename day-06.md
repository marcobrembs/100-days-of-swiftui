// for loop

let platforms = ["iOS", "macOS", "tvOS", "watchOS"]

for os in platforms {
    print("Swift works great on \(os).")
}
// os = loop variable
// print... = loop body

for i in 1...12 {
    print("The \(i) times table")
    
    for j in 1...12 {
        print("   \(j) x \(i) is \(j * i)")
    }
    
    print()
}

for i in 1...5 {
    print("Counting from 1 through 5: \(i)")
}

for i in 1..<5 {
    print("Counting from 1 up to 5: \(i)")
}

var lyric = "Haters gonna"

for _ in 1...5 {
    lyric += " hate"
}

print(lyric)


// while loop

var countdown = 10

while countdown > 0 {
    print("\(countdown)...")
    countdown -= 1
}

print("Blast off!")

let id = Int.random(in: 1...1000)
let amount = Double.random(in: 0...1)

var roll = 0

while roll != 20 {
    roll = Int.random(in: 1...20)
    print("I rolled a \(roll)")
}
print("Critical hit!")


// skip loop items

let filenames = ["me.jpg", "work.txt", "sophie.jpg"]

for filename in filenames {
    if filename.hasSuffix(".jpg") == false {
        continue
        // skip this iteration
    }
    print("Found picture \(filename)")
}

let number1 = 4
let number2 = 14
var multiples = [Int]()
for i in 1...100_000 {
    if i.isMultiple(of: number1) && i.isMultiple(of: number2) {
        multiples.append(i)
        
        if multiples.count == 10 {
            break
            // skips the remaining iterations
        }
    }
}

print(multiples)

// Checkpoint 3

let number3 = 3
let number5 = 5

for z in 1...100 {
    if z.isMultiple(of: number3) && z.isMultiple(of: number5) {
        print("\(z): FizzBuzz")
        // if multiple of 3 and 5 -> print "FizzBuzz"
    }
    else if z.isMultiple(of: number3) {
        print("\(z): Fizz")
        // if multiple of 3 -> print "Fizz"
    } else if z.isMultiple(of: number5) {
        print("\(z): Buzz")
        // if multiple of 5 -> print "Buzz"
    } else {
        print("\(z): \(z)")
        // otherwise -> print just the number
    }
}
