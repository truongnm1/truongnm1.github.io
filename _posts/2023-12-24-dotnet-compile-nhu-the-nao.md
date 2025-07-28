---
title: .NET Compile Như Thế Nào?
date: 2023-12-24 12:00:00 +0700
categories: [How it works, .NET framework]
tags: [.net, compilation, c#]     # TAG names should always be lowercase
---

Các ngôn ngữ thuộc .NET framework như C#, VB,..khi được compile sẽ tạo ra **ngôn ngữ trung gian** (MSIL – Microsft Intermediate Language). Ngôn ngữ này sau đó sẽ được runtime environment của .NET (Common Language Runtime) dịch về mã máy.

Ngôn ngữ trung gian hay CIL (MSIL) là một tập chỉ thị không phụ thuộc vào CPU được biên dịch từ source code, nó chứa các chỉ thị như lưu trữ, khởi tạo, gọi hàm và các phép tính, truy cập bộ nhớ. Một trong những ưu điểm của ngôn ngữ trung gian là cross-platform ( đa nền tảng ) vì sẽ được CLR dịch sang mã máy phù hợp với kiến trúc của máy đó. 

Đây cũng coi như một thế mạnh của CLR. Ngoài ra, những ngôn ngữ khác nhau thuộc .NET có thể kết hợp với nhau tốt vì chúng đều được biên dịch sang MSIL và cấu hình về CLR giống nhau trước khi đưa vào runtime.

Chi tiết chu trình biên dịch của .NET :
## Bước 1 : Source code -> MSIL
Source code được biên dịch thành ngôn ngữ trung gian. Ngoài ra, compiler còn phải gửi thêm đó là Metadata gồm các thông tin mô tả về types, các hàm, parameters, kiểu trả về,..và những thông tin cần thiết khác cho CLR. MSIL và Metadata của source code sau cùng được lưu vào trong file PE ( các file .exe hay .dll ) hay còn được gọi là .NET assembly.
## Bước 2 : MSIL -> Native code (Mã máy)
CLR phân tích những thông tin từ các header của file PE để quyết định tạo process phù hợp, đưa vào bộ nhớ và lấy thông tin về entry point của chương trình. Sau đó, một trong những thành phần của CLR là JIT Compiler sẽ đảm nhiệm việc dịch các dòng MSIL sang mã máy phù hợp với kiến trúc của máy host và đưa vào bộ nhớ, JIT sẽ không dịch toàn bộ mà chỉ dịch những dòng có sử dụng đến.

Đầu tiên, từ entry point của cả chương trình ( hàm main ), JIT sẽ bắt đầu tìm đến MSIL ( lấy từ các thư viện liên kết động – dll ) của hàm được gọi và lấy metadata của nó, sau đó tạo một khoảng trống trong bộ nhớ và dịch đoạn MSIL đó sang mã máy và để trong bộ nhớ đó và thực thi ( execute ) đồng thời thay đổi entry point của hàm thành địa chỉ của cùng bộ nhớ để khi sau này khi hàm này được gọi lần nữa, JIT không cần phải dịch lại, thay vào đó sẽ được tham chiếu thẳng đến bộ nhớ đã có sẵn mã máy. 

![Compilation steps](/assets/img/2023-12-24-dotnet-compile-nhu-the-nao/dotnet-compilation-steps.png)

## Tài liệu tham khảo:
[https://dev.to/kcrnac/net-execution-process-explained-c-1b7a](https://dev.to/kcrnac/net-execution-process-explained-c-1b7a)
<br>
[https://learn.microsoft.com/en-us/dotnet/standard/clr](https://learn.microsoft.com/en-us/dotnet/standard/clr)
<br>
[https://learn.microsoft.com/en-us/dotnet/standard/managed-execution-process](https://learn.microsoft.com/en-us/dotnet/standard/managed-execution-process)
