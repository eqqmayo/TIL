## 문자열(String)
문자열은 불변 객체라는 것이 가장 중요하다. 다트의 모든 타입은 참조타입이고 문자열도 마찬가지지만 값타입처럼 동작한다.
```dart
// 1. 문자열 결합
// 1-1. + 연산
String a = 'H';
a += 'i';
print(a);  // Hi
// 1-2. String Interpolation
print('하루는 내년에 ${age + 1}살');  // 하루는 내년에 3살

// 2. 문자열 처리
// 2-1. 일부 떼어내기
final str = 'eQQmayo';
print(str.substring(1, 4)); // QQm
// 2-2. 변환
print(str.replaceAll('QQ', 'GG')); // eGGmayo
print(str.toLowerCase()); // eqqmayo
// 2-3. 분리
print(str.split('')); // ['e', 'Q', 'Q', 'm', 'a', 'y', 'o']
// 2-4. 검색
print(str.indexOf('m')); // 3
print(str.lastIndexOf('o')); // 2
print(str.contains('e')); // true
print(str.endsWith('yo')); // true
// 2-5. 길이
print(str.length); // 7
print(str.isEmpty); // false
// 2-6. 내용비교
final newStr = 'eqqmayo';
print(str == newStr); // false
print(str.toLowerCase() == newStr); // true
```

### StringBuffer
문자열은 immutable 객체이기 때문에 + 연산자를 이용하여 문자열을 합치는 것은 느리다. 문자열이 업데이트 될때마다 새로운 객체를 생성하고, 가비지 컬렉터가 더 이상 안쓰는 문자열을 지우고 다닌다. 이는 비용이 드는 일이고 성능에 영향을 줄 수 있다.
대신 StringBuffer를 이용하면 훨씬 빠르다. StringBuffer는 다트에서 문자열을 효율적으로 조작하기 위해 제공되는 클래스로, 문자열 결합시 발생하는 성능 문제를 피할 수 있다.
- 여러 문자열을 반복적으로 결합할 때 새로운 문자열 객체를 계속해서 생성하는 대신 내부 버퍼를 사용한다.
- Mutable 객체로, 문자열을 추가/수정할 수 있다.
```dart
// + 연산자 시간 측정
final stopWatch = Stopwatch()..start();
String result = ''; // new
for (var i = 0; i < 10000; i++) {
  result += '$i'; // new
}
stopWatch.stop();
print(stopWatch.elapsedMilliseconds);  // 10

// StringBuffer 시간측정
final stopWatch = Stopwatch()..start();
final sb = StringBuffer('');
for (var i = 0; i < 10000; i++) {
  sb.write(i.toString());
}
stopWatch.stop();
print(stopWatch.elapsedMilliseconds);  // 2

// 사용 예시
StringBuffer buffer = StringBuffer();

buffer
  ..write('Hello');
  ..write(' ');
  ..write('World');
  ..writeln('!'); // 줄바꿈 추가
  ..writeAll(['This', 'is', 'a', 'test'], ' ');

  print(buffer.toString());
  // Hello World!
  // This is a test
```

### 문자열이 값타입처럼 동작하는 이유
- 불변성: 다트에서 문자열은 불변객체이다. 문자열을 한번 생성하면 그 내용을 변경하기 위해선 새로운 문자열 객체를 생성해야한다.
- 내용 기반 동등성: 다트에서 문자열의 동등성 비교는 내용 기반이다. 두 문자열의 내용이 같으면 동일한 것으로 본다(같은 메모리 주소를 참조). 이는 값타입의 동작 방식과 유사하다.

### Accessor와 Mutator
- Accessor: 인자가 없고 원본 객체를 변경하지 않음
- Mutator: 인자를 받고 원본 객체를 변경