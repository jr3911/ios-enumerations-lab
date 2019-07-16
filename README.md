# Enumerations lab

Fork and clone this repo. On your fork, answer and commit the follow questions. When you are finished, submit the link to your repo on Canvas.


## Question 1

a) Define an enumeration called `iOSDeviceType` with member values `iPhone`, `iPad`, `iWatch`. Create a variable called `myDevice` and assign it one member value.

```swift
enum iOSDeviceType {
    case iPhone
    case iPad
    case iWatch
}

var myDevice = iOSDeviceType.iPad

```

b) Adjust your code above so that `iPhone` and `iPad` have associated values of type String which represents the model number, eg: `iPhone("6 Plus")`. Use a switch case and let syntax to print out the model number of each device.

```swift
enum iOSDeviceType {
    case iPhone(String)
    case iPad(String)
    case iWatch(String)
}

var myDevice = iOSDeviceType.iPhone("6 Plus")


switch myDevice {
case let .iPhone(modelNumber):
    print("iPhone model number: \(modelNumber)")
case let .iPad(modelNumber):
    print("iPad model number: \(modelNumber)")
case let .iWatch(modelNumber):
    print("iWatch model number: \(modelNumber)")
}

```


## Question 2

a) Write an enum called `Shape` and give it cases for `triangle`, `rectangle`, `square`, `pentagon`, and `hexagon`.

```swift
enum Shape {
    case triangle
    case rectangle
    case square
    case pentagon
    case hexagon
}

```

b) Write a method inside `Shape` that returns how many sides the shape has. Create a variable called `myFavoritePolygon` and assign it to one of the shapes above, then print out how many sides it has.

```swift
enum Shape {
    case triangle
    case rectangle
    case square
    case pentagon
    case hexagon

    func numSides() -> Int {
        switch myFavoritePolygon {
        case .triangle:
            return 3
        case .rectangle:
            return 4
        case .square:
            return 4
        case .pentagon:
            return 5
        case .hexagon:
            return 6
        }
    }
}

let myFavoritePolygon = Shape.pentagon

print("My favorite shape is a \(myFavoritePolygon) and it has \(myFavoritePolygon.numSides()) sides")
```

c) Re-write `Shape` so that each case has an associated value of type Int that will represent the length of the sides (assume the shapes are regular polygons so all the sides are the same length) and write a method inside that returns the perimeter of the shape.

```swift
enum Shape {
    case triangle(Int)
    case rectangle(Int)
    case square(Int)
    case pentagon(Int)
    case hexagon(Int)

    func numSides() -> Int {
        switch myFavoritePolygon {
        case .triangle:
            return 3
        case .rectangle:
            return 4
        case .square:
            return 4
        case .pentagon:
            return 5
        case .hexagon:
            return 6
        }
    }

    func perimeter() -> Int {
        switch myFavoritePolygon {
        case .triangle(let length):
            return 3 * length
        case .rectangle(let length):
            return 4 * length
        case .square(let length):
            return 4 * length
        case .pentagon(let length):
            return 5 * length
        case .hexagon(let length):
            return 6 * length
        }
    }
}

let myFavoritePolygon = Shape.triangle(5)

print("My favorite shape is a \(myFavoritePolygon) and it has a perimeter of \(myFavoritePolygon.perimeter()) units")
```


## Question 3

Write an enum called `OperatingSystem` and give it cases for `windows`, `mac`, and `linux`. Create an array of 10 `OperatingSystem` objects where each one is set to a random operating system. Then, iterate through the array and print out a message depending on the operating system.

```swift
enum OperatingSystem {
    case windows
    case mac
    case linux
}

var arrOS = [OperatingSystem.windows, OperatingSystem.mac, OperatingSystem.linux, OperatingSystem.mac, OperatingSystem.windows, OperatingSystem.windows, OperatingSystem.linux]

for element in arrOS {
    switch element {
    case .windows:
        print("This is windows")
    case .mac:
        print("Apple sucks")
    case .linux:
        print("Never again")
    }
}
```


## Question 4

You are working on a game in which your character is exploring a grid-like map. You get the original location of the character and the steps he will take.

- A step .up will increase the y coordinate by 1.
- A step .down will decrease the y coordinate by 1.
- A step .right will increase the x coordinate by 1.
- A step .left will decrease the x coordinate by 1.
- Print the final location of the character after all the steps have been taken.

```swift
enum Direction {
    case up
    case down
    case left
    case right
}

var location = (x: 0, y: 0)
var steps: [Direction] = [.up, .up, .left, .down, .left]

for step in steps {
    switch step {
    case .up:
        location.y += 1
    case .down:
        location.y -= 1
    case .right:
        location.x += 1
    case .left:
        location.x -= 1
    }
}

print(location)

```


## Question 5

a) Define an enumeration named `HandShape` with three members: `.rock`, `.paper`, `.scissors`.

b) Define an enumeration named `MatchResult` with three members: `.win`, `.draw`, `.lose`.

c) Write a function called `match` that takes two `HandShapes` and returns a `MatchResult`. It should return the outcome for the first player (the one with the first hand shape).

Hint: Rock beats scissors, paper beats rock, scissor beats paper

