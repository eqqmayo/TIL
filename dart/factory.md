## Factory pattern
GoF의 디자인 패턴 중 하나

initializer list는 주로 단순히 필드를 초기화하는데 사용되지만 factory 생성자는 더 복잡한 로직을 포함할 수 있다.

1. 싱글톤 패턴을 구현하는데 유용(factory가 싱글톤을 따르는 것이 아님) 즉 클래스의 단일 인스턴스만 존재하도록 보장할 수 있다.
```dart
class Singleton {
  static final Singleton _instance = Singleton._internal();
  factory Singleton() {
    return _instance;
  }
  Singleton._internal();
}
```

2. 동일한 인스턴스를 재사용하거나 캐싱하는데 유용(factory가 자체적으로 캐싱 기능을 제공하는게 아니라 직접 구현해야함) 이를 통해 동일한 값을 가진 객체를 여러번 생성할 때 메모리 사용을 줄일 수 있다.
```dart
class Point {
  final int x, y;
  static final Map<String, Point> _cache = <String, Point>{};
  factory Point(int x, int y) {
    final key = '$x,$y';
    if (_cache.containsKey(key)) {
      return _cache[key]!;
    } else {
      final point = Point._internal(x, y);
      _cache[key] = point;
      return point;
    }
  }
  Point._internal(this.x, this.y);
}
```

3. 다양한 반환 타입: 다형성을 활용하야 다양한 타입의 객체를 반환할 수 있다.
```dart
abstract class Shape {
  factory Shape(String type) {
    if (type == 'circle') return Circle();
    if (type == 'square') return Square();
    throw '$type 객체를 생성할 수 없음';
  }
}
class Circle implements Shape {}
class Square implements Shape {}
void main() {
  var shape1 = Shape('circle');
  var shape2 = Shape('square');
}
```

4. 복잡한 생성 로직: 셍성 로직이 복잡하거나 다양한 초기화 과정이 필요한 경우 이를 캡슐화할 수 있다.
```dart
class ComplexObject {
  final int a, b;
  factory ComplexObject(int x) {
    // 복잡한 초기화 로직
    int a = x * 2;
    int b = x + 3;
    return ComplexObject._internal(a, b);
  }
  ComplexObject._internal(this.a, this.b);
}

팩토리도 this에 접근안됨,, 얘도 static 같은 느낌. 다른 공간에 있음
```