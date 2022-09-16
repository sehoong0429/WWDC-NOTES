

🍎 WWDC18 | Category : SwiftUI & UI Frameworks

Swift Generics (Expanded)
---
🔗 https://developer.apple.com/videos/play/wwdc2018/406/

WWDC 첫 영상 첫 정리


### A Simple Buffer Type


```swift
struct Buffer {
    var count: Int
    
    subscript(at: Int) -> ??? {
    // get/set from storage
    }
}

```
제네릭을 안쓰면 리턴타입을 정해주어야한다.

타입을 하나로 고정해두었기 때문에 다른 타입을 넣을 수 없다.

### Untyped Storage: Notice

```swift
var words: Buffer = ["subtyping", "ftw"]

// I know this array contains strings
words[0] as! String

// Uh-oh, now it doesn`t!
words[0] = 42
```
이렇게 Any 타입으로 되어있으면 매번 컴파일러에서 확인해야 하므로 overhead가 매우 증가한다.


# **Parametric Polymorphism**

컴파일러의 유연성을 위해 Parametric Polymorphism 즉 타입을 Generic하게 정하는 것을 Element을 사용할 수 있다.

Element가 여기에서 generics의 파라미터로 Parametric polymorphism이라고 한다.

이것이 컴파일러에게 어떤 것이 들어있는지 말해주고 있다.

```swift
struct Buffer<Element> {
  let count: Int
  
  subscript(at: Int) -> Element {
  // fetch from storage
  }
}

var words: Buffer<String> = ["generics","ftw"]

words[0]
words[0] =42

var boxes: Buffer<CGRect> = words
```
컴파일러가 타입이 맞지 않다면 바로 캐치해서 알려준다. (overhead)가 발생하지 않음

그러므로 타입 안정성을 추구할 수있다.

```swift
extension Buffer {
    func sum() -> Element {
        var total = 0
        for i in 0..<self.count {
            total += self[i]
        }
        return total
    }
}

let total = numbers.sum()
// 모든 타입 sum 불가해서 컴파일 이슈 발생
```

2가지 방법으로 해결 가능

```swift
extension Buffer where Element == Int {
    func sum() -> Element {
        var total = 0
        for i in 0..<self.count {
            total += self[i]
        }
        return total
    }

}

// 위 방법이나 아래방법 이용

extension Buffer where Element: Numeric {
    func sum() -> Element {
        var total: Element = 0
        for i in 0..<self.count {
            total += self[i]
        }
        return total
    }
}
```

### 연관 타입

```swift
protocol Collection {
    associatedtype Element
}

struct Buffer<Element> {}
extension Buffer: Collection {}

struct Array<Element> {}
extension Array: Collection {}

struct Dictionary<Key,Value> {}
extension Dictionary: Collection {
    typealias Element = (Key, Value)
}

protocol Collection {
    associatedtype Element

    var count: Int { get }
    subscript(at: Int) -> Element
}

extension Collection {
    func dump() {
        for i in 0..<count {
            print(self[i])
        }
    }
}

extension Collection where Index: Equatable {
    var count: Int {
        var i = 0
        var position = startIndex
        while position != endIndex {
            position = index(after: position)
            i += 1
        }
        return i
    }
}
```
Equatable은 타입끼리 비교(==) 하기 위해서 필수적으로 구현해야하는 프로토콜
하지만 매번 Equatable을 구현하기엔 번거로움이 있으니 이를 프로토콜을 이용하면 더 좋게 해결할 수 있다. ( 아래 코드 )

```swift
protocol Collection {
    associatedtype Element
    associatedtype Index: Equatable
// 이렇게하면 구현에서 해줄 필요없이 protocol에서 하므로 할 필요 없다.
```

### 양방향
```swift
// BidirectionalCollection 양방향 컬렉션, suffix(_:)와 같은 메서드를 사용할 수 있게 해줌
protocol RandomAccessCollection: BidirectionalCollection {
    func index(_ position: Index, offsetBy n: Int) -> Index
    func distance(from start: Index, to end: Index) -> Int
}

protocol MutableCollection: Collection {
    subscript (index: Index) -> Element { get set }
    mutating func swapAt(_: Index, _: Index) { }
}

// 이렇게 사용해서 클라이언트가 여러 개의 프로토콜들을 구성할 수 있게 만든다.

extension RandomAccessCollection where Self: MutableCollection {
    mutating func suhffle() {
        let n = count
        guard n > 1 else { return }
        for (i, pos) in indices.dropLast().enumerated() {
            let otherPos = index(startIndex, offsetBy: Int.random(in: i..<n))
            swapAt(pos, otherPos)
        }
    }
}
```

# Conditional conformance
특정조건이 충족될 때만 유형이 프로토콜을 준수하도록 허용한다.

예를 들어 Purchaseable 프로토콜이 있는 경우
```swift
protocol Purchaseable {
    func buy()
}
```
해당 프로토콜을 준수하는 간단한 유형
```swift
struct Book: Purchaseable {
    func buy() {
        print("You bought a book")
    }
}
```
다음 배열 내부의 모든 요소가 다음과 같은 경우 Array 준수하도록 만들 수 있다.
```swift
extension Array: Purchaseable where Element: Purchaseable {
    func buy() {
        for item in self {
            item.buy ()
        }
    }
}
```
Box참조
```swift
final class Box<T> {
    var value: T
    
    init(value: T) {
        self.value = value
    }
}
```
User 구조체 저장
```swift
struct User: Equatable {
    var username: String
}

let user = User(username: "twostraws")
let box1 = Box(value: user)
let box2 = Box(value: user)
```

```swift
extension Box: Equatable where T: Equatable {
    static func == (lhs: Box<T>, rhs: Box<T>) -> Bool {
        return lhs.value == rhs.value
    }
}
```

두 개의 상자 직접 선택 가능
```
box1 == box2
```

# Recursive Constraints
```swift
protocol Collection {
  associatedTyppe Element
  associatedType Index
  associatedType SubSequence: Collection
  	where SubSequence.Element == Element,
  				SubSequence.Index == Index,
  				SubSequence.SubSequence == SubSequence
}
```

### 마무리
- 리스코프 치환 원칙을 잘 생각하기

- 프로토콜의 채택도 서브 클래스에 상속된다.

- required initializer는 반드시 모든 서브 클래스에서 구현되어야 한다.

