π WWDC18 | Category : SwiftUI & UI Frameworks

Swift I Have This Idea For An App...
---
π https://developer.apple.com/videos/play/wwdc2018/203/

"μ°½μ‘°μ μΈ μΆμ μ΄κΈ° μν΄μλ νλ¦΄ κ²μ λν λλ €μμ μμ΄μΌ ν©λλ€" -μ‘°μ μ°°νΌ νΌμ΄μ€(Joseph Chilton Pearce)-

μμμμ  κΈ°λ³Έμ μΈ μ± λ§λλ λ°©λ² λ° MVC ν¨ν΄μ΄ λ¬΄μμΈμ§ μκ°νκ³  μκ³ , μ± λΉλ κ³Όμ μμ MVC ν¨ν΄μ μ μ©νμ¬ νμΌμ μ λ¦¬νκ³  μμ§λ μλλ€.

μ½λλ₯Ό λ°λΌμΉλκ² λ³΄λ€λ μ¬κΈ°μμ μλ €μ€ μμλ€μ κΈ°λ‘ ν΄λκ³  κ·Έ μμλ€μ λ³Ό λλ§λ€ λ°λ‘ μ λ¦¬ν  κ³νμ΄λ€!

## Our Journey
- Dream big and organize our ideas
- Learn to navigate Xcode
- Build a simple game using Swift
- Add multiple views within our app
- Persist and display data for users

<img width="1126" alt="αα³αα³αα΅α«αα£αΊ 2022-09-21 αα©αα₯α« 7 49 52" src="https://user-images.githubusercontent.com/111875357/191378451-a7072e70-224a-4d13-912e-67099b2dd0b7.png">


### Taking It Further
- Use SpriteKit to give more life to your good and bad buttons (Introduction to SpriteKit WWDC 2013)
- Add MusicKit integration to incorporate sound into the game play (Introduction MusicKit WWDC 2017 
- Read from sensors and change the speed of the game based on user movement (Creating Immersive Apps with Core Motion WWDC 2017)


<img width="1135" alt="αα³αα³αα΅α«αα£αΊ 2022-09-21 αα©αα₯α« 7 57 13" src="https://user-images.githubusercontent.com/111875357/191379241-4cbabf27-e3ff-45db-abdb-cbee200ef395.png">

<img width="1135" alt="αα³αα³αα΅α«αα£αΊ 2022-09-21 αα©αα₯α« 7 57 30" src="https://user-images.githubusercontent.com/111875357/191379292-796d1e46-5f46-4a58-a959-285019ac087d.png">

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

## Unit Test (λͺ¨λ  λ¨μ νμ€νΈλ μ νμ XCTest frameworkμ μμ‘΄νλ€)

π https://x-team.com/blog/how-to-get-started-with-ios-unit-tests-in-swift/

π https://zeddios.tistory.com/48

π https://silver-g-0114.tistory.com/142

π https://ssowonny.medium.com/%EC%84%A4%EB%A7%88-%EC%95%84%EC%A7%81%EB%8F%84-%ED%85%8C%EC%8A%A4%ED%8A%B8-%EC%BD%94%EB%93%9C%EB%A5%BC-%EC%9E%91%EC%84%B1-%EC%95%88-%ED%95%98%EC%8B%9C%EB%82%98%EC%9A%94-b54ec61ef91a

μ λνμ€νΈλ μ»΄ν¨ν° νλ‘κ·Έλλ°μμ μμ€ μ½λμ νΉμ  λͺ¨λμ΄ μλλ λλ‘ μ νν μλνλμ§ κ²μ¦νλ μ μ°¨λ€. μ¦ λͺ¨λ  ν¨μμ λ©μλμ λν νμ€νΈ μΌμ΄μ€(Test case)λ₯Ό μμ±νλ μ μ°¨λ₯Ό λ§νλ€.

- κ°κ°μ λͺ¨λμ λΆλΆμ μΌλ‘ νμΈν  μ μμ΄ μ΄λ€ λͺ¨λμμ λ¬Έμ κ° λ°μνλμ§ λΉ λ₯Έ νμΈμ΄ κ°λ₯νλ€.
- μ μ²΄ νλ‘κ·Έλ¨μ λΉλνλ λμ  μ λ λ¨μλ‘ λΉλν΄ νμΈνλ―λ‘ μκ° μ μ½μ΄ κ°λ₯νλ€.

## 2017λ κΈ°μ€

<img width="838" alt="αα³αα³αα΅α«αα£αΊ 2022-09-21 αα©αα₯α« 8 36 38" src="https://user-images.githubusercontent.com/111875357/191383147-99f12907-856b-4d70-9af5-f263386f0d68.png">

setup(): μ΄κΈ°ν μ½λ (νμ€νΈ μΌμ΄μ€κ° μμλ  λ νμ€νΈ μΌμ΄μ€μ΄ μ²« λ²μ§Έ νμ€νΈκ° μ€νλκΈ° μ μ μ νν ν λ² νΈμΆλ©λλ€.)

tear Down(): ν΄μ²΄ μ½λ (λͺ¨λ  κ°λ³ νμ€νΈκ° μ€ν λ ν νμ€νΈ μΌμ΄μ€κ° λλ  λ μ νν ν λ² νΈμΆλ©λλ€.)


<img width="1381" alt="αα³αα³αα΅α«αα£αΊ 2022-09-21 αα©αα₯α« 8 43 49" src="https://user-images.githubusercontent.com/111875357/191383825-aa265608-4d5d-4a8d-9474-692c785c8158.png">

Runν΄λ²λ¦¬λ κ²μ΄ μλ λ§λ¦λͺ¨λ₯Ό ν΄λ¦­νλ©΄ νμ€νΈ ν  μ μμ! μλͺ»λλ©΄ λ§λ¦λͺ¨μ x νμλ‘ νμ€νΈ ν΅κ³Ό λͺ»νλ€κ³  μλ €μ€λ€.

## Summary
- Explore Xcode
- Build a user interface
- Think about the data
- Create good experiences for all devices
- Follow best practices
- Congratulations! You`re an iOS App Developer!
