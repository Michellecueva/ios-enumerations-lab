# Enumerations lab

Fork and clone this repo. On your fork, answer and commit the follow questions. When you are finished, submit the link to your repo on Canvas.


## Question 1

a) Define an enumeration called `iOSDeviceType` with member values `iPhone`, `iPad`, `iWatch`. Create a variable called `myDevice` and assign it one member value.

b) Adjust your code above so that `iPhone` and `iPad` have associated values of type String which represents the model number, eg: `iPhone("6 Plus")`. Use a switch case and let syntax to print out the model number of each device.

```swift 

enum iOSDeviceType {

    case iphone (String)
    case iPad (String)
    case iWatch

    func printAllDevices() {
        switch self {
            case .iphone(let model):
                print("iphone model: \(model)")
            case .iPad(let model):
                print(("iphone model: \(model)"))
            case .iWatch:
                print("iWatch")
        }

    }

}

let myDevice = iOSDeviceType.iphone("6 Plus")

myDevice.printAllDevices()

let anotherDevice = iOSDeviceType.iPad("5th Generation")
anotherDevice.printAllDevices()

```


## Question 2

a) Write an enum called `Shape` and give it cases for `triangle`, `rectangle`, `square`, `pentagon`, and `hexagon`.

b) Write a method inside `Shape` that returns how many sides the shape has. Create a variable called `myFavoritePolygon` and assign it to one of the shapes above, then print out how many sides it has.

c) Re-write `Shape` so that each case has an associated value of type Int that will represent the length of the sides (assume the shapes are regular polygons so all the sides are the same length) and write a method inside that returns the perimeter of the shape.

```swift

enum Shape: String {
    case triangle
    case rectangle
    case square
    case pentagon
    case hexagon


    func howManySides() -> Int {
        switch self {
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

var myFavoritePolygon = Shape.square
print(myFavoritePolygon.howManySides())


enum Shape {
    case triangle(Int)
    case rectangle(Int)
    case square(Int)
    case pentagon(Int)
    case hexagon(Int)


    func perimeter() -> Int {
        switch self {
        case .triangle(let length):
            return length * 3
        case .rectangle(let length):
            return length * 4
        case .square(let length):
            return length * 4
        case .pentagon(let length):
            return length * 5
        case .hexagon(let length):
            return length * 6
        }
    }
}

var myFavoritePolygon = Shape.square(5)
print(myFavoritePolygon.perimeter())

```


## Question 3

Write an enum called `OperatingSystem` and give it cases for `windows`, `mac`, and `linux`. Create an array of 10 `OperatingSystem` objects where each one is set to a random operating system. Then, iterate through the array and print out a message depending on the operating system.

```swift
enum OperatingSystem: CaseIterable {
case windows
case mac
case linux

    func message() {
        switch self {
        case .windows:
            print("This is Windows")
        case OperatingSystem.mac:
            print("This is Mac")
        case OperatingSystem.linux:
            print("This is Linux")
        }
    }
}

var arr = [OperatingSystem]()

for _ in 0..<10 {
    arr.append(OperatingSystem.allCases.randomElement()!)
}

for i in arr {
    i.message()
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

// your code here

for direction in steps {
    switch direction {
    case .up:
        location.y += 1
    case .down:
        location.y -= 1
    case .left:
        location.x -= 1
    case .right:
        location.x += 1
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

enum Handshape {
    case rock
    case paper
    case scissors
}

enum MatchResult {
    case win
    case draw
    case lose
}

func match(firstShape:Handshape, secondShape: Handshape) -> MatchResult {
    switch firstShape {
    case .rock:
        switch secondShape {
        case .rock: return .draw
        case .paper: return .lose
        case .scissors: return .win
    }
    case .paper:
        switch secondShape {
        case .rock: return .win
        case .paper: return .draw
        case .scissors: return .lose
        }
        case .scissors:
            switch secondShape {
            case .rock: return .lose
            case .paper: return .win
            case .scissors: return .draw
        }
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

// your code here

enum CoinType: Int {
    case penny = 1
    case nickle = 5
    case dime = 10
    case quarter = 25

    func cost () -> Int {
        return self.rawValue
    }
}


var moneyArray:[(Int,CoinType)] = [(10,.penny),
(15,.nickle),
(3,.quarter),
(20,.penny),
(3,.dime),
(7,.quarter)]


var sum = 0.0

for i in moneyArray {
    sum += Double((i.1).cost())/100 * Double(i.0)
}

```

b) Write a method in the `CoinType` enum that returns an Int representing how many coins of that type you need to have a dollar. Then, create an instance of `CoinType` set to `.nickle` and use your method to print out how many nickels you need to have to make a dollar.

```swift 

enum CoinType: Int {
    case penny = 1
    case nickle = 5
    case dime = 10
    case quarter = 25

    func coinsNeeded () -> Int {
        return 100/self.rawValue
    }
}


var nickel = CoinType.nickle

print(nickel.coinsNeeded())

```


## Question 7

