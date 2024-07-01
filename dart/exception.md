## 예외(Exception)
프로그램을 설계할 때 실행시에 발생할 수 있는 예외 상황에 대해 사전에 적절한 조치를 취해야 한다.
이러한 예외 처리가 없으면 프로그램이 에러가 나며 죽어버린다.

## 에러(Error)
### 에러 종류
- syntax error: 문법, 형식적인 오류 / 컴파일중 에러남
- runtime error: 실행중 예상외의 상황이 발생하며 동작 중지 / 실행중 강제 종료됨
- logic error: 기술한 내용의 논리적인 오류 / 실행하면 예상외의 값 나옴

### 예외 상황
- 메모리 부족
- 파일 찾을 수 없음
- 네트워크 통신 문제

### 예외 처리
런타임 에러에 대한 대처로, try-catch문으로 예외 처리를 할 수 있다.
```dart
void main() {
  try {
    someError2();
  } on FormatException {            // 특정 예외를 캐치
    print('FormatException 발생');
  } catch (e) {                     // (cf. 에러는 Object 타입)
    print(e)
  } finally {
    print('항상 실행되는 코드');
  }
  void someError2() {
    try {
      someError();
    } catch (e) {
      rethrow;       // rethrow로 에러 처리 미룰 수 있음
    }
  }
  void someError() {
    // sth
    throw FormatException()  // 임의로 예외 발생시킴
  }
}
```