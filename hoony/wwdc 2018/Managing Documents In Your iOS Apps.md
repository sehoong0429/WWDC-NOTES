

🍎 WWDC18 | Category : SwiftUI & UI Frameworks

Managing Documents In Your iOS Apps
---
🔗 https://developer.apple.com/videos/play/wwdc2018/216/

문서 관리

iOS 앱에서 문서를 효과적으로 관리하는 방법과 Documents Picker와 Documents browser의 차이점과 사용 시기에 관한 내용들이다. 한 번도 안 써본 내용이기에 처음 들을때 이해 하기 쉽진 않았다.

## Document Management on iOS
#### What is it?
- API for application developers
- File provider API for cloud vendors
- Files app

UIDocumentBrowserViewController (iOS 11)

UIDocumentPickerViewController (개선)

고객이 선호하는 모든 클라우드 공급업체의 파일을 관리하고 탐색할 수 있다.

#### Client API
- Document Browser (UIDocumentBrowserViewController)
- Document Picker (UIDocumentPickerViewController)
- File Coordination (NSFileCoordinator, UIDocument)
- File Operations (NSFileManager)
- Building Great Document=based Apps in iOS 11 (WWDC 2017)

#### File Provider API
- File Provider Extension -> 로그인 화면을 포함한 사용자 정의 UI 작업 작성 가능 (NSFileProviderExtension)
- File Provider Custom Actions (FPUIActionextensionViewController)
- File Provider Enhancements (WWDC 2017)

테스트를 실행하고 파일 제공자, 확장자에 대한 문제를 보여주고 문제를 해결하도록 안내한다.
<img width="1163" alt="스크린샷 2022-09-23 오전 7 58 02" src="https://user-images.githubusercontent.com/111875357/191865664-5cccb862-f918-46bd-83c6-eab6cc8d3323.png">

<img width="1141" alt="스크린샷 2022-09-23 오전 8 03 46" src="https://user-images.githubusercontent.com/111875357/191866317-f52b5958-ee17-4ab4-9f86-652ec9ae1ee8.png">

### Siri Shourcuts
- 열리거나 최근에 생성되어 사용한 문서를 표시하고 검색이나 잠금화면에서 볼 수 있도록 한다.
<img width="1137" alt="스크린샷 2022-09-23 오전 8 05 22" src="https://user-images.githubusercontent.com/111875357/191866535-eba5ae55-fb9e-47da-84ee-5db5a79f8d2d.png">

<img width="1152" alt="스크린샷 2022-09-23 오전 8 05 31" src="https://user-images.githubusercontent.com/111875357/191866542-ef730e3d-2da8-4e7c-bae8-123aff799fa7.png">

<img width="1159" alt="스크린샷 2022-09-23 오전 8 05 45" src="https://user-images.githubusercontent.com/111875357/191867799-6447a41b-9c6d-4b94-b3b4-7237e62aa9ee.png">


## Document Picker vs Document Broswer

<img width="1153" alt="스크린샷 2022-09-23 오전 8 10 34" src="https://user-images.githubusercontent.com/111875357/191866979-e9d02a32-5144-4f6c-bfdb-ee2fc154c16c.png">

### UIDocumentBrowserViewController
- Starting point of your app, Best Practice is to make it the rootViewController
- Full screen , 풀 스크린으로 실행될 수 있음 그러나 여전히 앱의 시작점을 의미함
- Open and organize your documents
- All the features of the Files App
- Can be customized
- Present your own UI on top
<img width="1086" alt="스크린샷 2022-09-23 오전 8 25 20" src="https://user-images.githubusercontent.com/111875357/191868297-58e3e0cd-228d-4d57-b6b0-b230b856d57c.png">

### UIDocumentPickerViewController (mail에서 사용되는것)
- Access files in the cloud(.open)
- Move files to the cloud(.moveToService)
- Copy from/to cloud(.import, .exportToService)
- Example code
Acces a Video from the Cloud

Create a UIDocumentPickerViewController and present it
```swift
let picker = UIDocumentPickerViewController(documentTypes: [kUTTypeVideo as String], in: .open)

picker.delegate = self
self. present(picker, animated: true)
```
Get the selected file URL
```swift
override func documentPicker(_ controller: UIDocumentPickerViewController, didPickDocumentsAt urls: [URL] { 
                // user the retrieved URLS
}
```

## Document Types
애플리케이션이 처리하는 방법을 알고 있는 파일을 시스템에 알려준다.

파일 앱에서 파일을 탭하면 iOS에서 앱을 열 수 있기 때문에 중요하다.

### 2 Steps
- Declaring the type if it isn`t already declared by iOS
- Claiming that tyou can view or edit files of this type

### Declaring a Type
- More Detail

<img width="1092" alt="스크린샷 2022-09-23 오전 8 39 44" src="https://user-images.githubusercontent.com/111875357/191869477-35602666-3351-4963-87db-5932785a8458.png">

### Declaring a New File Type
- My type conforms to public.data, public.content

<img width="654" alt="스크린샷 2022-09-23 오전 8 44 46" src="https://user-images.githubusercontent.com/111875357/191869887-ed900257-7329-4725-aa08-8e46ce0e66b6.png">

### Type Conformance

<img width="649" alt="스크린샷 2022-09-23 오전 8 47 33" src="https://user-images.githubusercontent.com/111875357/191870134-2f5f801e-8da7-49af-b0d7-9e088cb24532.png">

### Claiming Support for a Type

<img width="651" alt="스크린샷 2022-09-23 오전 8 49 05" src="https://user-images.githubusercontent.com/111875357/191870203-1854e4af-c81e-42f1-9eaf-5a2ecb326143.png">

### What Can YOu Do?
- Use a Document Browser or Document Picker to access documents
- Your customers can access their favorite cloud vender
- Consider using UIDocumentBrowserViewController instead of your custom browser
- Configure the Document Types supported by your app in Xcode (앱이 필요한 위치에 정확히 표시되고 고객이 찾을 수 있게 올바르게 구성해야한다.)

## Sandbox
외부로부터 들어온 프로그램이 보호된 영역에서 동작해 시스템이 부정하게 조작되는 것을 막는 보안 형태이다. '보안' (Alert 창)
🔗 https://zeddios.tistory.com/432

## Docuemnt Browser ViewController 활용

🔗 https://medium.com/@esung/document-browser-viewcontroller-%EB%A5%BC-%ED%99%9C%EC%9A%A9%ED%95%98%EC%97%AC-ios%EC%97%90%EC%84%9C-%ED%8C%8C%EC%9D%BC%ED%83%90%EC%83%89-%ED%95%98%EB%8A%94-%EB%B2%95-4dd43193c724

<img width="1375" alt="스크린샷 2022-09-22 오전 8 45 41" src="https://user-images.githubusercontent.com/111875357/191629057-af953447-9c76-4c45-afbb-9e6d9141ebdb.png">

