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
