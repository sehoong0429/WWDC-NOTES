🍎 WWDC18 | Category : Swift 
<br>
## Create Your Own Swift Playgrounds Subscription
🔗 [https://developer.apple.com/videos/play/wwdc2018/413/](https://developer.apple.com/videos/play/wwdc2018/413/)

### Swift Playgrounds 
- Swift Playgrounds는 누구나 Swift 프로그래밍 언어를 사용하여 iPad에서 코딩할 수 있는 어플

#### Playground book format review
- Playground book : mechanism for you to construct a guide interactive exploration of a particular topic
- You can guide your learners through a sequence of chapters, which are then further subdivided into pages.
- To bundle all if this into a single file they use a package based file format.
- Playground book is itself a file hierachy. It contains a subdirectory for each chapter and nested within each chapter is a folder for each page in that chapter. 
- You can use auxiliary source files to achieve many different tasks. And by utillizinig sources, you can greatly simplify the code that you need to write in each page in your book! 


#### Swift Playgrounds Author Template
- LiveViewTestApp allows you to debug your live view in a full screen or in a side-by-side mode without first having to export your Playground book to Swift Playgrounds.
- The Swift playgrounds Author Template comes with three supporting frameworks. and Including frameworks in the project allows the book sources and the LiveViewTestApp targets to take full advantage of the APIs from frameworks.
  - Playground Support 
  - Playground Bluetooth 
  - LiveViewHost : LiveViewTestApp for displaying the live view.

#### Swift Playgrounds subscription format overview
- Subsscription content is hosted online 
- The way that you publish your content will be through publishing JSON files that have all of the data that Swift Playgrounds needs to download your content.

#### Hosting your own subscription feed 
- JSON file and all of your documents that you've written on the web. For this, you'll need a web host! Publishing your subscription requires a web host.
  - GitHub pages : you must be named "username.github.io" 
  - Squarespace 
  - and others
