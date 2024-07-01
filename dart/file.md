## File
파일 열기 - 파일 읽기/쓰기 - 파일 닫기
```dart
final myFile = File('파일경로');       // 파일 열기
myFile.writeAsStringSync('Hallo');   // 파일 쓰기
final content = file.readAsStringSync(); // 파일 읽기
```
파일 조작은 시간이 오래 걸림. readAsString (Future 타입) sync 어쩌구 x 다른 작업 못하니까 쓰지말기

파일 존재하는지 exist() 쓸 수 있음 퓨처함수라 await 써야함 

파일 write안하고 copy, delete 메서드 쓸 수 있음. 얘네도 퓨처기때문에 async await 써야함