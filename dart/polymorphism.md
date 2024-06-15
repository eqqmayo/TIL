## 다형성(Polymorphism)
- 어떤 대상을 이렇게도 저렇게도 부를 수 있는 것
- 같은 부모를 가지는 인스턴스들을 부모 클래스 타입에 담아 같은 타입 취급할 수 있음
- 다형성 활용 방법
    - 선언은 상위클래스 / 인스턴스 생성은 하위클래스로
    - 인터페이스를 변수의 타입으로 사용 가능
    - 이용 가능한 멤버는 선언 타입이, 멤버의 동작은 인스턴스의 실제 타입이 결정
```dart
void main() {
  X obj = A();
  Y y1 = A();
  Y y2 = B();

  obj.a(); // a()만 호출 가능하다. X타입으로 선언되어 있기 때문

  if (obj is A) {  // 타입 체크해서 b, c 호출 가능 
    obj.b();
    obj.c();
  }

  (obj as A).b(); // 이렇게도 가능하나 타입 일치하지 않을시 런타임 오류 발생
  obj.c(); // 해당 문맥에서 여전히 A타입으로 간주하지만, 명확하게 하기위해선 캐스팅한 객체를 새 변수에 할당하여 사용

  y1.a(); // Aa
  y2.a(); // Bb

  /** cf. 타입 체크(as, is)하면 비용 많이 들기 때문에 성능면에서 하지 않는게 낫다. 
  구체적인 타입을 쓸 수 있다면 구체적으로 **/

  // 공통으로 채택한 인터페이스, 혹은 상속한 추상클래스 타입으로 담아 활용 가능: 다형성
  List<Y> list = [];

  A a = A();
  B b = B();

  list.add(a);
  list.add(b);

  list.forEach((obj) => obj.b());
}

abstract interface class X {
  void a();
}

abstract class Y implements X {
  void b();
}

class A extends Y {
  @override
  void a() {
    print('Aa');
  }

  @override
  void b() {
    print('Ab');
  }

  void c() {
    print('Ac');
  }
}

class B extends Y {
  @override
  void a() {
    print('Ba');
  }

  @override
  void b() {
    print('Bb');
  }

  void c() {
    print('Bc');
  }
}
```

### 일반 클래스 상속해도 되는데 왜 추상 클래스가 필요한거야?
- 추상 메서드를 통해 오버라이딩 강제
- 인스턴스화를 막아 해당 클래스가 상속의 재료 용도로만 사용됨을 명확히 표현

### 인터페이스 활용: 그룹화
```dart
abstract interface class A {} // 인터페이스는 메서드 없어도 됨: 그룹핑 하고 싶을때

abstract interface class B {}

class Dog implements A {} // A 그룹에 속함

class Desk implements A, B {} // 교집합도 가능
```

### 다형성의 의의
- 다형성(상속, 그룹핑 등)을 이용해서 설계를 잘해놓으면 코드를 짤때 수월하다.
- **확장**이 자유로움. 결국에는 추상클래스보다 인터페이스를 많이 쓰게된다. -> 스위프트의 프로토콜 지향 프로그래밍

### 스위프트가 프로토콜을 지향하는 이유?
- 다중 상속을 허용하여 유연한 설계 가능, 모듈화하여 관리하기 쉬움 / 추상클래스는 단일 상속만 가능하다.
- 유연성과 재사용성: 특정 구현에 의존하지 않기 때문에 다른 타입에서 동일한 프로토콜을 채택하고 다른 방식으로 구현 가능
