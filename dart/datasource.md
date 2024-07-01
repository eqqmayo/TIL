## 데이터소스(DataSource)
데이터소스란 프로그램이 사용하는 모든 데이터의 근간이 되는 원천 데이터를 말한다.
예를 들어 지하철앱에는 지하철 이름, 출발/도착 시간, 출발/도착역 등의 정보를 담은 데이터소스가 필요하다.

### Json과 데이터 클래스의 상호 변환
서버와의 통신은 대부분 Json으로 이루어진다. Json 형태의 데이터소스를 쉽고 편하게 활용, 조작하려면 클래스 형태로 변환하는 과정이 필요하다.
1. 서버에서 Json 형태의 문자열 보내줌
2. 문자열을 다트의 Map으로 변환: jsonDecode (<-> jsonEncode)
3. Map 데이터를 클래스의 인스턴스로 변환: fromJson

```dart
class TodoDataSource {
  Future<List<Todo>> getTodo() async {
    final response = await http.get(Uri.parse('https://~'));
    final Map<String, dynamic> json = jsonDecode(response.body);
    return Todo.fromJson(json);
  }
  // Json List String을 List<모델>로 변경하려면 map() 활용
  Future<List<Todo>> getTodos() async {
    final response = await http.get(Uri.parse('https://~'));
    final List jsonList = jsonDecode(response.body);
    return jsonList.map((e) => Todo.fromJson(e)).toList();
  }
}
```
## Model Class
```dart
class Dog {
  String name;
  int age;
  Dog(this.name, this.age);
}
```
- 데이터소스를 앱에서 필요한 형태로 변환한 데이터
- 일반적으로 별도의 기능(메서드)을 가지지 않는 순수한 클래스로 작성
- 데이터 클래스 4종 세트 및 직렬화 2종이 필요하면 추가하여 사용
- 비슷한 용어: 도메인 모델, Entity, DTO, POJO, VO, 데이터 클래스

### 모델링 방법
**DDD(Domain Driven Design)**: 도메인(특정 상황, 객체가 중심이 된 유사한 업무의 집합)을 클래스로 작성
- 클래스를 사용하면 도메인의 복잡한 비즈니스 로직과 제약조건을 통합할 수 있고, 이를 독립적으로 테스트하기 쉬움
- 데이터를 보호(캡슐화)하고 데이터 무결성을 유지할 수 있음
- 단순한 데이터 교환이나 임시 데이터 저장 등 단순한 용도의 경우 Json이나 Map이 더 적합할 수 있지만, 도메인의 비즈니스 로직을 다루고자 할 때는 클래스를 사용하는 것이 많은 이점이 있음

**ORM(Object-relational mapping)**: DB 데이터소스와 모델 간의 상호변환을 돕는 기법