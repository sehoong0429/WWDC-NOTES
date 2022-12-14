

π WWDC18 | Category : SwiftUI & UI Frameworks

Managing Documents In Your iOS Apps
---
π https://developer.apple.com/videos/play/wwdc2018/216/

λ¬Έμ κ΄λ¦¬

iOS μ±μμ λ¬Έμλ₯Ό ν¨κ³Όμ μΌλ‘ κ΄λ¦¬νλ λ°©λ²κ³Ό Documents Pickerμ Documents browserμ μ°¨μ΄μ κ³Ό μ¬μ© μκΈ°μ κ΄ν λ΄μ©λ€μ΄λ€. ν λ²λ μ μ¨λ³Έ λ΄μ©μ΄κΈ°μ μ²μ λ€μλ μ΄ν΄ νκΈ° μ½μ§ μμλ€.

## Document Management on iOS
#### What is it?
- API for application developers
- File provider API for cloud vendors
- Files app

UIDocumentBrowserViewController (iOS 11)

UIDocumentPickerViewController (κ°μ )

κ³ κ°μ΄ μ νΈνλ λͺ¨λ  ν΄λΌμ°λ κ³΅κΈμμ²΄μ νμΌμ κ΄λ¦¬νκ³  νμν  μ μλ€.

#### Client API
- Document Browser (UIDocumentBrowserViewController)
- Document Picker (UIDocumentPickerViewController)
- File Coordination (NSFileCoordinator, UIDocument)
- File Operations (NSFileManager)
- Building Great Document=based Apps in iOS 11 (WWDC 2017)

#### File Provider API
- File Provider Extension -> λ‘κ·ΈμΈ νλ©΄μ ν¬ν¨ν μ¬μ©μ μ μ UI μμ μμ± κ°λ₯ (NSFileProviderExtension)
- File Provider Custom Actions (FPUIActionextensionViewController)
- File Provider Enhancements (WWDC 2017)

νμ€νΈλ₯Ό μ€ννκ³  νμΌ μ κ³΅μ, νμ₯μμ λν λ¬Έμ λ₯Ό λ³΄μ¬μ£Όκ³  λ¬Έμ λ₯Ό ν΄κ²°νλλ‘ μλ΄νλ€.
<img width="1163" alt="αα³αα³αα΅α«αα£αΊ 2022-09-23 αα©αα₯α« 7 58 02" src="https://user-images.githubusercontent.com/111875357/191865664-5cccb862-f918-46bd-83c6-eab6cc8d3323.png">

<img width="1141" alt="αα³αα³αα΅α«αα£αΊ 2022-09-23 αα©αα₯α« 8 03 46" src="https://user-images.githubusercontent.com/111875357/191866317-f52b5958-ee17-4ab4-9f86-652ec9ae1ee8.png">

### Siri Shourcuts
- μ΄λ¦¬κ±°λ μ΅κ·Όμ μμ±λμ΄ μ¬μ©ν λ¬Έμλ₯Ό νμνκ³  κ²μμ΄λ μ κΈνλ©΄μμ λ³Ό μ μλλ‘ νλ€.
<img width="1137" alt="αα³αα³αα΅α«αα£αΊ 2022-09-23 αα©αα₯α« 8 05 22" src="https://user-images.githubusercontent.com/111875357/191866535-eba5ae55-fb9e-47da-84ee-5db5a79f8d2d.png">

<img width="1152" alt="αα³αα³αα΅α«αα£αΊ 2022-09-23 αα©αα₯α« 8 05 31" src="https://user-images.githubusercontent.com/111875357/191866542-ef730e3d-2da8-4e7c-bae8-123aff799fa7.png">

<img width="1159" alt="αα³αα³αα΅α«αα£αΊ 2022-09-23 αα©αα₯α« 8 05 45" src="https://user-images.githubusercontent.com/111875357/191867799-6447a41b-9c6d-4b94-b3b4-7237e62aa9ee.png">


## Document Picker vs Document Broswer

<img width="1153" alt="αα³αα³αα΅α«αα£αΊ 2022-09-23 αα©αα₯α« 8 10 34" src="https://user-images.githubusercontent.com/111875357/191866979-e9d02a32-5144-4f6c-bfdb-ee2fc154c16c.png">

