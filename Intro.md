## Intro

### Một chương trình Dart cơ bản

Đoạn code sau sử dụng một số features cơ bản nhất của Dart:

```
    // This is a comment
    void printInteger(int aNumber) {
      print('The number is $aNumber.');
    }

    // This is where the app starts executing.
    void main() {
      var number = 42;
      printInteger(number);
    }
```

Những định nghĩa có trong đoạn code trên là:

*// This is a comment*

Comment gồm 1 dòng. Dart cũng có support comment gồm nhiều dòng hoặc document comments. Xem thêm về [Comments]()


*int*

Một kiểu dữ liệu trong Dart. Một số kiểu dữ liệu khác: [String](), [List]()... Xem thêm về [Kiểu dữ liệu]()


*42*

Một giá trị kiểu số. Các giá trị số là một loại của compile-time constant.


*print()*

Một function nhanh gọn để hiển thị output ra màn hình console.


*'...' hoặc "..."*

Một giá trị kiểu [String]()


*$variableName hoặc ${expression}*

Chèn một giá trị của biến vào một giá trị String. Xem thêm về [String]().


*main()*

Một function bắt buộc của bất kỳ một chương trình Dart nào. Đây là function sẽ được gọi đầu tiên trong chương trình (Đầu vào của một chương trình).


*var*

Một cách để khai báo biến mà không cần xác định rõ kiểu của biến là gì. Xem thêm [Variables]().


> **Note:** Những đoạn code trong docs này đều tuân theo [Dart style guide]()

### Các khái niệm quan trọng

Đây là những khái niệm quan trọng mà bạn cần phải nhớ khi học Dart:

* Mọi thứ mà bạn có thể gán cho một biến đều là *object* và mỗi *object* là một thể hiện của một *class*. Một số, một function, hay [null]() đều là một *object*. Tất cả các *object* đều kế thừa từ class [Object]().

* Dart là một ngôn ngữ todo, tuy nhiên kiểu dữ liệu khi khai báo có thể có hoặc không vì Dart có thể tự suy ra kiểu của biến dựa vào giá trị của biến đó. Ví dụ: trong đoạn code phía trên, biến *number* có thể được suy ra là kiểu dữ liệu [int](). Khi bạn cố ý không muốn xác định kiểu dữ liệu của một biến là gì, hãy sử dụng một kiểu dữ liệu đặc biết là [dynamic]().

* Dart có support [Generic]. Ví dụ: `List<int>` (một list gồm các giá trị kiểu int) hoặc `List<dynamic>` (một list gồm bất kỳ một kiểu giá trị nào)

* Dart support *top-level functions* - các function mà không cần phải khai báo trong một class nào cả (vd: [main()]()), hoặc các function mà được khai báo bên trong một class: *instance method* hoặc *static method*. Ngoài ra, bạn có thể khai báo một function bên trong một function khác (nested function hoặc local function).

* Tương tự như ý trên, Dart support *top-level variables* cũng như các biến được khai báo bên trong một class: *instance variables* hoặc *static variables*. *Instance variables* còn được gọi với tên khác như *field* hoặc *property*.

* Không giống như Java, Dart không có các *visibility modifier* như `public`, `protected`, `private` hay `default`. Thay vào đó, Dart phân biệt một biến là local dựa vào quy tắc đặt tên: tên biến bắt đầu bằng ký tự gạch dưới `_` thì todo

* Tên biến có thể bắt đầu bằng ký tự gạch dưới `_` và theo sau bởi các chữ hoặc số

* Dart có cả expression(biểu thức) và statement(câu lệnh). Ví dụ: biểu thức điều kiện `condition ? expr1 : expr2` sẽ trả về giá trị của biểu thức `expr1` hoặc `expr2`. Chúng ta có thể so sánh biểu thức trên với câu lệnh [if-else](https://www.dartlang.org/guides/language/language-tour#if-and-else) khi nó không trả về một giá trị nào. Ngoài ra, một câu lệnh sẽ gồm 1 hoặc nhiều biểu thức. Tuy nhiên, biểu thức thì không thể chứa trực tiếp một câu lệnh.

* Các chương trình viết bằng Dart có thể gặp 2 loại vấn đề: warnings và errors. Các warning thể hiện cho bạn code của bạn có thể sẽ không chạy, tuy nhiên, nó không ngăn bạn chạy chương trình. Đối với error, ta sẽ gặp 2 loại error là compile-time error (lỗi xảy ra khi biên dịch) hoặc run-time (lỗi xảy ra khi chạy chương trình). Compile-time error sẽ ngăn bạn chạy chương trình. Còn run-time error sẽ bắn ra những [exception](https://www.dartlang.org/guides/language/language-tour#exceptions) trong quá trình chạy chương trình, những run-time error này có thể làm chương trình của bạn bị dừng lại.
