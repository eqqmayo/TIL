## Context
Flutter에서 context는 위젯 트리에서 현재 위젯의 위치와 관련 정보에 접근할 수 있게해주는 중요한 객체이다.   
BuildContext 타입의 인스턴스로, 일반적으로 사용되는 변수명이 context이다.   
각 위젯은 자신만의 BuildContext를 가지며 context는 위젯 트리가 구축될 때 Flutter 프레임워크에 의해 생성된다.

1. 현재 위젯의 위젯 트리 내 위치 정보
2. 상위 위젯의 데이터나 기능에 접근 가능하게 함
3. Theme.of(context), MediaQuery.of(context) 등을 통해 앱의 전반적인 설정에 접근 가능

ex.
네비게이션: Navigator.of(context).push()   
상태 관리: Provider.of<T>(context)   
스낵바 표시: ScaffoldMessenger.of(context).showSnackBar()   
테마 접근: Theme.of(context).textTheme

context는 위젯이 트리에 추가될 때 생성되고, 위젯이 트리에서 제거될 때 함께 사라진다.   
mounted 속성은 이 context가 아직 유효한지(즉 위젯이 위젯 트리에 존재하는지)를 나타내며 비동기 작업 후에는 항상 context의 유효성을 확인해야 한다.   

또한 context는 위젯이 빌드될 때마다 생성되고, build 메서드 외부에서 저장하거나 사용하면 메모리 누수 문제를 일으킬 수 있다.   
Flutter의 위젯 생명주기와 일관되게 작동하려면 build 메서드 내에서 context를 사용하는 것이 가장 안전하고 권장된다.
