## Navigator
앱 내 간단한 화면 이동은 Navigator을 통해 구현할 수 있다.   
Navigation은 스택 구조로 관리되며, 네비게이터를 통해 데이터를 주고 받는 것도 가능하다.   
(딥 링크를 구현하려면 Named Router(사용 지양)를 함께 쓰거나 Go Router와 같은 패키지를 써야한다.)
 
### 데이터 전달
```dart
onTap: () {
  Navigator.push(
    context,
    MaterialPageRoute(
      builder: (context) => TodoDetailScreen(todo: todo)),  // 데이터를 전달받을 위젯에 생성자를 통해 전달
  );
}
```

### 데이터 돌려받기
Navigator.push는 비동기 작업이기 때문에 기존 화면으로 돌아오기까지 시간이 걸린다.   
이 시간동안 위젯 상태에 변화가 생길 수 있기 때문에(ex. 앱이 백그라운드로 보내지거나 종료됨) mounted 속성을 통해 해당 위젯이 아직 위젯 트리에 존재하는지 체크해야한다.   
mounted가 false인 상태에서 setState를 호출하거나 context를 사용하면 오류가 발생해 앱 크래시가 날 수도 있기 때문이다.   
하지만 체크를 통해 return이 실행된다면, 사용자가 선택 이후 스낵바는 받지 못하지만 크래시를 방지할 수 있다.

```dart
// MainScreen
onPressed: () async {
  final result = await Navigator.push(  // SelectionScreen에서 result를 반환할 때까지 기다림
    context,
    MaterialPageRoute(builder: (context) => const SelectionScreen()),
  );

  if (!context.mounted) return;  // 비동기 작업 후 context를 사용할 때는 항상 이 체크를 하는 것이 안전하다.

  ScaffoldMessenger.of(context)  // 앱 전체에 걸쳐 스낵바를 관리하는 객체
    ..removeCurrentSnackBar()
    ..showSnackBar(SnackBar(content: Text('$result')));
}

// ...

// SelectionScreen
onPressed: () {
  Navigator.pop(context, 'Yeah');  // result로 'Yeah' 리턴
}
```
