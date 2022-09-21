🍎 WWDC18 | Category : Swift 
<br>
## What's New in Swift
🔗 [https://developer.apple.com/videos/play/wwdc2018/401/](https://developer.apple.com/videos/play/wwdc2018/401/)

## what is Swift 4.2 ?
### 개발자 생산성  
  - Faster builds 
  - Language features to improve efficiency and remove boilerplate 
  - SDK(iOS개발을 위한 개발 키드)improvements for Swift
      -  Updates to important framework APIs
      - Some API changes will land in later Xcode 10 betas
  - Converging towards binary compatibility <br>
      - Swift5에서 다른 Swift 버전으로 컴파일 된 라이브러리와 앱 사이의 바이너리 호환성을 가능하게 하는 ABI stability를 이루기 위함
      - 시간, 메모리 사용량에도 영향을 미침. 

### 언어개선 

- Collection of Enum Cases
  - 기존 4.1 버전 
   
    ```swift
    //가능한 모든 경우의 목록으로 속성을 정의 해야하고, 
    //새 케이스를 추가하면 해당 속성을 업데이트 해야함.
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
  - Swift 4.2에서 변경 된 후
    ```swift
    //어떤 컬렉션의 모든 값들을 제공하는 타입의 CaseIterable 프로토콜 추가 
    enum Exercise: CaseIterable {
        case walking 
        case running
        case climbing 
    }

    // CaseIterable 프로토콜을 채택하면, allCases라는 프로퍼티를 통해 모든 케이스의 값을 가져옴.
    for gait in Exercise.allCases {
        print(gait)
    }
    ```

- Conditional Conformance (조건부 적합성)
  - swift 4.0  -> 4.2 
  ```swift
  //swift 4.0에서는 시퀀스의 요소 유형이 Equtable이어야 찾으려는 요소를 찾을 수 있다. 
  //*Equatable은 타입끼리 비교(==)연산을 하기 위해선 필수적으로 구현해야 하는 프로토콜
  extension Sequence where Element: Equatable { 
      func contains(_ element: Element) -> Bool
  }
  let animals = ["cat", "dog", "weasel"]
  animals.contains("dog") // 문자열이 Equtable이기 때문에 OK

  let coins = [[1, 2], [3, 6], [4, 12]] //배열내의 배열은 가능할까? 
  coins.contains([3, 6]) //컴파일 오류 
  
  ```
  - 위와 같이 4.0에서 오류 났던 부분이 Swift 4.2에서는 가능.
  - 이 기능은 확장에서 Hashable, Encodable, Decodable 적합성도 적용.
  
- Hashable Enhancements (해셔블 개선사항) 
  - 기존 문제점 
    - Too much magic 
    - Performance problems 
    - Denial of service attacks
    - Need a better API!


  ```swift

  // Swift 4.1
  //Hashable인 경우 set이나 딕셔너리에 값을 추가할 수 있고,
  //hasValue를 직접 커스텀하는 것이 가능하고,
  //구현이 이해하기 어려운데다 신뢰할수 없는 소스 값에 대해 비효율적.
  protocol Hashable {
    var hashValue: Int { get }
  }

  //Swift 4.2
  protocol Hashable {
    //hash(into:)의 요구사항은 더이상 사용하지 않을 hashValue 프로퍼티를 대체하기 위한것
    func hash(into hasher: inout Hasher) 
    //hash function은 Hashable 프로토콜에 선언된 메소드, hashValue를 정의하는 메소드 
  }
  ```
  
  - Hasher은 복원력이 있는 구조체라 기존 코드 변경 및 컴파일 필요없이 Hash기능을 향상 시킬 수 있다.
  ```swift
    
    //Swift 4.1
    var hashValue: Int {
      return x.hashValue ^ y.hashValue &* 16777619 // 이런식으로 hashvalue를 만들면 이해 하기 어려움 
    }
    
    //Swift 4.2
    struct iPad: Hashable {
      var serialNumber: String
      var capacity: Int
      
    func hash(into hasher: inout Hasher) {
      //해시함수를 이용하여 해시값을 구하는데 
      //Hasher객체 안에 들어있어서 Hasher에게 프로퍼티만 combine 해주면 해시 정수값을 제공
      hasher.combine(serialNumber)  //단순하게 combine의 파라미터로 serialNumber 넣기
     }
      //combine을 반복적으로 호출해서 프로퍼티를 추가 할 수 있고,
      //그 추가되는 순서는 완성된 hashValue에 영향을 줌. 
    }
    
     var hasher = Hasher() //독립적인 hash생성기로 사용도 가능 
     hasher.combine(first)
     hasher.combine(second)
     let lastHash = hasher.finalize() //최종 hash값 생성 
  ```
    - Hasher는 객체를 Hash할때마다 임의의 값을 사용함으로, 모든 객체의 hash값이 다르다는 것을 보장해줌. 
