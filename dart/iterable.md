## Iterable
Iterable class는 **순차적으로 접근**할 수 있는 요소의 Collections를 말한다. 순차적으로 접근이 가능하기 때문에 forEach, for문 등의 문법을 사용할 수 있는 것이다. List, Set 모두 iterable하고, 독립적인 object만 iterable하게 선언할 수 있기때문에 Map의 경우 Map 자체가 아닌 Key, Value, Entries가 iterable하다.

### Iterator
이러한 자료구조의 내부 요소를 순회하는 객체를 Iterator라고 한다. iterator는 다음에 순회할 값이 있는지 확인하는 moveNext()가 true를 리턴하면 iterator.current는 현재 순회하고 있는 값을 리턴한다.

```dart
  Set set = {3, 1, 5, 4};
  var a = set.iterator;

  print(a.current);  // null

  while (a.moveNext()) {
    print(a.current);      // 3 1 5 4
  }
```