## Assert
- 개발 모드에서 디버깅 중일때만 영향을 미치며 배포 코드에서는 작동되지 않는다. 
- 조건이 거짓인 경우 AssertionError 발생 및 오류 메세지 출력
```dart
assert(number < 100, 'number는 100보다 작아야함!');
```