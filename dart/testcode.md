## Tests
1. pubspec.yaml에 test 패키지 추가
2. test 폴더에 [클래스명]_test.dart 파일 생성
3. given-when-then 패턴을 사용할 수 있다.
```dart
void main() {
  test('Wand constructor test, 지팡이의 이름은 3문자 이상이어야함', () {
    expect(() => Wand(name: '지팡', power: 70), throwsException);
    expect(() => Wand(name: '지팡이', power: 70), returnsNormally);
  });
 
  group('Wand setter test', () {
    setUp(() { 
      Wand wand = Wand(name: '지팡이', power: 70);
    });

    test('지팡이의 이름은 3문자 이상이어야함', () {
      expect(() => wand.name = '지팡', throwsException);
      expect(() => wand.name = '지팡지팡', returnsNormally);
    });

    test('지팡이의 마력은 0.5 이상 100.0 이하여야함', () {
      expect(() => wand.power = 0.3, throwsException);
      expect(() => wand.power = 0.7, returnsNormally);
    });
  });
}
```
- test() 함수에 테스트에 대한 설명과 테스트 코드 작성
- group() 함수로 관련있는 테스트끼리 묶어서 수행할 수 있음
- setUp() 함수는 각 테스트 시작 전마다 실행
- setUpAll() 함수는 모든 테스트 시작 전 한 번만 실행되어 유지: 데이터베이스 연결 등 한 번만 초기화가 필요한 작업에 사용

## Tips
- 한 테스트 내에서 값 여러개 & 함수 여러번 실행하여 구체적으로 테스트
- 경계값도 테스트
- 경계값과 너무 먼 값 사용하지 않기 ex. double이라면 +/-0.01
- Matcher(equals, inInclusiveRange, etc) 잘 활용
- 테스트 설명 구체적으로
- 함수 내에 익셉션 있는 경우 익셉션 테스트도 포함
    - returnsNormally / throwsException

https://pub.dev/packages/test
