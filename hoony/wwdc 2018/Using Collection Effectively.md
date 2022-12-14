

๐ WWDC18 | Category : SwiftUI & UI Frameworks

Using Collection Effectively
---
๐ https://developer.apple.com/videos/play/wwdc2018/229/

Collection์์ lazy ํค์๋๋ฅผ ๋ค์ ๋ณด๊ฒ ๋๊ธฐ๋ ํ๊ณ , ์ฒ์๋ณด๋ ๊ฒ๋ค์ด ๋ง์๋ค ๋๋ฒ์งธ ์์์ธ๋ฐ ๋๋ฒ ๋ค ์ฒ์๋ณผ๋ ํ๋๋ ์ดํด ์๋๋ค๊ฐ ์ฝ๋๋ ์ณ๋ณด๊ณ  ๊ตฌ๊ธ๋ง ํ๋ค๋ณด๋ฉด ์กฐ๊ธ์ฉ์ ์ดํด๋๋ค!

# Collection Types
![collection](https://user-images.githubusercontent.com/111875357/190842817-52c68c1f-bd6b-42dd-8df1-56c70a272803.png)

Swift๋ ์ฌ๋ฌ ๊ฐ๋ค์ ์ ์ฅํ๊ธฐ ์ํด Array, Set, Dictionary๋ผ๋ collection type(์ปฌ๋ ์ ํ์)์ ์ ๊ณตํ๋ค.

Array(๋ฐฐ์ด)์ ์์๋๋ก ๊ฐ์ ๋ชจ์ ๊ฒ์ด๊ณ  Set(์งํฉ)์ ์์๊ฐ ์๋ ๊ฐ๋ค์ ๋ชจ์ ๊ฒ์ด๋ค.

Dictionary๋ Key-value ์์ ์์ ์์ด ๋ชจ์ ๊ฒ์ด๋ค.

### Swift์ Array, Set, Dictionary์ ์ ์ฅ๋๋ ๊ฐ์ ํญ์ ๋ชํํ ํ์์ ๊ฐ์ง๊ณ  ์์ด์ผ ํ๋ค!



![Collection Protocol Hierarchy](https://user-images.githubusercontent.com/111875357/190842557-e1bb6c0e-dc36-4321-8c9e-3110701a0548.png)


## Collection
```swift
protocol Collection : Sequence {
    associatedtype Element
    associatedtype Index : Comparable
    
    subscript(position: Index) -> Element { get }
    
    var startIndex: Index { get }
    var endIndex: Index { get }
    
    func index(after i: Index) -> Index
}
```

## Collection2
```swift
extension Collection {
  func everyOther(_ body: (Element) -> Void) {
    let start = self.startIndex
    let end = self.endIndex
      
    var iter = start
    while iter != end 
    body(self[iter])
          
        let next = index(after: iter
        if next == end { break }
        iter = index(after: next)
    }
  }
}

(1...10).everyOther { print($0) }
```
### Indices
- Each collection defines its own idex
- Must be Comparable
- Think of these as opaque


## Find the Second Element of a Collection
```swift
extension Collection {
    var second: Element? {
    // Is the collection empty?
    guard self.startIndex != self.endIndex else { return nil }
    // Get the second index
    let index = self.index(after: self.startIndex)
    // Is that index valid?
    guard index != self.endIndex else { return nil }
    // Return the second element
    return self[index]
```


## Forming a Slice
#### ๋ชจ๋  ์ฌ๋ผ์ด์ค์๋ ๊ณ ์ ํ ์์ ๋ฐ ๋ ์ธ๋ฑ์ค๊ฐ ์์ผ๋ฉฐ ์ฌ๋ผ์ด์ค๋ ์๋ ์ปฌ๋ ์๊ณผ ๋ณ๋๋ก ์กด์ฌํ๋ค.
```swift
// Slice Share Indices with Original Collection

let array = [1, 2, 3, 4, 5]

let subarray = array.dropFrist() // ์ฒซ๋ฒ์งธ๊บผ ์์ฐ
let secondIndex = array.index(after: array.startIndex) // ์ฒซ๋ฒ๊บผ ์ดํ

print(second Index == subarray.startIndex) // true
```

```swift
var second: Element? {
   return self.dropFirst().frist
}
```
๊ฐ๊ฒฐํ๊ฒ ์ฒ๋ฆฌ ๊ฐ๋ฅํ๋ค.

```swift
// Slicing Keeps Underlying Storage

extension Array {
    var firstHalf: ArraySlice<Element> {
        return self.dropLast(self.count /2)
    }
}

var array = [1, 2, 3, 4, 5, 6, 7, 8]
var firstHalf = array.firstHalf // [1, 2, 3, 4]
array = [] // ๋ฐฐ์ด์ ๋น์ด์๊ฒ ํด๋ ์ด๋ป๊ฒ๋  ์ถ๋ ฅ์ด ๋ฉ๋๋ค!
print(firstHalf.first!) // 1

let copy = Array(firstHalf) // [1, 2, 3, 4]
firstHalf = [] // ๋ฐฐ์ด์ ๋น์ด์๊ฒ ํด๋ ์ด๋ป๊ฒ๋  ์ถ๋ ฅ์ด ๋ฉ๋๋ค! 2
print(copy.first!) // 1
```

#### Slices

- Produce Collection- like peers of original collection

- Array -> ArraySlice

- String -> Substring

- Set -> Slice

- Data -> Data

- Range -> Range

## Lazy Collection
```swift
func increment(x: Int) -> Int {
    print("Computing next value of \(x)")
    return x+1
}

let array = Array(0..<10)
let incArray = array.map(increment)
print("Result:")
print(incArray[0], incArray[4])
    
// ์ถ๋ ฅ์
//Computing next value of 0
//Computing next value of 1
//Computing next value of 2
//Computing next value of 3
//Computing next value of 4
//Computing next value of 5
//Computing next value of 6
//Computing next value of 7
//Computing next value of 8
//Computing next value of 9
//Result:
//1 5
```
increment๊ฐ ์ง๊ธ์ 10์ด์ง๋ง 1000 ๊ทธ ์ด์ 10000 ์ด๋ ๊ฒ ์ปค์ง๋ฉด ํจ์ ๋ด์์ ์๊ฐ์ด ์ค๋ ๊ฑธ๋ฆฌ๊ธฐ์ ๊ต์ฅํ ์ํด์ด๋ค.

์ด๋ฅผ ํด๊ฒฐํ๊ธฐ ์ํค ์ฌ์ฉํ๋ ๊ฒ์ด lazy

Swift ํ์ค ๋ผ์ด๋ธ๋ฌ๋ฆฌ์์ SequenceType ๋ฐ CollectionType ํ๋กํ ์ฝ์๋ lazy๋ผ๋ ์ฐ์ฐ ํ๋กํผํฐ๊ฐ ์์ผ๋ฉฐ,

์ด ํด๋์ค๋ ํน์ LazySequence ๋๋ LazyCollection์ ๋ฐํํ๋ค. ์ด๋ฌํ ํ์์ map, flatMap, filter ๋ฑ๊ณผ ๊ฐ์

๊ณ ์ฐจ ํจ์๋ฅผ lazy ๋ฐฉ์์ผ๋ก ์ ์ฉํ๋ ๋ฐ์๋ง ์ฌ์ฉํ๋ค.

```swift
// lazy ํค์๋๋ฅผ ๋ฃ๋๊ฒฝ์ฐ
func increment(x: Int) -> Int {
    print("Computing next value of \(x)")
    return x+1
}

let array = Array(0..<10)
let incArray = array.lazy.map(increment)
print("Result:")
print(incArray[0], incArray[4])

//์ถ๋ ฅ์
//Result:
//Computing next value of 0
//Computing next value of 4
//1 5
```
0~9 ๊น์ง array์ ๋ชจ๋  ์์์ ์ ๊ทผํ๋ ๊ฒ์ด ์๋๋ผ 0๋ฒ์งธ์ 4๋ฒ์งธ ์ธ๋ฑ์ค์๋ง ์ ๊ทผํ๊ณ  ์๋ค. ๊ทธ๋ฌ๋ฏ๋ก

ํผํฌ๋จผ์ค๋ฅผ ํฅ์ ์ํฌ์ ์๋ค!

์ด๊ฒ์ด Sequence์์ lazy๋ฅผ ์ฌ์ฉํ๋ ๋ฐฉ๋ฒ์ด๋ค.

### Advice: When to Be Lazy?
- Chained computation
- ์ ์ฒด ๊ฒฐ๊ณผ๊ฐ ํ์ํ์ง ์์๋
- No side effects
- Avoid API boundaries

### collection์์ crash ๋๋ ์ด์ 
- collection์ mutating ์ํค๊ณ  ์์ง ์์์ง ํ์ธํ๊ธฐ
- ์ฌ๋ฌ ์ฐ๋ ๋์์ ์ปฌ๋ ์์ ์ ๊ทผํ๊ณ  ์๋์ง ํ์ธํ๊ธฐ

### Advice: Indices and Slice
- Use caution when keeping indcies/slices
- Mutation invalidates
- ์ฌ๋ผ์ด์ค๋ ์ปฌ๋ ์์ด ๋ณ๊ฒฝ๋ ํ์๋ ์ปฌ๋ ์์ ๊ธฐ๋ณธ ์๋ ์ํ๋ฅผ ์ ์งํ๋ฏ๋ก ๊ธฐ๋ณธ ์ปฌ๋ ์์ด ๋ณ๊ฒฝ ๊ฐ๋ฅํ ๊ฒฝ์ฐ ์ธ๋ฑ์ค ๋๋ ์ฌ๋ผ์ด์ค๋ฅผ ์ ์งํ๋ ๊ฒ์ ๋ํด
- ๋ค์ ํ ๋ฒ ์๊ฐํ๊ธฐ
- Calculate only as needed

## Are your collections reachable from multiple threads?
### Multithreaded Mutable Collections
- Our collections optimized for single-threaded access
- This is a Good Thing
- Underfined behavior without mutal exclusion

```swift
/// Example of Thread-Unsafe Practices

var sleepingBears = [String]()
let queue = DispatchQueue.global()

queue.async { sleepingBears.append("Grandpa") }
queue.async { sleepingBears.append("Cub") }
```
Swift ์ก์ธ์ค ๊ฒฝ์์ด ์์์ ์ ์ ์์ ( TSPN )

์ฌ๋ฌ ์ค๋ ๋์ ๋ํ ์ปฌ๋ ์ ์์์ ๋ํ ์กฐ์ธ์ผ๋ก๋ ๋ฐ์ดํฐ๋ฅผ ๊ฒฉ๋ฆฌํ์ฌ ๋จ์ผ ์ค๋ ๋์์๋ง ๋ณผ ์ ์๋๋ก ํ๊ณ 

๊ทธ๋ ๊ฒ ํ  ์ ์๋ ๊ฒฝ์ฐ ์ํธ ๋ฐฐ์ ์ ์ ์ ํ ํ์์ด ์๋์ง ํ์ธํ๊ธฐ

### Advice: Prefer Immutable Collections
- Easier to reason about data that can't change (ํผํ  ์ ์๋ค๋ฉด ๋ณ๊ฒฝ ๊ฐ๋ฅํ ์ํ๋ฅผ ์ฌ์ฉํ์ง ์๊ธฐ)
- Lss surface area for bugs
- Emulate mutation with slices and lazy
- The complier will help you

### Advice: Formoing New Collection
- Use capacity hints if possible
```swift
Array.reserveCapacity(_:)
Set(minimumCapacity:)
Dictionaray(minimumCapacity:)
```

### Bridging between Objective-C and Swift
- Converts between runtime types
- Bidirectional
- Bridging of collections
  - Is necessary
  - Can be cheap, but is never free

### Two Kinds of Bridging
- Eager when element types are bridged
- Otherwise lazy
  - Bridged on first use

### Identifying Bridging Problems
- Measure your performance with Instruments
- Especially inside loops at language boundaries
- Look for hotspots like:
  - _unconditionallyBridgeFromObjectiveC
  - bridgeEverything

```swift
let story = NSString(string: "์์ด ์์ด ์์ด")

let text = NSMutableAttributedString(string: story)

// ์ฒซ ๋ฒ์งธ  (Bridging overhead๊ฐ ํผ)
let range = text.string.range(of: "Brown")!
let nsrange = NSRange(range, in: text.string)

// ๋ ๋ฒ์งธ
let string = text.string // ์ฌ๊ธฐ์ ์ค๋ฒํค๋ ํ ๋ฒ ๋ฐ์
let range = text.string.range(of: "Brown")!
let nsrange = NSRange(range, in: text.string)

// ์ธ ๋ฒ์งธ
let string = text.string as NSString
let nsrange = string.range(of: "Brown")

text.addAttribute(.forgroundColor, value: NSColor.brown, range: nsrange)
```
์ฒ๋ฆฌ ์๋๋ฉด์์ ์ธ๋ฒ์งธ๊ฒ์ด ํจ์จ์ ์!

### Adivce: When to Use Foundation Collection
- You need reference semantics (์ฐธ์กฐ ์๋ฏธ ์ฒด๊ณ๊ฐ ์๋ ์ปฌ๋ ์์ด ํ์ํ  ๋ ๋ช์์ ์ผ๋ก ์ฌ์ฉ ๊ณ ๋ คํ๊ธฐ)
- You are working with known proxies
  - NSAttributedSring.string
  - Core Data /managed Objects
- You`ve measured and identified bridging costs

### Now It`s Your Turn
- Explore your existing collections
- Measure your code
- Audit your mutable state
- Gain mastery in Playgrounds
