# Part 1, common programming interview questions in Swift.

Some solutions to common programming interview questions, list compiled by [/u/dandr01d](https://www.reddit.com/user/dandr01d) on reddit.

I take no resonsibility, if you implement one of these on your interview and don't get the posistion because I had a terrible implementation. These are my personal notes I feel might help somebody.

# Whats covered?

  - Check if sequence contains, sequence index
  - Linear search, bubble sort, binary search
  - Find most frequent integer in list
  - Find pairs in an integer array whose sum is equal to a given number
  - Iteratively and recursive Fibbonaci numbers
  - Find the only element in an array that only occurs once.
  - Find the common elements of 2 int arrays
  - Iteratively and recursive exponent function

### Sequence Contains

```swift
func sequenceContains(n: Int, list: Array<Int>) -> Bool {
    if list.contains(3){
        return true
    } else {
        return false
    }
}
```

### Sequence Index

```swift
func sequenceIndex(n: Int, list: Array<Int>) -> Bool {
    
    if let _ = list.index(where: { $0 == n }) {
        return true
        // print(true elementIndex) // 23 9
    } else {
        return false
    }
}
```

### Linear Search

```swift
func linearForLoop(n: Int, list: Array<Int>) -> Bool {
    var matches = Bool()
    for item in list {
        if n == item {
            matches = true
            break
        } else {
            matches = false
        }
    }
    return matches
}
```

### Bubblesort

```swift
func bubbleSort( list: Array<Int>) -> Array<Int> {
    
    var list = list
    var key, passCount, z: Int
    //track iterations
    for x in 0..<list.count {
        passCount = (list.count - 1) - x
        for y in 0 ..< passCount {
            key = list[y]
            //comparisons and value ranking
            if (key > list[y + 1]) {
                z = list[y + 1]
                list[y + 1] = key
                list[y] = z
            }
        }
    }
    return list
}
```

### Binary Search

```swift
func binarySearch(key: Int,  list: Array<Int>) -> (Bool, Int?, Int) {
    
    let sortedList = list.sorted()
    var min = 0
    var max = list.count - 1
    var stepCount = 0
    
    while min < max {
        stepCount += 1
        let mid = min + (max - min) / 2
        if sortedList[mid] == key {
            return (true, mid, stepCount)  // mid / index in the sorted array
        } else if (min > max) {
            return (false, nil, stepCount)
        } else {
            if (sortedList[mid] > key) {
                max = mid  - 1
            } else {
                min = mid + 1
            }
        }
    }
    return (false, nil, stepCount)
}
```

### Most frequent integer in an array

Swifty way
```swift
func countArray(inArray: Array<Int>) -> [Int: Int] {
    var counted:[Int:Int] = [:]
    for item in inArray {
        counted[item] = (counted[item] ?? 0) + 1
    }
    return counted
}
```
Not really that Swifty, but a fall back
```swift
func countMethodTwo(inArray: Array<Any>) -> [Int: Int] {
var counted:[Int:Int] = [:]

for element in arrList {
    if counted[element] != nil {
        counted[element]! += 1
    } else {
        counted[element] = 1
    }
}
    return counted
}
```
### Find pairs in an integer array whose sum is equal to a given number
```swift
var arrListTwo = [0,2,3,4,4,3,3,2,0,6,5,3432,6,4,2,23,4,5,3,2,1,6,89,4,1,2,3,4,5,8]
//not necessary but for "efficiancy"
let arrReduced = Array(Set(arrListTwo))


func pairFinder(inArray: [Int], sumToFind: Int) {

for element in arrListTwo {
    let myPairIs = sumToFind - element
    if arrListTwo.contains(myPairIs) {
        print("\(element) has a pair \(myPairIs) to sum \(sumToFind)")
         }
    }
}
```
### Fibbonaci numbers
Iteratively

```swift
func fibonacciIterative(n: Int) {
    var (a, b) = (0, 1)
    for _ in 0 ..< n {
        (a, b) = (b, a + b)
        print(a)
    }
}
```
Recursively
```swift
func fibonacciRecursive(n: Int) -> Int {
    if n == 0 {
        return 0
    } else if n == 1{
        return 1
    }
    return fibonacciRecursive(n: n - 1) + fibonacciRecursive(n: n - 2)
}
```

### Find the only element in an array that only occurs once.
```swift
func singular(inArray: [Int]) {
    var value = 0
    for (index, _) in inArray.enumerated() {
        value = value ^ inArray[index]
    }
    print(value)
}
```
Find multiple single elements.
```swift
func singularTwo(inArray: [Int]) -> [Int] {
    var singlesArr = [Int]()
    for item in inArray {
        if singlesArr.contains(item) {
          let idx = singlesArr.index(of: item)
            singlesArr.remove(at: idx!)
        } else {
            singlesArr.append(item)
        }
    }
    return singlesArr
}
```

### Find the common elements of 2 intger arrays

Modified version of above
```swift
func singularTwo(inArrayOne: [Int], inArrayTwo: [Int]) -> [Int] {
  var commonArr = [Int]()
    for item in inArrayOne {
        if inArrayTwo.contains(item) && commonArr.index(of: item) == nil{
            commonArr.append(item)
        }
    }
    return commonArr
}
```

### Exponent function
PLEASE PLEASE PLEASE, just use pow(), but in the spirit of things:

Irritative
```swift
func exponentialIrritative(n: Double, x: Double) -> Double
{
    var x = x
    var sum = 1.0 // initialize sum of series
    
    while (x>0){
        sum *= n
        x = x - 1
    }
    return sum
}
```
Recursive
```swift
func recursiveExponential(n: Double, x: Double) -> Double
{
    //Edge cases
    if x == 1 {
        return n
    }
    if x == 2{
        return n * n
    }
    if (x.truncatingRemainder(dividingBy: 2) == 1){
        return n * recursiveExponential(n: n, x: x - 1)
    }
}
```

# Part 2 to Follow