a) Write an enum called `DayOfWeek` to represent the days of the week with a raw value of type String.
``` swift

enum DayOfWeek: String {
    case Monday = "Monday"
    case Tuesday = "Tuesday"
    case Wednesday = "Wednesday"
    case Thursday = "Thursday"
    case Friday = "Friday"
    case Saturday = "Saturday"
    case Sunday = "Sunday"

}

```

b) Given the array `poorlyFormattedDays`, write code that will produce an array of enums that match the days.

`let poorlyFormattedDays = ["MONDAY", "wednesday", "Sunday", "monday", "Tuesday", "WEDNESDAY", "thursday", "SATURDAY", "tuesday", "FRIDAy", "Wednesday", "Monday", "Friday", "sunday"]`
```swift

enum DayOfWeek: String {
    case Monday = "Monday"
    case Tuesday = "Tuesday"
    case Wednesday = "Wednesday"
    case Thursday = "Thursday"
    case Friday = "Friday"
    case Saturday = "Saturday"
    case Sunday = "Sunday"

}
var arr = [DayOfWeek]()

for i in poorlyFormattedDays {
    switch i.lowercased() {
    case DayOfWeek.Monday.rawValue.lowercased():
        arr.append(DayOfWeek.Monday)
    case DayOfWeek.Tuesday.rawValue.lowercased():
        arr.append(DayOfWeek.Tuesday)
    case DayOfWeek.Wednesday.rawValue.lowercased():
        arr.append(DayOfWeek.Wednesday)
    case DayOfWeek.Thursday.rawValue.lowercased():
        arr.append(DayOfWeek.Thursday)
    case DayOfWeek.Friday.rawValue.lowercased():
        arr.append(DayOfWeek.Friday)
    case DayOfWeek.Saturday.rawValue.lowercased():
        arr.append(DayOfWeek.Saturday)
    case DayOfWeek.Sunday.rawValue.lowercased():
        arr.append(DayOfWeek.Sunday)
    default:
        arr
    }
}

print(arr)

```

c) Write a method in `DayOfWeek` called `isWeekend` that determines whether a day is part of the weekend or not and write code to calculate how many week days appear in `poorlyFormattedDays`.

```swift 

enum DayOfWeek: String {
    case Monday = "Monday"
    case Tuesday = "Tuesday"
    case Wednesday = "Wednesday"
    case Thursday = "Thursday"
    case Friday = "Friday"
    case Saturday = "Saturday"
    case Sunday = "Sunday"

    func isWeekend() -> Bool {
        return self.rawValue == "Saturday" || self.rawValue == "Sunday"
    }

}



let poorlyFormattedDays = ["MONDAY", "wednesday", "Sunday", "monday", "Tuesday", "WEDNESDAY", "thursday", "SATURDAY", "tuesday", "FRIDAy", "Wednesday", "Monday", "Friday", "sunday"]

var arr = [DayOfWeek]()

for i in poorlyFormattedDays {
    switch i.lowercased() {
    case DayOfWeek.Monday.rawValue.lowercased():
        arr.append(DayOfWeek.Monday)
    case DayOfWeek.Tuesday.rawValue.lowercased():
        arr.append(DayOfWeek.Tuesday)
    case DayOfWeek.Wednesday.rawValue.lowercased():
        arr.append(DayOfWeek.Wednesday)
    case DayOfWeek.Thursday.rawValue.lowercased():
        arr.append(DayOfWeek.Thursday)
    case DayOfWeek.Friday.rawValue.lowercased():
        arr.append(DayOfWeek.Friday)
    case DayOfWeek.Saturday.rawValue.lowercased():
        arr.append(DayOfWeek.Saturday)
    case DayOfWeek.Sunday.rawValue.lowercased():
        arr.append(DayOfWeek.Sunday)
    default:
    arr
    }
}

print(arr.filter{!$0.isWeekend()}.count)

```


## Question 8

a) Create an enum called `MetroLine` with cases for the colors of the metro train lines. Create an instance of `MetroLine`.

b) Modify your enum so that each case has an associated value of either Character or Int that will represent the train on that line. Create a new instance of `MetroLine` and give it an appropriate train letter or number.

c) Write code that prints the train letter or number of your instance of `MetroLine`.

```swift

enum MetroLine {
    case purple(Int)
    case green(Int)
    case red(Int)
    case brown(Character)
    case orange(Character)

    func printTrain() {
        switch self {
        case let .purple(num):
            print(num)
        case let .green(num):
            print(num)
        case let .red(num):
            print(num)
        case let .brown(letter):
            print(letter)
        case let .orange(letter):
            print(letter)
        }
    }
}

var fTrain = MetroLine.orange("f")

var purpleTrain = MetroLine.purple(7)



```




## Question 9

a) Think of your own example of something that can be modeled as an enum and write it. Remember that enums allow you to create instances of a defined list of cases.

b) Add a method to your enum.... try to have the method make sense.
```swift
enum chores : String {
    case clean = "On Friday"
    case cook = "Everyday"
    case wash_Dog = "Once a month"
    case dishes = "Every night"

    func whatday () {
        print(self.rawValue)
    }

}

var whenToClean = chores.clean

whenToClean.whatday()
```
