๐ WWDC18 | Category : SwiftUI & UI Frameworks
<br>
## High Performance Auto Layout
๐ [https://developer.apple.com/videos/play/wwdc2018/220/](https://developer.apple.com/videos/play/wwdc2018/220/)

### Auto Layout 
- ์คํ ๋ ์ด์์์ Engine(layout cache, dependency tracker)์ ํตํด์ ๋ฐฉ์ ์์ ๊ณ์ฐํด์ ๋ง๋ค๊ณ  ๊ณ์ฐ ๋ ๊ฐ์ ํตํด ๋ ์ด์์์ ์๋ฐ์ดํธ
- iOS์์ ์ฝํ์ธ ๋ฅผ ๋ฐฐ์นํ๋ ๋ฐฉ๋ฒ 
- ๊ธฐ์กด์ Frame-Based Layout๊ณผ ๋ค๋ฅธ View๋ค ๊ฐ์ ๊ด๊ณ๋ฅผ ์ด์ฉํ์ฌ View์ ์์น์ ํฌ๊ธฐ๋ฅผ ์๋์ผ๋ก ๊ฒฐ์ ํ๋ Layout System
- ๊ด๊ณ๋ Constraint๋ก ์ค์ ์ด ๊ฐ๋ฅ
- View์ ์ฃผ์ด์ง ์ ์ฝ์กฐ๊ฑด์ ๋ฐ๋ผ View์ ํฌ๊ธฐ์ ์์น๋ฅผ ๋์ ์ผ๋ก ๊ณ์ฐํด ๋ฐฐ์นํ๊ณ  ์ธ๋ถ ๋๋ ๋ด๋ถ์ ๋ณํ์ ๋์ ์ผ๋ก ๋ฐ์ํ์ฌ User Interface๋ฅผ ๊ตฌ์ฑ

### The Render Loop 
<img width="800" alt="image" src="https://user-images.githubusercontent.com/67987230/193951201-cc47c799-a25b-498e-af78-e378284d6b47.png">

- What is updateConstraints?
     - Update Constraint ํจ์๋ Render loop์ ์ํจ
- ์ด๋น 120 ํ๋ ์์ ์คํ
- ๋ณ๋ ฌ์ ์ผ๋ก ์ด๋ฃจ์ด์ง 
- ์ค์ ๋ก ํ์ํ ๊ฒฝ์ฐ(์ค๋ณต ์์ ํผํ๊ธฐ)์ ์ ์ฉ 
- ์์ฑํ๋ ๋น๋๋ฅผ ์ต์ํ
     - 1์ด๋ง๋ค 120๋ฒ ์คํ๋๊ธฐ ๋๋ฌธ์ ๊ณ์ constraint๋ฅผ ๋ง๋ค์๋ค ์์ด๋ค ํ์ง๋ง๊ณ  ํ๋ฒ๋ง ์์ฑ๋๋๋ก!
- Interface Builder๋ฅผ ์ฌ์ฉํ  ์ ์์ผ๋ฉด ์ต๋ํ Interface Builder๋ฅผ ์ฌ์ฉํ๊ธฐ 


โญ๏ธ ์ฐธ๊ณ ํ๋ฉด ์ข์ ๋ธ๋ก๊ทธ โญ๏ธ<br>
https://vapor3965.tistory.com/20
