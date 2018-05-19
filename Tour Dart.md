# Mở đầu
Hi anh em! Tiếp tục sau vụ dịch [tài liệu Kotlin](https://github.com/ngohado/Kotlin-Docs) ngót cũng được một năm. Nay mình sẽ tiếp tục dịch docs của Dart, đây cũng là cơ hội để mình học và dấn thân vào Flutter. Mời anh em theo dõi series này nhé.

# A Tour of the Dart Language
Tour này sẽ tập trung vào những phần chính của Dart.

## A basic Dart program

Đoạn code dưới đây thể hiện tổng quan của ngôn ngữ Dart.

```
// Định nghĩa 1 hàm (function)
printInteger(int aNumber) {
  print('The number is $aNumber.'); // Print to console.
}

// Khi chương trình được excute, hàm main sẽ được thực thi đầu tiên
main() {
  var number = 42; // Khai báo và gán giá trị cho biến.
  printInteger(number); // Gọi hàm printInteger()
}
```
## Những concepts quan trọng
Nếu như bạn học Dart, hãy luôn ghi nhớ những khái niệm dưới đây:

* Do Dart là ngôn ngữ thuần OOP nên tất cả những thứ bạn gán cho biến đều là `object`, mọi `object` đều là `instance` (thể hiện) của một `class`. Kể cả số, method (hàm), và `null` cũng đều là `object`. Tất cả các `object` đều kế thừa từ [Object](https://api.dartlang.org/dev/2.0.0-dev.55.0/dart-core/Object-class.html) class.

* Kiểu type của 1 variable là `optional` bởi vì Dart có thể tự suy ra type dựa trên giá trị truyền vào cho biến. Ở đoạn code bên trên, biến `number` được hiểu là kiểu `int`. Khi bạn muốn khai báo 1 variable mà type của nó không được xác định, hãy sử dụng type [dynamic](https://www.dartlang.org/guides/language/effective-dart/design#do-annotate-with-object-instead-of-dynamic-to-indicate-any-object-is-allowed).


* Như các ngôn ngữ khác, Dart hỗ trợ `generic type`, ví dụ như `List<int>` (1 danh sách kiểu số nguyên) hoặc `List<dynamic>` (1 danh sách các `object` mà type không xác định, nó có thể chấp nhận mọi loại type).

* Dart hỗ trợ `top-level function` (giống như `main()`), đồng nghĩa bạn có thể sử dụng hàm đó ở bất cứ đâu mà không cần thông qua tên class hay bất kỳ instance của class nào cả. Bạn cũng có thể tạo một hàm bên trong một hàm (còn gọi là `nested function` hoặc `local function`).

* Tương tự Dart cũng hỗ trợ `top-level variable`.

* Không giống với Java, Dart không hỗ trợ `public`, `protected`, và `private`. Nếu như `identifier` (tên biến, hàm,...) bắt đâu vời dấu gạch dưới ( _ ) , thì nó `private` trong `library` của nó. Mỗi file `.dart` được coi là 1 `library`. Chi tiết [Libraries and visibility](https://www.dartlang.org/guides/language/language-tour#libraries-and-visibility) .

* `Identifier` có thể bắt đầu bằng một chữ cái hoặc dấu gạch dưới ( _ ).

* Sometimes it matters whether something is an expression or a statement, so it helps to be precise about those two words. (Đoạn này mình không hiểu lắm, anh em chia sẻ giúp)

* Dart tools có thể báo cho bạn 2 loại vấn đề: warnings và errors. Warnings là những dấu hiểu chỉ ra rằng code của bạn có thể không hoạt động, nhưng chương trình của bạn vẫn có thể chạy. Errors có thể là error lúc compile-time hoặc run-time. Error lúc compile-time hiển nhiên sẽ khiến code bạn không chạy được, còn kết quả của error run-time sẽ là những [exceptions](https://www.dartlang.org/guides/language/language-tour#exceptions) được throw ra khi chạy.

## Keywords

Sau đây là danh sách các keywords mà Dart sử dụng. Bạn không thể dụng những keyword này như một `identifier`. [Tham khảo link](https://www.dartlang.org/guides/language/language-tour#keywords).

## Variables

Dưới đây là đoạn code tạo một variable và khởi tạo giá trị ban đầu cho nó:

```
var name = 'Bob';
// name = 1; Compile lỗi, do name đã được định nghĩa là String sau khi được khởi tạo với giá trị 'Bob'
```

Variables lưu trữ `references` (tham chiếu). Biến trên gọi là `name` chứa tham chiếu đến `String` object và có giá trị là "Bob".

Kiểu của biến `name` được hiểu là `String`. Nếu bạn muốn biến đó không bị giới hạn một loại type, hãy dùng `Object` hoặc `dynamic`:

```
dynamic name = 'Bob';
name = 1; // Hoàn toàn oke.
```

## Giá trị mặc định (Default value)

Nếu 1 variable không được khởi tạo, thì giá trị mặc định của chúng là `null`. Ngay kể cả chúng là kiểu `int` thì nếu không tạo thì giá trị mặc định vẫn là `null`, vì mọi thứ trong Dart đều là object mà.

```
int lineCount;
assert(lineCount == null);
```

## Final và const

Nếu bạn không định thay đổi giá trị của một variable, hãy sử dụng `final` hoặc `const`, thay cho `var` hoặc đi kèm cùng các type khác như `int`, `String`,... Một biến `final` (final variable) chỉ được khởi tạo một lần duy nhất, một biến `const` (const variable) được khởi tạo lúc compile (const được ngầm hiểu là final). Những biến final ở top-level được khởi tạo lần đầu tiên khi chúng được sử dụng.

>**Note:** Instance variables can be `final` but not `const`. (Nghĩa là với các biến được khai báo như một property của 1 class thì có thể là `final`, còn `const` thì không)

Ví dụ về final variable:
```
final name = 'Bob'; // Không định nghĩa type biến
// name = 'Alice';  // Bỏ comment ra sẽ lỗi
final String nickname = 'Bobby';
```
Sử dụng `const` cho variable khi bạn muốn nó thành `compile-time constant`. Nếu khai báo const variable ở trong class, thay vì chỉ sử dụng `const`, bạn phải sử dụng `static const`. Khởi tạo một `const` variable với 1 số, hoặc 1 string, hoặc với một `const` variable khác, hoặc có thể là phép tính toán học:
```
const bar = 1000000; // Unit of pressure (dynes/cm2)
const double atm = 1.01325 * bar; // Standard atmosphere
```
`const` không chỉ khởi tạo 1 constant variable, mà nó cũng có thể sử dụng để tạo một constant _values_.
```
// Note: [] tạo một list rỗng.
// const [] tạo một list rỗng (Empty), và không thể thay đổi (Immutable) (EIL).
var foo = const []; // foo is currently an EIL.
final bar = const []; // bar will always be an EIL.
const baz = const []; // baz is a compile-time constant EIL.
```
Để dùng `const` tạo constant values, anh em có thể xem ở đây [Lists](https://www.dartlang.org/guides/language/language-tour#lists), [Maps](https://www.dartlang.org/guides/language/language-tour#maps), và [Classes](https://www.dartlang.org/guides/language/language-tour#classes).

## Built-in types

Dart hỗ trợ những loại dữ liệu sau đây:

* numbers
* strings
* booleans
* lists (cũng có thể coi như _arrays_)
* maps
* runers (dùng để hiện thị các ký hiệu Unicode trong string, kiểu như mấy emotion)
* symbols

Do tất cả các variable ở trong Dart đều được coi là object, bạn có thể sử dụng _constructors_ để khởi tạo variable. Có nhiều loại built-in type có constructor. Ví dụ như bạn có thể dụng constructor `Map()` để khởi tạo một map.

## Numbers

Các kiểu số trong Dart tồn tại dưới 2 dạng chính: [int](https://api.dartlang.org/dev/dart-core/int-class.html) và [double](https://api.dartlang.org/dev/dart-core/double-class.html).

Cả `int` và `double` đều là subtypes của [num](https://api.dartlang.org/dev/dart-core/num-class.html). Do chúng đều là object nên có khá nhiều method hỗ trợ như `abs()`, `ceil()` làm tròn lên, `floor()` làm tròn xuống. Nếu bạn muốn nhiều hơn [dart:math](https://api.dartlang.org/dev/dart-math) có thể giúp bạn.
```
int x = 1;
int hex = 0xDEADBEEF;

double y = 1.1;
double exponents = 1.42e5;
```

Dưới đây là cách bạn chuyển từ string sang số và ngược lại
```
// String -> int
var one = int.parse('1');
assert(one == 1);

// String -> double
var onePointOne = double.parse('1.1');
assert(onePointOne == 1.1);

// int -> String
String oneAsString = 1.toString();
assert(oneAsString == '1');

// double -> String
String piAsString = 3.14159.toStringAsFixed(2);
assert(piAsString == '3.14');
```

## Strings
```
var s1 = 'Single quotes work well for string literals.';
var s2 = "Double quotes work just as well.";
var s3 = 'It\'s easy to escape the string delimiter.';
var s4 = "It's even easier to use the other delimiter.";
```

Để tạo 1 string, bạn có thể dụng nháy đơn `'` hoặc nháy kéo `"`. Điểm mình rất thích đó là bạn có thể truyền value vào trong string rất đơn giản `$variable` hoặc `${expression}`:
```
var s = 'string interpolation';

assert('Dart has $s, which is very handy.' ==
    'Dart has string interpolation, ' +
        'which is very handy.');
assert('That deserves all caps. ' +
        '${s.toUpperCase()} is very handy!' ==
    'That deserves all caps. ' +
        'STRING INTERPOLATION is very handy!');
```

>**Note:** Bạn dùng `==` để so sánh xem 2 object có bằng nhau hay không. Với string thì 2 string bằng nhau khi các phần tử (unit) trong string giống nhau (string là một dãy các UTF-16 code unit).

Để tạo một `multi-line string`:
```
var s1 = '''
You can create
multi-line strings like this one.
''';

var s2 = """This is also a
multi-line string.""";
```

Bạn có thể tạo "raw" string bằng cách thêm đằng trước `r`:
```
var s = r"In a raw string, even \n isn't special.";
```
Raw string bạn có thể hiểu là nó sẽ hiển thị đúng như những gì bạn ghi lên, giả sử như đoạn code trên `\n` sẽ **không** được coi là xuống dòng nữa.
Anh em có thể tìm hiểu thêm về cách sử dụng strings ở đây: [Strings and regular expressions](https://www.dartlang.org/guides/libraries/library-tour#strings-and-regular-expressions).

## Lists
Collection phổ biến nhất trong hầu hết các ngôn ngữ đều là _array_. Trong Dart thì arrays là [Lists](https://api.dartlang.org/dev/dart-core/List-class.html) object.

List trong Dart nhìn có vẻ giống với array của JavaScript:
```
var list = [1, 2, 3];
```
>**Note:** identifier `list` được suy ra type là `List<int>`

Bạn cũng có thể tạo list như một `compile-time constant`:
```
var constantList = const [1, 2, 3];
// constantList[1] = 1; // Uncommenting this causes an error.
```
List có rất nhiều các method hỗ trợ. Anh em có thể tham khảo thêm ở đây: [Collections](https://www.dartlang.org/guides/libraries/library-tour#collections).

## Maps
Map là một object dạng giúp liên kết giữa `key` và `value`. Bạn có thể khởi tạo một map bằng map `literals` hoặc `Map` type.

Dưới đây là cách tạo map bằng map `literals`:
```
var gifts = {
  // Key:    Value
  'first': 'partridge',
  'second': 'turtledoves',
  'fifth': 'golden rings'
};

var nobleGases = {
  2: 'helium',
  10: 'neon',
  18: 'argon',
};
```

Hoặc tạo bằng constructor:
```
var gifts = new Map();
gifts['first'] = 'partridge';
gifts['second'] = 'turtledoves';
gifts['fifth'] = 'golden rings';

var nobleGases = new Map();
nobleGases[2] = 'helium';
nobleGases[10] = 'neon';
nobleGases[18] = 'argon';
```

Thêm một cặp key-value mới:
```
var gifts = {'first': 'partridge'};
gifts['fourth'] = 'calling birds'; // Add a key-value pair
```

Lấy giá trị từ map bằng key:
```
var gifts = {'first': 'partridge'};
assert(gifts['first'] == 'partridge');
```

Nếu key không tồn tại, giá trị trả ra là `null`:
```
var gifts = {'first': 'partridge'};
assert(gifts['fifth'] == null);
```

Sử dụng `.length` để lấy số cặp key-value trong map:
```
var gifts = {'first': 'partridge'};
gifts['fourth'] = 'calling birds';
assert(gifts.length == 2);
```

Bạn cũng có thể tạo map như một `compile-time constant`:
```
final constantMap = const {
  2: 'helium',
  10: 'neon',
  18: 'argon',
};

// constantMap[2] = 'Helium'; // Uncommenting this causes an error.
```

Map có rất nhiều các method hỗ trợ. Anh em có thể tham khảo thêm ở đây: [Maps](https://www.dartlang.org/guides/libraries/library-tour#maps)

## Functions

Như trong phần concepts đã nêu, `function` ũng là object và có type [Function](https://api.dartlang.org/dev/dart-core/Function-class.html). Có nghĩa là một function cũng có thể gán cho 1 variable và truyền nó cho một function khác như một 1 argument.

Dưới đây là cách implement 1 function:
```
bool isNoble(int atomicNumber) {
  return _nobleGases[atomicNumber] != null;
}
```
Bạn hoàn toàn có thể bỏ qua type trong function, tuy nhiên Dart không recommend theo cách này:
```
isNoble(atomicNumber) {
  return _nobleGases[atomicNumber] != null;
}
```
Nếu function chỉ có một expression (biểu thức), bạn có thể viết 1 cách ngắn gọn sau:
```
bool isNoble(int atomicNumber) => _nobleGases[atomicNumber] != null;
```

`=> expression` là cách viết gọn của `{ return expression; }`

>**Note:** Chỉ có expression đứng đằng sau `=>`, không áp dụng cho statement. Ví dụ bạn không thể để `if statement` đằng sau `=>` được. Tuy nhiên bạn có thể sử dụng conditional expression `condition ? expr1 : expr2`.

Một function có thể có 2 loại parameter: required(là những parame cần phải có) và optional(là những parameter có truyền hay vào hay không cũng được, nếu không truyền thì giá trị của parameter đó là `null`). Required parameters sẽ được viết trước, theo sau là các optional parameters.

## Optional named parameters
Khi gọi 1 function, bạn có truyền giá trị thông qua tên biến `paramName: value`, việc này giúp việc đọc code dễ dàng hơn trong các trường hợp function có quá nhiều parameter:
```
enableFlags(bold: true, hidden: false);
```
Để làm được thế, function phải khai báo parameters ở trong `{ }`, ví dụ `{param1, param2, …}`:
```
/// Sets the [bold] and [hidden] flags ...
void enableFlags({bool bold, bool hidden}) {
  // ...
}
```

## Optional positional parameters
Với optional parameter bạn có thể không cần truyền giá trị cho parameter đó. Bằng cách cho chúng vào trong `[]`:
```
String say(String from, String msg, [String device]) {
  var result = '$from says $msg';
  if (device != null) {
    result = '$result with a $device';
  }
  return result;
}

//Bỏ qua optional parameter
assert(say('Bob', 'Howdy') == 'Bob says Howdy');

//Truyền giá trị cho optional parameter
assert(say('Bob', 'Howdy', 'smoke signal') ==
    'Bob says Howdy with a smoke signal');
```

## Default parameter values
Bạn có thể sử dụng `=` để gán giá trị default cho parameter. Giá trị default phải là các compile-time constant:
```
/// Sets the [bold] and [hidden] flags ...
void enableFlags({bool bold = false, bool hidden = false}) {
  // ...
}

// bold will be true; hidden will be false.
enableFlags(bold: true);
```
Bạn cũng có thể gán _list_ hoặc _map_ là giá trị default bằng từ khóa `const`:
```
void doStuff(
    {List<int> list = const [1, 2, 3],
    Map<String, String> gifts = const {
      'first': 'paper',
      'second': 'cotton',
      'third': 'leather'
    }}) {
  print('list:  $list');
  print('gifts: $gifts');
}
```
