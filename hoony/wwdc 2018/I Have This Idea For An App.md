🍎 WWDC18 | Category : SwiftUI & UI Frameworks

Swift I Have This Idea For An App...
---
🔗 https://developer.apple.com/videos/play/wwdc2018/203/

"창조적인 삶을 살기 위해서는 틀릴 것에 대한 두려움을 잃어야 합니다" -조셉 찰튼 피어스(Joseph Chilton Pearce)-

영상에선 기본적인 앱 만드는 방법 및 MVC 패턴이 무엇인지 소개하고 있고, 앱 빌드 과정에서 MVC 패턴을 적용하여 파일을 정리하고 있지는 않는다.

코드를 따라치는것 보다는 여기에서 알려준 영상들을 기록 해놓고 그 영상들을 볼 때마다 따로 정리할 계획이다!

## Our Journey
- Dream big and organize our ideas
- Learn to navigate Xcode
- Build a simple game using Swift
- Add multiple views within our app
- Persist and display data for users

<img width="1126" alt="스크린샷 2022-09-21 오전 7 49 52" src="https://user-images.githubusercontent.com/111875357/191378451-a7072e70-224a-4d13-912e-67099b2dd0b7.png">


### Taking It Further
- Use SpriteKit to give more life to your good and bad buttons (Introduction to SpriteKit WWDC 2013)
- Add MusicKit integration to incorporate sound into the game play (Introduction MusicKit WWDC 2017 
- Read from sensors and change the speed of the game based on user movement (Creating Immersive Apps with Core Motion WWDC 2017)


<img width="1135" alt="스크린샷 2022-09-21 오전 7 57 13" src="https://user-images.githubusercontent.com/111875357/191379241-4cbabf27-e3ff-45db-abdb-cbee200ef395.png">

<img width="1135" alt="스크린샷 2022-09-21 오전 7 57 30" src="https://user-images.githubusercontent.com/111875357/191379292-796d1e46-5f46-4a58-a959-285019ac087d.png">

### Saving Data
- Core Data Best Practices (WWDC 2018)
- Networking wuth NSURLSession (WWDC 2015)
- Introducing CloudKit (WWDC 2014)

### View Controllers
- View Controller Programming Guide for iOS (Apple Developer Documentation)
- Table View Programmijng Guide (Apple Developer Documentation)
- Navigation Controllers (Apple Developer Documentation)

### Auto LayOut
- Mysteries of Auto Layout, Part 1 (WWDC 2015)
- Auto Layout Techniques in Interface Builder (WWDC 2017)
- High Performance Auto Layout (WWDC 2018)

### Next Steps
- Test your app using XCTest framework
- Review App Store Review Guidelines
- Enroll in the Apple Developer Program
- Submit for App Review
- Tell the world!

## Unit Test (모든 단위 테스트는 애플의 XCTest framework에 의존한다)

🔗 https://x-team.com/blog/how-to-get-started-with-ios-unit-tests-in-swift/

🔗 https://zeddios.tistory.com/48

🔗 https://silver-g-0114.tistory.com/142

🔗 https://ssowonny.medium.com/%EC%84%A4%EB%A7%88-%EC%95%84%EC%A7%81%EB%8F%84-%ED%85%8C%EC%8A%A4%ED%8A%B8-%EC%BD%94%EB%93%9C%EB%A5%BC-%EC%9E%91%EC%84%B1-%EC%95%88-%ED%95%98%EC%8B%9C%EB%82%98%EC%9A%94-b54ec61ef91a

유닛테스트는 컴퓨터 프로그래밍에서 소스 코드의 특정 모듈이 의도된 대로 정확히 작동하는지 검증하는 절차다. 즉 모든 함수와 메소드에 대한 테스트 케이스(Test case)를 작성하는 절차를 말한다.

- 각각의 모듈을 부분적으로 확인할 수 있어 어떤 모듈에서 문제가 발생하는지 빠른 확인이 가능하다.
- 전체 프로그램을 빌드하는 대신 유닛 단위로 빌드해 확인하므로 시간 절약이 가능하다.

## 2017년 기준

<img width="838" alt="스크린샷 2022-09-21 오전 8 36 38" src="https://user-images.githubusercontent.com/111875357/191383147-99f12907-856b-4d70-9af5-f263386f0d68.png">

setup(): 초기화 코드 (테스트 케이스가 시작될 때 테스트 케이스이 첫 번째 테스트가 실행되기 전에 정확히 한 번 호출됩니다.)

tear Down(): 해체 코드 (모든 개별 테스트가 실행 된 후 테스트 케이스가 끝날 때 정확히 한 번 호출됩니다.)


<img width="1381" alt="스크린샷 2022-09-21 오전 8 43 49" src="https://user-images.githubusercontent.com/111875357/191383825-aa265608-4d5d-4a8d-9474-692c785c8158.png">

Run해버리는 것이 아닌 마름모를 클릭하면 테스트 할 수 있음! 잘못되면 마름모에 x 표시로 테스트 통과 못했다고 알려준다.

## Summary
- Explore Xcode
- Build a user interface
- Think about the data
- Create good experiences for all devices
- Follow best practices
- Congratulations! You`re an iOS App Developer!
