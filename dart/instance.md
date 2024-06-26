## Object class
**모든** 클래스는 Object 클래스를 상속한다.
즉 어떤 타입의 인스턴스든 Object로 선언할 수 있고 Object의 멤버를 가진다.
- toString()
- operator ==
- hashCode

```dart
class Cat extends Object {} // 이렇게 하지않아도 이미 상속받고 있음
```

### toString()
오버라이드하여 해당 데이터를 문자열 형태로 나타내기 위해 쓸 수 있음

```dart
class Person {
  String name;
  int age;

  Person({
    required this.name,
    required this.age,
  });

  @override
  String toString() {
    return '이름: $name, 나이: $age';
  }
}
```

### operator(==)
== 연산자를 오버라이드하여 내가 정한 규칙에 따라 두 객체가 같다고 정의할 수 있다.

```dart
// 재정의하지 않았을때
final person1 = Person(name: 'haru', age: 3, pet: haru);
final person2 = Person(name: 'haru', age: 3, pet: haru);

print(person1 == person2); // false
```

두 인스턴스는 모든 속성값이 같지만 다른 객체로 취급된다. 해쉬값이 다르기 때문이다.

```dart
@override
bool operator ==(Object other) =>
    identical(this, other) ||  // 메모리 주소 같은지 확인
    other is Person &&
        runtimeType == other.runtimeType &&
        name == other.name &&
        age == other.age &&
        pet == other.pet;
          
@override
int get hashCode => name.hashCode ^ age ^ pet.hashCode;

print(person1 == person2); // true
```

== 과 hashCode를 내가 정한 동등성 규칙에 맞게 재정의하면, 규칙을 만족하는 인스턴스끼리는 같은 객체로 취급된다.

동등성을 비교할 때는 클래스 내부의 모든 속성의 동등함을 비교해야 하므로, 사용자 정의 클래스에 관한 동등성 규칙이 있다면 해당 클래스의 동등성 규칙도 작성해야한다. ex) 코드의 Animal 클래스

Object 클래스에 정의된 == 연산자의 매개변수 타입이 Object인데, 이떼 같은 타입의 객체끼리만 비교하고 싶다면 covariant 키워드를 사용해 파라미터 타입을 구체적인 서브타입으로 바꿔줄 수 있다. 그럼 타입 확인하는 코드도 없어도 된다.

```dart
@override
bool operator ==(covariant Person other) =>
    identical(this, other) ||
        name == other.name &&
        age == other.age &&
        pet == other.pet;
```

### hashCode
일반적으로 ==와 hashCode는 일관성있게 재정의한다. 거의 무조건

서로 다른 hashCode를 가지는 객체는 == 연산자로 비교했을때 다른 객체로 판단된다.
hashCode를 재정의하지 않으면 Object 클래스의 hashCode를 사용하는데, 이 기본 해시코드는 객체의 메모리 주소를 기반으로 하므로(cf. 해시코드 != 메모리주소)
기대한 동등 관계를 얻을 수 없다.

해시테이블의 평균 시간복잡도는 O(1): 데이터가 아무리 많아도 항상 검색 속도 일정
```dart
@override
int get hashCode => name.hashCode ^ age ^ pet.hashCode;
```

## Deep copy
깊은 복사는 원본 객체와 동일한 내용을 가지면서 원본 객체와는 완전히 독립적인 새 객체를 만드는 것이다. 참조가 아닌 값을 복사하는 것

다트에서는 별도로 깊은 복사 메서드를 제공하지 않는다. 직접 작성해야함
```dart
Person copyWith({
  String? name,
  int? age,
  Animal? pet,
}) {
  return Person(
    name: name ?? this.name,
    age: age ?? this.age,
    pet: pet ?? this.pet
  );
}

final person3 = person2.copyWith();
print((person2.name, person2.age, person2.pet) 
    == (person3.name, person3.age, person3.pet)); // true
```

## sort()
Comparable 인터페이스를 상속받아 compareTo 메서드를 구현하거나, sort 함수 사용시 즉석에서 comparator 함수를 구현해 정의한 규칙에 따라 대상을 정렬할 수 있다.
```dart
// 방법1)
class Person implements Comparable<Person> {
  @override
  int compareTo(Person other) {
    return -age.compareTo(other.age); // - 붙이면 순서 반대로
  }

  List<Person> people = [person1, person2, person3];
  people.sort();
}

// 방법2)
people.sort((a, b) => -a.age.compareTo(b.age));
// 이렇게도 가능
people.sort((a, b) => b.age.compareTo(a.age));
```