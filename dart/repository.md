## Repository
Repository 패턴은 데이터 저장소에 접근하는 객체를 추상화하고, 데이터소스와의 통신을 담당하는 객체를 캡슐화하는 디자인 패턴이다.

- 데이터소스와 상호 작용하여 데이터 추가, 조회, 수정, 삭제(CRUD) 역할을 담당
- 데이터 캡슐화
- 데이터 추상화
- 예외 처리

Business logic <-> Repositories <-> Datasource

데이터소스와 비즈니스 로직을 분리하면 유지 관리성, 재사용성, 테스트 용이성, 확장성이 향상하고, 데이터 액세스 추상화가 가능하다는 이점이 있다.
```dart
// Repository를 통해 데이터 조작을 캡슐화
class UserRepository {
    final _database = SqliteDatabase('users.db');
    Future<User> findUserById(String id) async {
        final results = await _database.query('users', where: 'id = ?');
        if (results.isEmpty) {
            return null;
        }
        return User(results[0]['id'], results[0]['name'], result[0]['age']);
    }
    Future<void> deleteUser(String id) async {
        await _database.delete('users', where: 'id = ?', whereArgs: [id]);
    }
 }
 ```
 확장을 고려하여 인터페이스를 정의해 추상화할 수 있다. 여러 버전의 Impl 클래스가 작성될 수 있고 테스트가 용이하다는 장점이 있다.
 ```dart
 abstract interface class TodoRepository {
    Future<Todo> findTodoById(int id);
    Future<List<Todo>> getAllTodos({bool refresh = false});
 }
 class TodoRepositoryImpl implements TodoRepository {
    final TodoDataSource _todoDataSource;
    List<Todo> _todos = []; // 네트워크로 받은 데이터 캐시
    TpdpRepositoryImpl(this._todoDataSource);
    @override
    Future<Todo> findTodoById(int id) => _todoDataDource.getTodo(id);
    @override
    Future<List<Todo>> getAllTodos({bool refresh = false}) async {
        if (refresh || _todos.isEmpty) {
            _todos = await _todoDataDource.getTodos();
        }
        return _todos;
    }
 }