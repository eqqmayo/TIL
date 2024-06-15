## Field vs. Property
### 필드(Field)
- 클래스의 상태를 저장하는 변수
- (= 멤버 변수)

### 프로퍼티(Property)
- 필드(=멤버 변수)에 대한 접근을 제어하는 메서드의 집합
- 보통 getter/setter를 포함
- private한 필드에 접근하지 않고 값을 읽거나 쓰도록 함: **캡슐화**

```dart
class Monster {
  String name;  // field
  int _hp;      // field

  int get hp => _hp;    // property

  set hp(int value) {   // 유효성 검사
    if (value < 0) {
      throw Exception('hp는 0 이상이어야 함!');    
    }
    _hp = value;
  }

  Monster({
    required this.name,
    required int hp,
  }) : _hp = hp {
    this.hp = hp
  };
}
```

### 프로퍼티를 사용하는 이유: 객체 무결성
1. 상태의 일관성:
객체의 속성, 필드가 항상 예상 가능하고 정해진 로직에 따라 유지됨
2. 데이터 보호 및 유효성 검사:
객체의 필드에 잘못된 값이 할당되는 것을 방지
3. 캡슐화:
객체의 내부 데이터를 외부로부터 숨겨 데이터의 무결성 보장

## getter와 setter
### getter 읽기 속성 / setter 쓰기 속성
- 속성 형태지만 메서드임
- 둘을 같이 쓸 일은 거의 없음: 같이 쓰면 일반 속성과 다름없음
- read only 혹은 write only 실현
### 참고
- 무조건 getter나 setter에서 유효성 검사를 수행하기보다는 경우에 따라 생성자에서만 거르는게 적합
- setter에서 value 할당하는것 잊지않기
- get 블럭에서 set을 구현할 수는 있지만 읽기에만 집중하는 것이 바람직
