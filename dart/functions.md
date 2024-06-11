## Function vs. Method

| |함수|메서드|
|:---:|:---:|:---:|
|위치|클래스 외부|클래스 내부|
|역할|특정 작업 수행|객체의 동작 수행|
|의존성|객체 상태에 의존 x|객체의 속성에 접근/변경 가능|
|호출|독립적|객체를 통해 호출

```dart
int plus(int a, int b) {
  return a + b;
}

class Person {
  String name = '태오';
    
  void introduce() {
    print('내 이름은 $name야!');
  }
}

plus(1, 2); // 함수 호출

final theo = Person(); // 인스턴스 생성 및 메서드 호출
theo.introduce();
```

## Anonymous functions