```swift
enum HandShape {
    case rock
    case paper
    case scissors
}

enum MatchResult {
    case win
    case draw
    case lose
}

func match(player1 player1: HandShape, player2 player2: HandShape) -> MatchResult {
    if player1 == player2 {
        return .draw
    } else if player1 == .rock && player2 == .scissors {
        return .win
    } else if player1 == .paper && player2 == .rock {
        return .win
    } else if player1 == .scissors && player2 == .paper {
        return .win
    } else {
        return .lose
    }
}
```


## Question 6

a) You are given a `CoinType` enumeration which describes different coin values. Print the total value of the coins in the array `moneyArray` which contains tuples of type (`quantity`, `CoinType`).

```swift
enum CoinType: Int {
    case penny = 1
    case nickle = 5
    case dime = 10
    case quarter = 25
}

var moneyArray:[(Int,CoinType)] = [(10,.penny),
                                   (15,.nickle),
                                   (3,.quarter),
                                   (20,.penny),
                                   (3,.dime),
                                   (7,.quarter)]

var totalValue = 0

for tuple in moneyArray {
    totalValue += tuple.0 * tuple.1.rawValue
}

let formattedTotalValue = Double(totalValue) / 10.0

print(String(format: "$%.2f", formattedTotalValue))

```

b) Write a method in the `CoinType` enum that returns an Int representing how many coins of that type you need to have a dollar. Then, create an instance of `CoinType` set to `.nickle` and use your method to print out how many nickels you need to have to make a dollar.

```swift
enum CoinType: Int {
    case penny = 1
    case nickle = 5
    case dime = 10
    case quarter = 25

    func quantityNeededToMakeOneDollar() -> Int {
        switch coins {
        case .penny:
            return 100
        case .nickle:
            return 20
        case .dime:
            return 10
        case .quarter:
            return 4
        }
    }
}

let coins = CoinType.nickle

print("You need \(coins.quantityNeededToMakeOneDollar()) \(coins)s to make $1")
```


## Question 7

a) Write an enum called `DayOfWeek` to represent the days of the week with a raw value of type String.

```swift
enum DayOfWeek: String {
    case sunday = "Sunday"
    case monday = "Monday"
    case tuesday = "Tuesday"
    case wednesday = "Wednesday"
    case thursday = "Thursday"
    case friday = "Friday"
    case saturday = "Saturday"
}

```

b) Given the array `poorlyFormattedDays`, write code that will produce an array of enums that match the days.

```swift
let poorlyFormattedDays = ["MONDAY", "wednesday", "Sunday", "monday", "Tuesday", "WEDNESDAY", "thursday", "SATURDAY", "tuesday", "FRIDAy", "Wednesday", "Monday", "Friday", "sunday"]

enum DayOfWeek: String {
    case sunday = "sunday"
    case monday = "monday"
    case tuesday = "tuesday"
    case wednesday = "wednesday"
    case thursday = "thursday"
    case friday = "friday"
    case saturday = "saturday"
}

var properlyFormattedDays = [DayOfWeek]()

for element in poorlyFormattedDays {
    if let day = DayOfWeek(rawValue: element.lowercased()) {
        properlyFormattedDays.append(day)
    }
}

print(properlyFormattedDays)

```


c) Write a method in `DayOfWeek` called `isWeekend` that determines whether a day is part of the weekend or not and write code to calculate how many week days appear in `poorlyFormattedDays`.

```swift
//reusing the code from part b above, the code below this comment are the additions

func isWeekend() -> Bool {
    switch self {
    case .sunday:
        return true
    case .saturday:
        return true
    default:
        return false
    }
}

var numWeekDays = 0

for day in properlyFormattedDays where day.isWeekend() ==  false {
    numWeekDays += 1
}

print("There are \(numWeekDays) week days in the array.")

```

## Question 8

a) Create an enum called `MetroLine` with cases for the colors of the metro train lines. Create an instance of `MetroLine`.

```swift
enum MetroLine {
    case yellow
    case orange
    case red
    case green
    case blue
    case brown
}

let train = MetroLine.red
```

b) Modify your enum so that each case has an associated value of either Character or Int that will represent the train on that line. Create a new instance of `MetroLine` and give it an appropriate train letter or number.

```swift
enum MetroLine {
    case yellow(Character)
    case orange(Int)
    case red(Int)
    case blue(Character)
}

let train = MetroLine.red(7)
```

c) Write code that prints the train letter or number of your instance of `MetroLine`.

```swift
switch train {
case .yellow(let line):
    print(line)
case .orange(let line):
    print(line)
case .red(let line):
    print(line)
case .blue(let line):
    print(line)
}

```


## Question 9

a) Think of your own example of something that can be modeled as an enum and write it. Remember that enums allow you to create instances of a defined list of cases.

b) Add a method to your enum.... try to have the method make sense.

```swift
enum Animal {
    case dog
    case cat
    case birb

    func noise() -> String {
        switch self {
        case .dog:
            return "woof woof bork"
        case .cat:
            return "meow mrreeooow hiss"
        case .birb:
            return "tweet, like, and follow for more content"
        }
    }
}
```
