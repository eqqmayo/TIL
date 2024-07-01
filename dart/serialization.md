## 데이터 형식
### CSV
데이터를 콤마로 나눈 형식
### XML
<> 태그를 활용, 포함관계 기술 가능, Parsor를 제작해야함
### JSON
- 네트워크 통신에서 가장 많이 사용됨
- XML에 비해 용량이 작고, 컴퓨터와 사람이 이해하기 쉽다.
- []로 리스트, {}로 객체 표현
- key, value 형태로, 다트의 Map<String, dynamic>과 똑같이 생겼다.

## 직렬화와 역직렬화
직렬화란 데이터 구조나 객체 상태를 파일 형태로 저장하고 나중에 재구성이나 통신을 하기 쉬운 포맷으로 변환하는 과정

클래스 내부 필드에 다른 클래스가 있다면 모두 직렬화 해주어야 한다.

서버에서 Json 형태의 String으로 들어오기 때문에 디코딩, 반대 상황에서는 인코딩이 필요하다.

직렬화: 클래스 -> Json / 역직렬화: Json -> 클래스
```dart
class Department {
  String name;
  Employee leader;
  Department(
    this.name,
    this.leader,
  );
  Department.fromJson(Map<String, dynamic> json)
      : name = json['name'],
        leader = Employee.fromJson(json['leader']);  // 역직렬화 처리
  Map<String, dynamic> toJson() => {
        'name': name,
        'leader': leader.toJson(),      // 직렬화 처리
      };
}
// ...
void main() {
  final gildong = Employee('홍길동', 41);
  final admin = Department('총무부', gildong);
  final companyFile = File('company.txt');
  final encodedAdmin = jsonEncode(admin.toJson());
  companyFile.writeAsStringSync(encodedAdmin);
}
```