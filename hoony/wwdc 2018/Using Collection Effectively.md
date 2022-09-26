

🍎 WWDC18 | Category : SwiftUI & UI Frameworks

Using Collection Effectively
---
🔗 https://developer.apple.com/videos/play/wwdc2018/229/

Collection에서 lazy 키워드를 다시 보게 되기도 했고, 처음보는 것들이 많았다 두번째 영상인데 두번 다 처음볼땐 하나도 이해 안되다가 코드도 쳐보고 구글링 하다보면 조금씩은 이해된다!

# Collection Types
![collection](https://user-images.githubusercontent.com/111875357/190842817-52c68c1f-bd6b-42dd-8df1-56c70a272803.png)

Swift는 여러 값들을 저장하기 위해 Array, Set, Dictionary라는 collection type(컬렉션 타입)을 제공한다.

Array(배열)은 순서대로 값을 모은 것이고 Set(집합)은 순서가 없는 값들을 모은 것이다.

Dictionary는 Key-value 쌍을 순서 없이 모은 것이다.

### Swift의 Array, Set, Dictionary에 저장되는 값은 항상 명확한 타입을 가지고 있어야 한다!



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
#### 모든 슬라이스에는 고유한 시작 및 끝 인덱스가 있으며 슬라이스는 원래 컬렉션과 별도로 존재한다.
```swift
// Slice Share Indices with Original Collection

let array = [1, 2, 3, 4, 5]

let subarray = array.dropFrist() // 첫번째꺼 없앰
let secondIndex = array.index(after: array.startIndex) // 첫번꺼 이후

print(second Index == subarray.startIndex) // true
```

```swift
var second: Element? {
   return self.dropFirst().frist
}
```
간결하게 처리 가능하다.

```swift
// Slicing Keeps Underlying Storage

extension Array {
    var firstHalf: ArraySlice<Element> {
        return self.dropLast(self.count /2)
    }
}

var array = [1, 2, 3, 4, 5, 6, 7, 8]
var firstHalf = array.firstHalf // [1, 2, 3, 4]
array = [] // 배열을 비어있게 해도 어떻게든 출력이 됩니다!
print(firstHalf.first!) // 1

let copy = Array(firstHalf) // [1, 2, 3, 4]
firstHalf = [] // 배열을 비어있게 해도 어떻게든 출력이 됩니다! 2
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
    
// 출력시
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
increment가 지금은 10이지만 1000 그 이상 10000 이렇게 커지면 함수 내에서 시간이 오래 걸리기에 굉장히 손해이다.

이를 해결하기 위헤 사용하는 것이 lazy

Swift 표준 라이브러리에서 SequenceType 및 CollectionType 프로토콜에는 lazy라는 연산 프로퍼티가 있으며,

이 클래스는 특수 LazySequence 또는 LazyCollection을 반환한다. 이러한 타입은 map, flatMap, filter 등과 같은

고차 함수를 lazy 방식으로 적용하는 데에만 사용한다.

```swift
// lazy 키워드를 넣는경우
func increment(x: Int) -> Int {
    print("Computing next value of \(x)")
    return x+1
}

let array = Array(0..<10)
let incArray = array.lazy.map(increment)
print("Result:")
print(incArray[0], incArray[4])

//출력시
//Result:
//Computing next value of 0
//Computing next value of 4
//1 5
```
0~9 까지 array에 모든 요소에 접근하는 것이 아니라 0번째와 4번째 인덱스에만 접근하고 있다. 그러므로

퍼포먼스를 향상 시킬수 있다!

이것이 Sequence에서 lazy를 사용하는 방법이다.

### Advice: When to Be Lazy?
- Chained computation
- 전체 결과가 필요하지 않을때
- No side effects
- Avoid API boundaries

### collection에서 crash 나는 이유
- collection을 mutating 시키고 있지 않은지 확인하기
- 여러 쓰레드에서 컬렉션을 접근하고 있는지 확인하기

### Advice: Indices and Slice
- Use caution when keeping indcies/slices
- Mutation invalidates
- 슬라이스는 컬렉션이 변경된 후에도 컬렉션의 기본 원래 상태를 유지하므로 기본 컬렉션이 변경 가능한 경우 인덱스 또는 슬라이스를 유지하는 것에 대해
- 다시 한 번 생각하기
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
Swift 액세스 경쟁이 있음을 알 수 있음 ( TSPN )

여러 스레드에 대한 컬렉션 작업에 대한 조언으로는 데이터를 격리하여 단일 스레드에서만 볼 수 있도록 하고

그렇게 할 수 없는 경우 상호 배제에 적절한 형식이 있는지 확인하기

### Advice: Prefer Immutable Collections
- Easier to reason about data that can't change (피할 수 있다면 변경 가능한 상태를 사용하지 않기)
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
let story = NSString(string: "영어 영어 영어")

let text = NSMutableAttributedString(string: story)

// 첫 번째  (Bridging overhead가 큼)
let range = text.string.range(of: "Brown")!
let nsrange = NSRange(range, in: text.string)

// 두 번째
let string = text.string // 여기서 오버헤드 한 번 발생
let range = text.string.range(of: "Brown")!
let nsrange = NSRange(range, in: text.string)

// 세 번째
let string = text.string as NSString
let nsrange = string.range(of: "Brown")

text.addAttribute(.forgroundColor, value: NSColor.brown, range: nsrange)
```
처리 속도면에서 세번째것이 효율적임!

### Adivce: When to Use Foundation Collection
- You need reference semantics (참조 의미 체계가 있는 컬렉션이 필요할 때 명시적으로 사용 고려하기)
- You are working with known proxies
  - NSAttributedSring.string
  - Core Data /managed Objects
- You`ve measured and identified bridging costs

### Now It`s Your Turn
- Explore your existing collections
- Measure your code
- Audit your mutable state
- Gain mastery in Playgrounds
