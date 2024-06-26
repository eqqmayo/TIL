## 동기
- 코드 순서대로 작업: 이전 작업 완료되어야 다음 작업 시작
- 작업 완료될 때까지 프로그램 중단되지 않음

## 비동기
- 임의의 순서 또는 동시에 작업
- 현재 코드의 실행 결과를 받지 않고 다음 코드를 실행
- 대부분의 코드는 기본적으로 동기적으로 실행되지만, API 통신, 파일 I/O, 타이머 등과 같은 오래 걸리는 작업은 비동기적으로 실행됨
- 콜백, Future, async-await을 사용해 비동기 작업을 동기 작업처럼 처리할 수 있음

### 콜백(Callback)
콜백함수는 함수의 인자로 전달되어 특정 작업이 끝났을때 호출된다.

비동기는 현재 코드의 실행 결과를 받지 않고 다음 코드를 수행한다. 그렇기 때문에 정확한 순서를 지켜 실행되어야 하는 경우 문제가 생길 수 있다. 예를 들어 통신의 결과로 전달받은 데이터를 다음 함수에 전달해야할 때, 비동기적으로 실행된다면 빈 데이터가 전달될 수 있다.

콜백 함수를 이용해 코드를 순차적으로(동기적으로) 실행하여 이러한 문제를 막을 수 있다.

```dart
void loadData(Function(String) success, Function(String) error) {
  Future.delayed(Duration(seconds: 2), () {
    bool success = true;
    if (success) {
      success('성공');
    } else {
      error('Error');
    }
  });
}
```
하지만 콜백을 너무 많이 사용할 경우 가독성이 좋지 않다. async-await를 활용해 더 깔끔한 코드를 작성할 수 있다. 

### Future
미래에 완료되는 객체로, 미래에 받아올 값을 의미한다.
Dart, Flutter의 많은 API는 Future 타입을 리턴한다.
Future 함수는 본문 앞에 async 키워드를 붙여야한다. 비동기 함수를 실행할때 await 키워드를 사용하면 코드 작성 순서대로 실행된다.

```dart
void myFunc() {
  print('start');

  Future.delayed(Duration(seconds: 2), () {
    print('2초');
  });

  print('end');     
}

myFunc();   // start end 2초
```
```dart
Future<void> myFunc() async {
  print('start');

  await Future.delayed(Duration(seconds: 2), () {
    print('2초');
  });

  print('end');
}

myFunc();   // start 2초 end
```
then 메서드는 Future가 완료되었을 때 호출될 콜백 함수를 받을 수 있다.
Future 함수의 결과를 then 함수를 이용해 전달할 수 있고, 불필요하다면 _를 이용해 생략한다. Future는 성공일 수도 오류를 발생시킬 수도 있다.

```dart
saveDb(user)
    .then((_) => sendEmail(user))
    .then((_) => getResult(user));
    .catchError((e) => print(e));
    .whenComplete(() => print('성공, 실패 관계없이 실행'));
```
콜백보다 편리하지만 단계가 많아지면 체이닝 방식 사용, 결과 예측, 예외처리면에서 용이하지 않다.

### async-await
가장 큰 장점은 비동기 코드를 깔끔하게 작성할 수 있다는 점이다.
await 키워드는 Future가 끝날때까지 함수 실행을 일시 정지한다.
await를 이용해 비동기 코드를 동기 코드처럼 실행할 수 있고 async 키워드를 함께 써줘야 한다.
퓨처 함수를 쓰려면 await를 써야하고, await는 퓨처 함수 내에서만 쓸 수 있다.

```dart
Futrue<String> register(user) async {
  await saveDb(user);
  await sendEmail(user);
  return await getResult(user);
}
```
예외 처리시 async-await와 try-catch를 함께 이용하면 가독성이 좋다.

```dart
Future<String> getData() async {
  try {
    var data = await fetchData();
    return data;
  } catch (e) {
    print('데이터 가져오기 실패: $e');
    return '';
  }
}
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7cb2da65-5d73-4b42-9d3f-d5937394ba97/30b0bc7b-9c62-4edb-a763-1ba3a1f9cc50/Untitled.png)
미묘하게 다름 선생님은 위에거 선호하신다고..