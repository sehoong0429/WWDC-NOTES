🍎 WWDC18 | Category : SwiftUI & UI Frameworks
<br>
## High Performance Auto Layout
🔗 [https://developer.apple.com/videos/play/wwdc2018/220/](https://developer.apple.com/videos/play/wwdc2018/220/)

### Auto Layout 
- 오토레이아웃은 Engine(layout cache, dependency tracker)을 통해서 방정식을 계산하고, 계산 된 값을 통해 레이아웃을 업데이트
- iOS에서 콘텐츠를 배치하는 방법 
- 기존의 Frame-Based Layout과 다른 View들 간의 관계를 이용하여 View의 위치와 크기를 자동으로 결정하는 Layout System
- 관계는 Constraint로 설정이 가능
- View에 주어진 제약조건에 따라 View의 크기와 위치를 동적으로 계산해 배치하고 외부 또는 내부의 변화에 동적으로 반응하여 User Interface를 구성

### The Reder Loop 
<img width="800" alt="image" src="https://user-images.githubusercontent.com/67987230/193951201-cc47c799-a25b-498e-af78-e378284d6b47.png">

- What is updateConstraints?
     - Update Constraint 함수는 Render loop에 속함
- 초당 120 프레임을 실행
- 병렬적으로 이루어짐 
- 실제로 필요한 경우(중복 작업 피하기)에 유용 
- 작성하는 빈도를 최소화
     - 1초마다 120번 실행되기 때문에 계속 constraint를 만들었다 없앴다 하지말고 한번만 생성되도록!
- Interface Builder를 사용할 수 있으면 최대한 Interface Builder를 사용하기 
