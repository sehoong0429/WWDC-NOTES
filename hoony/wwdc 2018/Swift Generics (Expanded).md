

๐ WWDC18 | Category : SwiftUI & UI Frameworks

Swift Generics (Expanded)
---
๐ https://developer.apple.com/videos/play/wwdc2018/406/

WWDC ์ฒซ ์์ ์ฒซ ์ ๋ฆฌ


### A Simple Buffer Type


```swift
struct Buffer {
    var count: Int
    
    subscript(at: Int) -> ??? {
    // get/set from storage
    }
}

```
์ ๋ค๋ฆญ์ ์์ฐ๋ฉด ๋ฆฌํดํ์์ ์ ํด์ฃผ์ด์ผํ๋ค.

ํ์์ ํ๋๋ก ๊ณ ์ ํด๋์๊ธฐ ๋๋ฌธ์ ๋ค๋ฅธ ํ์์ ๋ฃ์ ์ ์๋ค.

### Untyped Storage: Notice

```swift
var words: Buffer = ["subtyping", "ftw"]

// I know this array contains strings
words[0] as! String

// Uh-oh, now it doesn`t!
words[0] = 42
```
์ด๋ ๊ฒ Any ํ์์ผ๋ก ๋์ด์์ผ๋ฉด ๋งค๋ฒ ์ปดํ์ผ๋ฌ์์ ํ์ธํด์ผ ํ๋ฏ๋ก overhead๊ฐ ๋งค์ฐ ์ฆ๊ฐํ๋ค.


# **Parametric Polymorphism**

์ปดํ์ผ๋ฌ์ ์ ์ฐ์ฑ์ ์ํด Parametric Polymorphism ์ฆ ํ์์ Genericํ๊ฒ ์ ํ๋ ๊ฒ์ Element์ ์ฌ์ฉํ  ์ ์๋ค.

Element๊ฐ ์ฌ๊ธฐ์์ generics์ ํ๋ผ๋ฏธํฐ๋ก Parametric polymorphism์ด๋ผ๊ณ  ํ๋ค.

์ด๊ฒ์ด ์ปดํ์ผ๋ฌ์๊ฒ ์ด๋ค ๊ฒ์ด ๋ค์ด์๋์ง ๋งํด์ฃผ๊ณ  ์๋ค.

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
์ปดํ์ผ๋ฌ๊ฐ ํ์์ด ๋ง์ง ์๋ค๋ฉด ๋ฐ๋ก ์บ์นํด์ ์๋ ค์ค๋ค. (overhead)๊ฐ ๋ฐ์ํ์ง ์์

๊ทธ๋ฌ๋ฏ๋ก ํ์ ์์ ์ฑ์ ์ถ๊ตฌํ  ์์๋ค.

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
// ๋ชจ๋  ํ์ sum ๋ถ๊ฐํด์ ์ปดํ์ผ ์ด์ ๋ฐ์
```

2๊ฐ์ง ๋ฐฉ๋ฒ์ผ๋ก ํด๊ฒฐ ๊ฐ๋ฅ

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

// ์ ๋ฐฉ๋ฒ์ด๋ ์๋๋ฐฉ๋ฒ ์ด์ฉ

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

### ์ฐ๊ด ํ์

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
Equatable์ ํ์๋ผ๋ฆฌ ๋น๊ต(==) ํ๊ธฐ ์ํด์ ํ์์ ์ผ๋ก ๊ตฌํํด์ผํ๋ ํ๋กํ ์ฝ
ํ์ง๋ง ๋งค๋ฒ Equatable์ ๊ตฌํํ๊ธฐ์ ๋ฒ๊ฑฐ๋ก์์ด ์์ผ๋ ์ด๋ฅผ ํ๋กํ ์ฝ์ ์ด์ฉํ๋ฉด ๋ ์ข๊ฒ ํด๊ฒฐํ  ์ ์๋ค. ( ์๋ ์ฝ๋ )

```swift
protocol Collection {
    associatedtype Element
    associatedtype Index: Equatable
// ์ด๋ ๊ฒํ๋ฉด ๊ตฌํ์์ ํด์ค ํ์์์ด protocol์์ ํ๋ฏ๋ก ํ  ํ์ ์๋ค.
```

### ์๋ฐฉํฅ
```swift
// BidirectionalCollection ์๋ฐฉํฅ ์ปฌ๋ ์, suffix(_:)์ ๊ฐ์ ๋ฉ์๋๋ฅผ ์ฌ์ฉํ  ์ ์๊ฒ ํด์ค
protocol RandomAccessCollection: BidirectionalCollection {
    func index(_ position: Index, offsetBy n: Int) -> Index
    func distance(from start: Index, to end: Index) -> Int
}

protocol MutableCollection: Collection {
    subscript (index: Index) -> Element { get set }
    mutating func swapAt(_: Index, _: Index) { }
}

// ์ด๋ ๊ฒ ์ฌ์ฉํด์ ํด๋ผ์ด์ธํธ๊ฐ ์ฌ๋ฌ ๊ฐ์ ํ๋กํ ์ฝ๋ค์ ๊ตฌ์ฑํ  ์ ์๊ฒ ๋ง๋ ๋ค.

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
ํน์ ์กฐ๊ฑด์ด ์ถฉ์กฑ๋  ๋๋ง ์ ํ์ด ํ๋กํ ์ฝ์ ์ค์ํ๋๋ก ํ์ฉํ๋ค.

์๋ฅผ ๋ค์ด Purchaseable ํ๋กํ ์ฝ์ด ์๋ ๊ฒฝ์ฐ
```swift
protocol Purchaseable {
    func buy()
}
```
ํด๋น ํ๋กํ ์ฝ์ ์ค์ํ๋ ๊ฐ๋จํ ์ ํ
```swift
struct Book: Purchaseable {
    func buy() {
        print("You bought a book")
    }
}
```
๋ค์ ๋ฐฐ์ด ๋ด๋ถ์ ๋ชจ๋  ์์๊ฐ ๋ค์๊ณผ ๊ฐ์ ๊ฒฝ์ฐ Array ์ค์ํ๋๋ก ๋ง๋ค ์ ์๋ค.
```swift
extension Array: Purchaseable where Element: Purchaseable {
    func buy() {
        for item in self {
            item.buy ()
        }
    }
}
```
Box์ฐธ์กฐ
```swift
final class Box<T> {
    var value: T
    
    init(value: T) {
        self.value = value
    }
}
```
User ๊ตฌ์กฐ์ฒด ์ ์ฅ
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

๋ ๊ฐ์ ์์ ์ง์  ์ ํ ๊ฐ๋ฅ
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

### ๋ง๋ฌด๋ฆฌ
- ๋ฆฌ์ค์ฝํ ์นํ ์์น์ ์ ์๊ฐํ๊ธฐ

- ํ๋กํ ์ฝ์ ์ฑํ๋ ์๋ธ ํด๋์ค์ ์์๋๋ค.

- required initializer๋ ๋ฐ๋์ ๋ชจ๋  ์๋ธ ํด๋์ค์์ ๊ตฌํ๋์ด์ผ ํ๋ค.

