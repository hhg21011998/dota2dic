# Dota 2 Dictionary
Ứng dụng dành cho mục đích tìm kiếm nhanh thông tin về những vị tướng và các trang bị trong Dota 2.
Ứng dụng bao gồm 4 màn hình dành cho các nội dung về:
 - Các bản cập mới
 - Thông tin chi tiết về các vị tướng
 - Thông tin chi tiết về các trang bị
 - Đăng nhập, đăng ký và hiển thị các vị tướng yêu thích

<img src="https://github.com/hhg21011998plus/dota2dic/blob/master/Files/gif1.gif" width="25%" height="25%"> | <img src="https://github.com/hhg21011998plus/dota2dic/blob/master/Files/gif2.gif" width="25%" height="25%"> | <img src="https://github.com/hhg21011998plus/dota2dic/blob/master/Files/gif3.gif" width="25%" height="25%"> | <img src="https://github.com/hhg21011998plus/dota2dic/blob/master/Files/gif4.gif" width="25%" height="25%"> 

## RxSwift: Reactive Programing
### 1. Everything is a sequence.
> Sequence như là một mảng bất đồng bộ, các phần tử của nó không tồn tại cùng 1 thời điểm, giống như các hành động của user, không đoán trước được. Và RxSwift cung cấp cho ta một listener để lắng nghe và quan sát lúc nào phần tử được phát ra, cũng như bất cứ khi nào người dùng tương tác với ứng dụng; từ đó ta có thể react lại các sự kiện đó và thực hiện những hành động tương ứng để phản hồi lại người dùng.
### 2. RxSwift sử dụng higher order function
### 3. Phù hợp với mô hình MVVM
> Trong mô hình MVVM, View và Model không ràng buộc chặt với nhau mà được "bind" với nhau, nghĩa là thay đổi ở Model sẽ được cập nhật ở View và ngược lại.
> Và với RxSwift và RxCocoa ta có thể dễ dàng bind ViewModel với View nhờ toán tử .bind(to:)

## Clean Architecture MVVM (Sergdort)
### 1. High level overview

<img src="https://raw.githubusercontent.com/sergdort/CleanArchitectureRxSwift/master/Architecture/Modules.png" width="50%" height="50%"> 

Chia làm 3 folder chính: Mỗi folder sẽ chứa các file xử lý nhiệm vụ riêng biệt:

`Domain` bao gồm các file Model để truy xuất dữ liệu từ API và các file UseCaseDomain dùng để khởi tạo các protocol cần thiết cho mỗi screen. Không phụ thuộc vào bất cứ thành phần nào của UI.

`Platform` bao gồm các file dùng để phân tích API và các file UseCasePlatform thực thi các protocol được khởi tạo từ Domain. Làm việc trực tiếp với database tại folder này.

`Application` bao gồm các file View và ViewModel. Là tầng chịu trách nhiệm cung cấp thông tin từ ứng dụng cho user và tiếp nhận những input từ user cho ứng dụng.

<img src="https://raw.githubusercontent.com/sergdort/CleanArchitectureRxSwift/master/Architecture/MVVMPattern.png" width="50%" height="50%">

### 2. Tất cả ViewModel đều phải tuân thủ protocol ViewModelType
```swift
protocol ViewModelType {
    associatedtype Input
    associatedtype Output
    
    func transform(input: Input) -> Output
}
```
- Input là cái mình nhập vào, tác động vào (tap button, edit textfield, ...)
- Output là cái mà sẽ thay đổi dựa trên input (như label, button, ...)
- Nguyên tắc áp dụng:
Bên ViewController có bao nhiêu input thì bên ViewModel phải khai báo bấy nhiêu observable tương ứng.
ViewModel sẽ nhận tín hiệu của input từ ViewController (như tap button, edit textfield, …).
ViewModel sau khi nhận tín hiệu sẽ xử lý data đó theo yêu cầu thông qua Platform rồi gửi kết quả cuối cùng cho ViewController bằng cách phát ra các Observable tương ứng.
Output ở ViewController sẽ subscribe các observable mà ViewModel cung cấp.

### 3. Ưu nhược điểm của mô hình này
Về mặt ưu điểm, Clean architecture đạt được:
- Giúp logic nghiệp vụ trở nên rõ ràng.
- Không phụ thuộc vào framework
- Các thành phần UI hoàn toàn tách biệt và độc lập.
- Dễ dàng kiểm thử.
Về mặt nhược điểm:
- Clean architecture do phân tách cấu trúc thành nhiều tầng nên dẫn đến việc số lượng code sinh ra là rất lớn.

## Cấu trúc file
```
- /Dota2Dictionary
	-/AppDelegate
	-/Resource
	-/Utility
	-/Application
		- Application.swift
		-/Scene
			-/Patch
				- PatchNavigator.swift
				- PatchViewController
				-/ViewModel
				-/View
			-/PatchDetail	
			-/Hero
			-/HeroDetail
…			
	-/Platform
		-/Network
		-/UseCase
	-/Domain
		-/Entities
		-/UseCase
```

## C 
