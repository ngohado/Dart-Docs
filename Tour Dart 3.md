## Control flow statements
Anh em có thể tham khảo tại [official docs](https://www.dartlang.org/guides/language/language-tour#control-flow-statements). Vì phần này khá cơ bản và giống Java, không có gì đặc biệt nên mình sẽ bỏ qua.

## Throw and Exceptions
Tương tự như các ngôn ngữ khác, Dart cũng hỗ trợ [Exceptions](https://api.dartlang.org/dev/dart-core/Exception-class.html), [Errors](https://api.dartlang.org/dev/dart-core/Error-class.html) và rất nhiều các subtypes của 2 class đó.

Để throw hay raise lên một Exception ta có thế làm như sau:
```
throw new FormatException('Expected at least 1 section');

throw 'Out of llamas!';
```

>**Note:** Để tăng tính hiệu quả, cũng như giúp cho code meaning hơn. Chúng ta thường throw những error là subtype của `Error` và `Exception`.

Bởi vì việc throw ra một exception được coi là một expression. Do đó chúng ta có thể làm như sau:
```
void distanceTo(Point other) =>
    throw new UnimplementedError();
```

## Catch
```
try {
  breedMoreLlamas();
} on OutOfLlamasException {
  buyMoreLlamas();
}
```
Trên là cách chúng ta handle một exception `OutOfLlamasException` mà đoạn code trong `try` có thể throw ra. Bạn cũng có thể catch nhiều exception:
```
try {
  breedMoreLlamas();
} on OutOfLlamasException {
  // Xác định rõ loại exception mà bạn muốn handle
  buyMoreLlamas();
} on Exception catch (e) {
  // Nếu exception không phải là OutOfLlamasException, chúng ta handle những error là subtype của Exception
  print('Unknown exception: $e');
} catch (e) {
  // Không xác định, handle tất cả
  print('Something really unknown: $e');
}
```
Bạn dùng `on` khi muốn xác định type mà bạn muốn catch. Sử dụng `catch` để nhận được object mà đoạn code trong `try` throw ra.
```
try {
  // ···
} on Exception catch (e) {
  print('Exception details:\n $e');
} catch (e, s) {
  print('Exception details:\n $e');
  print('Stack trace:\n $s');
}
```

## Classes
Dart là ngôn ngữ hướng đối tượng với class và _mixin-based inheritance_. Mọi object đều là một instance của class. _Mixin-based inheritance_ có nghĩa là, mặc dù một class chỉ có duy nhất một superclass, nhưng mà class body (các variable, method) có thể được sử dụng lại như _multiple class hierarchies_ (hiểu nôm na là đa thừa kế, phần này đoạn sau sẽ làm rõ).

Bạn có thể tạo 1 object bằng từ khóa `new` với _constructor_ của class. Constructor có thể là _Classname_ hoặc _Classname.identifier_ (identifier này kiểu như là đặt tên cho constructor, ở mục constructor sẽ nói rõ):
```
var jsonData = jsonDecode('{"x":1, "y":2}');

// Create a Point using Point().
var p1 = new Point(2, 2);

// Create a Point using Point.fromJson().
var p2 = new Point.fromJson(jsonData);
```
>**Dart 2 note:** Với Dart 2 bạn có thể bỏ từ khóa `new`. Ví dụ: var p1 = Point(2, 2).

Để lấy ra type của object, bạn sử dụng property `runtimeType`:
```
print('The type of a is ${a.runtimeType}');
```

## Constructors
Đây là cách tạo một constructor:
```
class Point {
  num x, y;

  Point(num x, num y) {
    // There's a better way to do this, stay tuned.
    this.x = x;
    this.y = y;
  }
}
```
>**Note:** Chỉ sử dụng `this` when xảy ra name conflict.

Nếu chúng ta muốn gán trực tiếp các variable thông qua constructor chúng ta có thể làm như sau (cách này rất phổ biến):
```
class Point {
  num x, y;

  // Syntactic sugar for setting x and y
  // before the constructor body runs.
  Point(this.x, this.y);
}
```

### Default constructors
Nếu ta không tạo constructor cho class, mặc định Dart sẽ tạo ra constructor không tham số cho class đó.

### Constructors aren’t inherited
Các subclass không kế thừa các constructor của superclass. Nghĩa là nếu superclass có tạo ra 1 constructor, đồng nghĩa với việc các subclass cũng phải tạo ra constructor và gọi lại construcor của superclass:
```
class Person {
  final _name;

  Person(this._name);
}

class Musican extends Person {
  Musican(String name): super(name);
}
```

### Named constructors
Đánh tên cho constructor giúp cho constructor có nghĩa và rõ ràng hơn:
```
class Point {
  num x, y;

  Point(this.x, this.y);

  // Named constructor
  Point.origin() {
    x = 0;
    y = 0;
  }
}
```
Trong trường hợp kế thừa:
```
class Person {
  String firstName;

  Person.fromJson(Map data) {
    print('in Person');
  }
}

class Employee extends Person {
  // Person does not have a default constructor;
  // you must call super.fromJson(data).
  Employee.fromJson(Map data) : super.fromJson(data) {
    print('in Employee');
  }
}

main() {
  var emp = new Employee.fromJson({});
```

### Redirecting constructors
Thỉnh thoảng nhiệm vụ duy nhất của một constructor đó là chuyển hướng sang một constructor khác trong cùng một class:
```
class Point {
  num x, y;

  // The main constructor for this class.
  Point(this.x, this.y);

  // Delegates to the main constructor.
  Point.alongXAxis(num x) : this(x, 0);
}
```

### Constant constructors
Nếu như chúng ta muốn tạo ra một object không bao giờ thay đổi. Để làm điều đó, tạo ra một `const` constructor, và đảm bảo rằng các variable là `final`:
```
class ImmutablePoint {
  static final ImmutablePoint origin =
      const ImmutablePoint(0, 0);

  final num x, y;

  const ImmutablePoint(this.x, this.y);
}
```

### Factory constructors
Chúng ta sử dụng `factory` khi muốn tạo constructor không chỉ để tạo ra một instance mới của class mà có thể một instance từ cache, hoặc một subtype instance.

Dưới đây là ví dụ factory constructor trả ra một object từ cache.
```
class Logger {
  final String name;
  bool mute = false;

  // _cache is library-private, thanks to
  // the _ in front of its name.
  static final Map<String, Logger> _cache =
      <String, Logger>{};

  factory Logger(String name) {
    if (_cache.containsKey(name)) {
      return _cache[name];
    } else {
      final logger = new Logger._internal(name);
      _cache[name] = logger;
      return logger;
    }
  }

  Logger._internal(this.name);

  void log(String msg) {
    if (!mute) print(msg);
  }
}
```
>**Note:** Lưu ý rằng Factory constructor không thể truy cập vào `this`.

Sử dụng factory constructor như bình thường:
```
var logger = new Logger('UI');
logger.log('Button clicked');
```
