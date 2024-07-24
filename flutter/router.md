## Named Router(잘 안씀)
1. 모든 라우트를 한 곳에서 정의할 수 있고
2. 딥링킹 구현이 용이하며
3. 라우트 이름을 기반으로 네비게이션 로직을 쉽게 테스트할 수 있다.
   
간단하고 직관적이지만, 복잡한 네비게이션 구조나 중첩 라우팅을 처리하는 데는 한계가 있다.   
또한 타입 안정성이 부족하고 컴파일 타임에 오류(오타, 존재하지 않는 라우트, 잘못된 타입의 인자 전달 등)를 잡기 어려우며,   
뒤로가기가 지원되지 않기 때문에 사용이 권장되지 않는다.

```dart
MaterialApp(
  initialRoute: '/',
  routes: {
    '/': (context) => FirstScreen(),
    '/profile': (context) => ProfileScreen(userId: ModalRoute.of(context)!.settings.arguments as int),
    '/settings': (context) => SettingsScreen(),
  };
)

Navigator.pushNamed(context, '/profile', arguments: 8);
```
대규모 프로젝트나 복잡한 네비게이션 구조를 가진 앱에서는 Named Router 대신 주로 GoRouter, AutoRoute를 사용한다.   
이런 라이브러리들은 타입 안정성을 개선하고 컴파일 타임 체크를 강화하여 Named Router의 문제들을 보완한다.

## Go Router
```dart
final router = GoRouter(
  initialLocation: '/',
  routes: [
    GoRoute(
      path: '/',
      builder: (context, state) => FirstScreen()
    ),
  ],
)
```

tbu