### UIDocumentBrowserViewController
- Starting point of your app, Best Practice is to make it the rootViewController
- Full screen , ν μ€ν¬λ¦°μΌλ‘ μ€νλ  μ μμ κ·Έλ¬λ μ¬μ ν μ±μ μμμ μ μλ―Έν¨
- Open and organize your documents
- All the features of the Files App
- Can be customized
- Present your own UI on top
<img width="1086" alt="αα³αα³αα΅α«αα£αΊ 2022-09-23 αα©αα₯α« 8 25 20" src="https://user-images.githubusercontent.com/111875357/191868297-58e3e0cd-228d-4d57-b6b0-b230b856d57c.png">

### UIDocumentPickerViewController (mailμμ μ¬μ©λλκ²)
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
μ νλ¦¬μΌμ΄μμ΄ μ²λ¦¬νλ λ°©λ²μ μκ³  μλ νμΌμ μμ€νμ μλ €μ€λ€.

νμΌ μ±μμ νμΌμ ν­νλ©΄ iOSμμ μ±μ μ΄ μ μκΈ° λλ¬Έμ μ€μνλ€.

### 2 Steps
- Declaring the type if it isn`t already declared by iOS
- Claiming that tyou can view or edit files of this type

### Declaring a Type
- More Detail

<img width="1092" alt="αα³αα³αα΅α«αα£αΊ 2022-09-23 αα©αα₯α« 8 39 44" src="https://user-images.githubusercontent.com/111875357/191869477-35602666-3351-4963-87db-5932785a8458.png">

### Declaring a New File Type
- My type conforms to public.data, public.content

<img width="654" alt="αα³αα³αα΅α«αα£αΊ 2022-09-23 αα©αα₯α« 8 44 46" src="https://user-images.githubusercontent.com/111875357/191869887-ed900257-7329-4725-aa08-8e46ce0e66b6.png">

### Type Conformance

<img width="649" alt="αα³αα³αα΅α«αα£αΊ 2022-09-23 αα©αα₯α« 8 47 33" src="https://user-images.githubusercontent.com/111875357/191870134-2f5f801e-8da7-49af-b0d7-9e088cb24532.png">

### Claiming Support for a Type

<img width="651" alt="αα³αα³αα΅α«αα£αΊ 2022-09-23 αα©αα₯α« 8 49 05" src="https://user-images.githubusercontent.com/111875357/191870203-1854e4af-c81e-42f1-9eaf-5a2ecb326143.png">

### What Can YOu Do?
- Use a Document Browser or Document Picker to access documents
- Your customers can access their favorite cloud vender
- Consider using UIDocumentBrowserViewController instead of your custom browser
- Configure the Document Types supported by your app in Xcode (μ±μ΄ νμν μμΉμ μ νν νμλκ³  κ³ κ°μ΄ μ°Ύμ μ μκ² μ¬λ°λ₯΄κ² κ΅¬μ±ν΄μΌνλ€.)

## Sandbox
μΈλΆλ‘λΆν° λ€μ΄μ¨ νλ‘κ·Έλ¨μ΄ λ³΄νΈλ μμ­μμ λμν΄ μμ€νμ΄ λΆμ νκ² μ‘°μλλ κ²μ λ§λ λ³΄μ ννμ΄λ€. 'λ³΄μ' (Alert μ°½)
π https://zeddios.tistory.com/432

## Docuemnt Browser ViewController νμ©

π https://medium.com/@esung/document-browser-viewcontroller-%EB%A5%BC-%ED%99%9C%EC%9A%A9%ED%95%98%EC%97%AC-ios%EC%97%90%EC%84%9C-%ED%8C%8C%EC%9D%BC%ED%83%90%EC%83%89-%ED%95%98%EB%8A%94-%EB%B2%95-4dd43193c724

<img width="1375" alt="αα³αα³αα΅α«αα£αΊ 2022-09-22 αα©αα₯α« 8 45 41" src="https://user-images.githubusercontent.com/111875357/191629057-af953447-9c76-4c45-afbb-9e6d9141ebdb.png">

