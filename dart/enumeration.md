## 열거형(Enum)
정해둔 값만 넣어둘 수 있는 타입
```dart
enum Rps {
  rock,
  scissors,
  paper, 
}

// 열거형을 쓰지 않고 클래스의 정적 상수를 사용할때
class Rps {
  static const rock = 1;
  static const scissors = 2;
  static const paper = 3;
}

// ...

if (myChoice == Rps.rock) {
  print('바위');
} else if (myChoice == Rps.scissors) {
  print('가위');
} else {
  print('보');
}
```
### 열거형만의 장점
- 가독성: 특정한 값 집합을 명확하게 표현, 값 비교가 명확함
- 유지보수 및 확장성: 새로운 값 추가, 기존 값 변경이 쉬움
- switch문을 이용해 패턴 매칭 가능

```dart
void getMyChoice(Rps rps) {
  switch (rps) {
    case Rps.rock:
      print('바위');
    case Rps.scissors:
      print('가위');
    case Rps.paper:
      print('보');
  }
}
```