
Part 2:
## Functions as first-class objects
Bạn có thể truyền 1 function như 1 parameter của 1 function khác:
```
void printElement(int element) {
  print(element);
}

var list = [1, 2, 3];

// Pass printElement as a parameter.
list.forEach(printElement);
```
Bạn cũng có thể gán 1 function cho 1 variable:
```
var loudify = (msg) => '!!! ${msg.toUpperCase()} !!!';
assert(loudify('hello') == '!!! HELLO !!!');
```
Ở ví dụ trên, chúng ta đã sử dụng anonymous function. Chúng ta cùng tìm hiểu xem nó là gì nhé.

## Anonymous functions
Hầu hết các function đều có tên, như `main()` hoặc `printElement()`. Bạn cũng có thể tạo những function "vô danh" hay còn gọi là _anonymous function_, hoặc _lambda_(với anh em Java hay Kotlin có vẻ sẽ hay dùng từ này) hoặc _closure_(anh em Swift thì có thể sẽ quen với từ này). Bạn có thể gán nó cho 1 variable hay có thể add hay remove khỏi một collection như một element bình thường.

Anonymous function nhìn có vẻ giống như một function bình thường, chỉ khác là nó không có tên:
```
([[Type] param1[, …]]) {
  codeBlock;
};
```
Ví dụ ở dưới, chúng ta sẽ tạo một anonymous function với parameter là `item` và không xác định type cho nó. Chúng ta truyền anonymous function cho function `forEach`, và anonymous function được gọi bên trong function `forEach`:
```
var list = ['apples', 'bananas', 'oranges'];
list.forEach((item) {
  print('${list.indexOf(item)}: $item');
});
```
Kết quả:
```
0: apples
1: bananas
2: oranges
```
Nếu như function body chỉ chứa 1 statement, bạn có thể sử dụng `=>` để rút ngắn code:
```
list.forEach(
    (item) => print('${list.indexOf(item)}: $item'));
```

## Lexical scope
>Dart is a lexically scoped language

Nghĩa là "scope" phạm vi của một variable được xác định tĩnh, dựa trên "layout" cấu trúc của code.
```
bool topLevel = true;

void main() {
  var insideMain = true;

  void myFunction() {
    var insideFunction = true;

    void nestedFunction() {
      var insideNestedFunction = true;

      assert(topLevel);
      assert(insideMain);
      assert(insideFunction);
      assert(insideNestedFunction);
    }
  }
}
```
Function `nestedFunction()` có thể sử dụng những variable ở các level trên và ngoài nó.

## Lexical closures
```
/// Returns a function that adds [addBy] to the
/// function's argument.
Function makeAdder(num addBy) {
  return (num i) => addBy + i;
}

void main() {
  // Create a function that adds 2.
  var add2 = makeAdder(2);

  // Create a function that adds 4.
  var add4 = makeAdder(4);

  assert(add2(3) == 5);
  assert(add4(3) == 7);
}
```
Function `makeAdder` giữ lại variable `addby`. Kể cả khi function kết thúc, nó vẫn giữ lại variable `addBy`.

## Return values
```
foo() {}

assert(foo() == null);
```

Tất cả các function đều trả ra giá trị. Nếu bạn không xác định giá trị return, hoặc không return ra giá trị nào trong body. Giá trị mặc định trả ra mặc định của function là `null`.

## Operators
Dart hỗ trợ rất nhiều operator từ cơ bản đến một số operator mới. Bạn có thể override lại khá nhiều operator tùy vào mục đích của bạn. Dưới đây là bảng operator được hỗ trợ bởi Dart: [Operators Table](https://www.dartlang.org/guides/language/language-tour#operators)

## Arithmetic operators
Dart hỗ trợ một số operator toán học:[Arithmetic operators table](https://www.dartlang.org/guides/language/language-tour#arithmetic-operators)

Mình sẽ giải trích dẫn một số operator có thể mới mẻ với mọi người:
* `~/`: Chia 2 số và trả về kết quả là số nguyên. `assert(5 ~/ 2 == 2); // Result is an int`

## Equality and relational operators
Một số operator so sánh hơn, bằng: [Equality and relational operators table](https://www.dartlang.org/guides/language/language-tour#equality-and-relational-operators).

## Type test operators
Chúng ta sử `as`, `is`, và `is!` operator để kiểm tra type lúc runtime.

| Operator| Ý nghĩa       |
| --------|:-------------:|
| as      | Operator dùng để ép kiểu |
| is      | Return True nếu type checking là đúng     |
| is!     | Return False nếu type checking là sai      |
Hãy cùng nhìn đoạn code ở dưới đây:
```
if (emp is Person) {
  // Type check
  emp.firstName = 'Bob';
}
```
Ở trong Kotlin họ gọi đây là _smart cast_ vì variable `emp` được kiểm tra bằng operator `is` với `Person`, nếu True thì statement ở dưới, variable `emp` tự động được hiểu là `Person` luôn.

Bạn có thể dùng operator `as` như sau:
```
(emp as Person).firstName = 'Bob';
```
>**Note:** 2 đoạn code trên không tương đương nhé. Nếu trong trường hợp `emp` là `null` hoặc không phải là `Person`, example đầu tiên sẽ không có vấn đề gì xảy ra vì nó trả ra False, còn với example 2 sẽ throw ra exception.

## Assignment operators
```
// Assign value to a
a = value;
// Assign value to b if b is null; otherwise, b stays the same
b ??= value;
```
Bình thường bạn có thể dùng operator `=` để gán 1 giá trị, vậy chuyện gì sẽ ra khi giá trị gán là null và bạn không muốn điều đó xảy ra. Đoạn code trên giải quyết vấn đề đó một cách ngắn gọn với operator `??=`. Chỉ khi `value` không `null`, thì `value` mới được gán cho `b`.

Anh em tham khảo thêm một số assignment operator ở đây: [Assignment operators table](https://www.dartlang.org/guides/language/language-tour#assignment-operators).

## Conditional expressions
Dart hỗ trợ 2 operator giúp bạn thực hiện code nhanh hơn tương tự với `if-else`:
```
condition ? expr1 : expr2
```
Cái này có vẻ quá quen thuộc rồi nên mình sẽ không nói nữa.

```
expr1 ?? expr2
```
Với operator này, nếu _expr1_ không null, sẽ return giá trị của nó, nếu không sẽ return giá trị của _expr2_

Ví dụ:
```
var visibility = isPublic ? 'public' : 'private';

String playerName(String name) => name ?? 'Guest';
```

## Cascade notation (..)
`..` cho phép bạn thực hiện một loạt các operation trên cùng 1 object.
Nếu không dùng cascade:
```
var button = querySelector('#confirm');
button.text = 'Confirm';
button.classes.add('important');
button.onClick.listen((e) => window.alert('Confirmed!'));
```
Sau khi dùng cascade:
```
querySelector('#confirm') // Get an object.
  ..text = 'Confirm' // Use its members.
  ..classes.add('important')
  ..onClick.listen((e) => window.alert('Confirmed!'));
```
>**Note:** "double dot" `..` không phải là operator. Nó là một syntax của Dart.

## Safe call
Lý do mình gọi nó là "safe call" vì  hẳn trong chúng ta đã đối mặt rất nhiều với `NullPointerException`. Lý do là chúng ta không check `null` trước khi gọi một object, thực sự thì nó rất rườm rà `if not nul...`. Do đó Dart cung cấp cho chúng ta một operator để làm việc đó dễ dàng hơn: `?.`
```
var a = foo?.bar()
```
Nếu `foo` là null, function `bar()` sẽ không được gọi và `a` sẽ bằng `null`.
