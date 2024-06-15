## 추상 클래스(Abstract class)
상속의 재료로 사용하는 부모 클래스
- 구현부가 정의되지 않은 추상메서드가 일부 포함된 클래스, 꼭 포함 안해도 됨
- 인스턴스화가 금지되어 있음 ⭐️
- 해야하는 오버라이드를 안하는 실수를 막는 효과
- 추상클래스를 상속받은 추상클래스는 오버라이드 안해도됨

## 인터페이스(Interface)
인터페이스 == 프로토콜
- 기능들만 모여있음, 필드 없음
- 모든 메서드의 구현부가 없음
- 여러 인터페이스를 구현할 수 있음(다중 구현)
- 인터페이스에서 getter/setter 구현 가능

```dart
abstract interface class Creature {
  double get weight;

  set weight(double value);  
}

abstract class Animal {
  String name;
  int age;

  Animal({
    required this.name,
    required this.age,
  });

  void talk();       // 강제 오버라이드 o

  void walk() {
    print('걷기');    // 강제 오버라이드 x
  }
}

class Dog extends Animal implements Creature {
  String breed;
  @override
  double weight;

  Dog({
    required super.name,
    required super.age,
    required this.breed,
    required this.weight,
  });

  @override
  void talk() {
    print('왈왈');
  }
}
```