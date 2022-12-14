๐ WWDC18 | Category : Swift 
<br>
## What's New in Swift
๐ [https://developer.apple.com/videos/play/wwdc2018/401/](https://developer.apple.com/videos/play/wwdc2018/401/)

## what is Swift 4.2 ?
### ๊ฐ๋ฐ์ ์์ฐ์ฑ  
  - Faster builds 
  - Language features to improve efficiency and remove boilerplate 
  - SDK(iOS๊ฐ๋ฐ์ ์ํ ๊ฐ๋ฐ ํค๋)improvements for Swift
      -  Updates to important framework APIs
      - Some API changes will land in later Xcode 10 betas
  - Converging towards binary compatibility <br>
      - Swift5์์ ๋ค๋ฅธ Swift ๋ฒ์ ์ผ๋ก ์ปดํ์ผ ๋ ๋ผ์ด๋ธ๋ฌ๋ฆฌ์ ์ฑ ์ฌ์ด์ ๋ฐ์ด๋๋ฆฌ ํธํ์ฑ์ ๊ฐ๋ฅํ๊ฒ ํ๋ ABI stability๋ฅผ ์ด๋ฃจ๊ธฐ ์ํจ
      - ์๊ฐ, ๋ฉ๋ชจ๋ฆฌ ์ฌ์ฉ๋์๋ ์ํฅ์ ๋ฏธ์นจ. 

### ์ธ์ด๊ฐ์  

- Collection of Enum Cases
  - ๊ธฐ์กด 4.1 ๋ฒ์  
   
    ```swift
    //๊ฐ๋ฅํ ๋ชจ๋  ๊ฒฝ์ฐ์ ๋ชฉ๋ก์ผ๋ก ์์ฑ์ ์ ์ ํด์ผํ๊ณ , 
    //์ ์ผ์ด์ค๋ฅผ ์ถ๊ฐํ๋ฉด ํด๋น ์์ฑ์ ์๋ฐ์ดํธ ํด์ผํจ.
     enum Exercise {
        case walking 
        case running
        case climbing 
     
        static var allCases: [Exercise] = [.walking, .running] 
      }
      for gait in Exercise.allCases {
        print(gait)
      }

    ```
  - Swift 4.2์์ ๋ณ๊ฒฝ ๋ ํ
    ```swift
    //์ด๋ค ์ปฌ๋ ์์ ๋ชจ๋  ๊ฐ๋ค์ ์ ๊ณตํ๋ ํ์์ CaseIterable ํ๋กํ ์ฝ ์ถ๊ฐ 
    enum Exercise: CaseIterable {
        case walking 
        case running
        case climbing 
    }

    // CaseIterable ํ๋กํ ์ฝ์ ์ฑํํ๋ฉด, allCases๋ผ๋ ํ๋กํผํฐ๋ฅผ ํตํด ๋ชจ๋  ์ผ์ด์ค์ ๊ฐ์ ๊ฐ์ ธ์ด.
    for gait in Exercise.allCases {
        print(gait)
    }
    ```

- Conditional Conformance (์กฐ๊ฑด๋ถ ์ ํฉ์ฑ)
  - swift 4.0  -> 4.2 
  ```swift
  //swift 4.0์์๋ ์ํ์ค์ ์์ ์ ํ์ด Equtable์ด์ด์ผ ์ฐพ์ผ๋ ค๋ ์์๋ฅผ ์ฐพ์ ์ ์๋ค. 
  //*Equatable์ ํ์๋ผ๋ฆฌ ๋น๊ต(==)์ฐ์ฐ์ ํ๊ธฐ ์ํด์  ํ์์ ์ผ๋ก ๊ตฌํํด์ผ ํ๋ ํ๋กํ ์ฝ
  extension Sequence where Element: Equatable { 
      func contains(_ element: Element) -> Bool
  }
  let animals = ["cat", "dog", "weasel"]
  animals.contains("dog") // ๋ฌธ์์ด์ด Equtable์ด๊ธฐ ๋๋ฌธ์ OK

  let coins = [[1, 2], [3, 6], [4, 12]] //๋ฐฐ์ด๋ด์ ๋ฐฐ์ด์ ๊ฐ๋ฅํ ๊น? 
  coins.contains([3, 6]) //์ปดํ์ผ ์ค๋ฅ 
  
  ```
  - ์์ ๊ฐ์ด 4.0์์ ์ค๋ฅ ๋ฌ๋ ๋ถ๋ถ์ด Swift 4.2์์๋ ๊ฐ๋ฅ.
  - ์ด ๊ธฐ๋ฅ์ ํ์ฅ์์ Hashable, Encodable, Decodable ์ ํฉ์ฑ๋ ์ ์ฉ.
  
- Hashable Enhancements (ํด์๋ธ ๊ฐ์ ์ฌํญ) 
  - ๊ธฐ์กด ๋ฌธ์ ์  
    - Too much magic 
    - Performance problems 
    - Denial of service attacks
    - Need a better API!


  ```swift

  // Swift 4.1
  //Hashable์ธ ๊ฒฝ์ฐ set์ด๋ ๋์๋๋ฆฌ์ ๊ฐ์ ์ถ๊ฐํ  ์ ์๊ณ ,
  //hasValue๋ฅผ ์ง์  ์ปค์คํํ๋ ๊ฒ์ด ๊ฐ๋ฅํ๊ณ ,
  //๊ตฌํ์ด ์ดํดํ๊ธฐ ์ด๋ ค์ด๋ฐ๋ค ์ ๋ขฐํ ์ ์๋ ์์ค ๊ฐ์ ๋ํด ๋นํจ์จ์ .
  protocol Hashable {
    var hashValue: Int { get }
  }

  //Swift 4.2
  protocol Hashable {
    //hash(into:)์ ์๊ตฌ์ฌํญ์ ๋์ด์ ์ฌ์ฉํ์ง ์์ hashValue ํ๋กํผํฐ๋ฅผ ๋์ฒดํ๊ธฐ ์ํ๊ฒ
    func hash(into hasher: inout Hasher) 
    //hash function์ Hashable ํ๋กํ ์ฝ์ ์ ์ธ๋ ๋ฉ์๋, hashValue๋ฅผ ์ ์ํ๋ ๋ฉ์๋ 
  }
  ```
  
  - Hasher์ ๋ณต์๋ ฅ์ด ์๋ ๊ตฌ์กฐ์ฒด๋ผ ๊ธฐ์กด ์ฝ๋ ๋ณ๊ฒฝ ๋ฐ ์ปดํ์ผ ํ์์์ด Hash๊ธฐ๋ฅ์ ํฅ์ ์ํฌ ์ ์๋ค.
  ```swift
    
    //Swift 4.1
    var hashValue: Int {
      return x.hashValue ^ y.hashValue &* 16777619 // ์ด๋ฐ์์ผ๋ก hashvalue๋ฅผ ๋ง๋ค๋ฉด ์ดํด ํ๊ธฐ ์ด๋ ค์ 
    }
    
    //Swift 4.2
    struct iPad: Hashable {
      var serialNumber: String
      var capacity: Int
      
    func hash(into hasher: inout Hasher) {
      //ํด์ํจ์๋ฅผ ์ด์ฉํ์ฌ ํด์๊ฐ์ ๊ตฌํ๋๋ฐ 
      //Hasher๊ฐ์ฒด ์์ ๋ค์ด์์ด์ Hasher์๊ฒ ํ๋กํผํฐ๋ง combine ํด์ฃผ๋ฉด ํด์ ์ ์๊ฐ์ ์ ๊ณต
      hasher.combine(serialNumber)  //๋จ์ํ๊ฒ combine์ ํ๋ผ๋ฏธํฐ๋ก serialNumber ๋ฃ๊ธฐ
     }
      //combine์ ๋ฐ๋ณต์ ์ผ๋ก ํธ์ถํด์ ํ๋กํผํฐ๋ฅผ ์ถ๊ฐ ํ  ์ ์๊ณ ,
      //๊ทธ ์ถ๊ฐ๋๋ ์์๋ ์์ฑ๋ hashValue์ ์ํฅ์ ์ค. 
    }
    
     var hasher = Hasher() //๋๋ฆฝ์ ์ธ hash์์ฑ๊ธฐ๋ก ์ฌ์ฉ๋ ๊ฐ๋ฅ 
     hasher.combine(first)
     hasher.combine(second)
     let lastHash = hasher.finalize() //์ต์ข hash๊ฐ ์์ฑ 
  ```
    - Hasher๋ ๊ฐ์ฒด๋ฅผ Hashํ ๋๋ง๋ค ์์์ ๊ฐ์ ์ฌ์ฉํจ์ผ๋ก, ๋ชจ๋  ๊ฐ์ฒด์ hash๊ฐ์ด ๋ค๋ฅด๋ค๋ ๊ฒ์ ๋ณด์ฅํด์ค. 
