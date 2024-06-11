## static
- 인스턴스가 아닌 해당 클래스 자체에 속하는 멤버: 모든 인스턴스가 공유
- 인스턴스를 생성하지 않고도 클래스 이름을 통해 접근 가능
- 클래스의 static 멤버에 처음 접근하거나 클래스의 인스턴스를 처음 생성할 때 초기화됨: 메모리 효율 좋음
- static 함수는 메서드가 아닌 함수여야만함: 클래스의 인스턴스 멤버에 영향받지 않아야함
```dart
void main() {
  final a = MyClass();
  final b = MyClass();

  a.plusOne();
  print(MyClass.num);  // 1

  b.plusOne();
  print(MyClass.num);  // 2
}
```