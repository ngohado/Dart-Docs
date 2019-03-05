## Variable và kiểu dữ liệu trong Dart

### Variable

Đây là đoạn code ví dụ về cách khai báo và khởi tạo một biến trong Dart:

```
var s1 = "hello world";
String s2 = "hi moon";
```

Biến là nơi lưu một reference(tham chiếu) đến một đối tượng. Trong trường hợp ở trên, biến s1 và biến s2 lưu một reference đến một đối tượng kiểu String và đối tượng đó có giá trị tương ứng là "hello world" và "hi moon". Trong Dart, ta có thể xác định rõ kiểu của biến hoặc để Dart tự suy ra dựa vào dữ liệu gán cho biến đó. Nếu bạn không muốn cố định là một kiểu dữ liệu nào, hãy sử dụng kiểu dữ liệu (Object)[] hoặc từ khóa [dynamic]().

```
dynamic s = "Voilà";
```

#### Giá trị mặc định

Tất cả các biến khi chưa được khởi tạo đều có giá trị ban đầu là `null`, kể cả các biến kiểu số. Đó là bởi vì số cũng như tất các các kiểu dữ liệu khác, đều là một object trong Dart.

```
int number;
print(number == null); //true
```
#### Final và const

Để đánh dẫu một biến là hằng số trong Dart, ta sử dụng `final` hoặc `const`. Tuy nhiên, 2 khái niệm này không giống nhau. Ta có thể hiểu như sau:

* `final` là những một biến mà giá trị của biến đó chỉ được gán 1 lần duy nhất. Tuy nhiên, nếu biến đó là đối tượng và chứa các đối tượng khác ở bên trong, ta vẫn có thể thay đổi giá trị của các biến ở bên trong.

```
final number = 4;
number = 3; //compile-error

final a = [1, 2 ,3];
a[0] = 0; // ok
```

Với một biến `final` có kiểu object, biến này phải được khởi tạo ngay khi khai báo.

* `const` là những biến được có giá trị được xác định khi biên dịch (compile-time constant). Bởi vậy, giá trị của biến sẽ được đóng băng và không thể thay đổi. Cùng với đó, vì giá trị của biến được xác định khi biên dịch, do đó giá trị của biến không thể là một object mà chỉ có thể là một số, một giá trị String hoặc kết quả của một biểu thức toán học. Một biến muốn được khai báo là `const` thì buộc phải là `static` (đối với biến nằm trong class) hoặc là biến `top-level`.

```
const c = 3; // ok

const bar = 1000000; // Unit of pressure (dynes/cm2)
const double atm = 1.01325 * bar; // Standard atmosphere

class Constant{
    static const g = 9.8;
}

const d = new Constant(); //compile-error
```

Ngoài việc khai báo một biến là hằng số, ta có thể dùng `const` để khai báo cho dữ liệu truyền vào một biến.

```
var a = const [];  // (1) a có thể được đổi thành giá trị khác.
a = [0, 1, 2];  // ok

final b = const [];  // (2) b chính là const chứ còn gì nữa
b = [3, 4, 5];  // compile error

const c = const [];  // (3) c được khuyến cáo là viết thừa
c = [7, 8, 9];  // compile error
```

### Kiểu dữ liệu

Dart có những kiểu dữ liệu sau

* numbers
* strings
* booleans
* lists (also known as arrays)
* sets
* maps
* runes (for expressing Unicode characters in a string)
* symbol

Bạn có thể khởi tạo một object của mỗi kiểu dữ liệu trên bằng cách gán cho chúng một giá trị. VD: "hello word", 4... Ngoài ra, vì mọi biến trong Dart đều tham chiếu đến một object, bạn cũng có thể dùng constructor để khởi tạo biến.

#### Numbers

Kiểu số trong Dart có thể thuộc 2 kiểu dữ liệu con:

*int*
Kiểu dữ liệu số nguyên với độ rộng tối đa là 64 bit và tùy thuộc vào platform. Với máy ảo Dart (Dart VM), giá trị của kiểu `int` có thể nằm trong khoảng -2^63 đến 2^63 - 1.

*double*
