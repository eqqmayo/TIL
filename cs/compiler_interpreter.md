## 컴파일러 언어 vs. 인터프리터 언어
### 컴파일러 언어
- 컴파일러가 전체 소스 코드를 한 번에 번역하여 실행 파일 생성
- 컴파일된 파일은 기계어로 직접 실행되기 때문에 실행 속도가 빠름
- 컴파일 중 문법, 타입 오류 발견
- C, C++, Swift, Dart 등

### 인터프리터 언어
- 인터프리터에 의해 한 줄씩 번역되고 즉시 실행
- 매번 번역과 실행을 거치므로 비교적 느릴 수 있음
- 실행 중 오류 발생 즉시 알려줌: 런타임 에러 많이 발생
- Python, JavaScript, Ruby 등

### 요약

| |컴파일러 언어|인터프리터 언어|
|:---:|:---:|:---:|
|실행|한 번에 번역|한 줄씩 번역|
|속도|빠름|느릴 수 있음|
|배포|실행 파일만 필요|소스코드 + 인터프리터 필요|
|오류|컴파일 과정중 발견|실행 중 발견|