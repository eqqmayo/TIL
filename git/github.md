## HTTPS와 SSH
원격 저장소에 접근하고 데이터를 전송하는 프로토콜
- HTTPS
    - 사용자의 id/pw를 이용하여 인증
    - 쉽고 간편하지만 원격저장소에 push, pull 하거나 접근할 때마다 인증해야하는 불편함
    - git의 credential 저장소 기능 혹은 OS 자체의 인증 캐싱(mac keychain)을 이용하면 매번 입력안해도 됨

- SSH
    - 기기별 key 개념, 매번 로그인안해도 됨
    - 초기설정이 복잡
    - 로컬 컴퓨터와 원격 서버 컴퓨터의 private과 public key를 비교하여 자동로그인
    - 보안성이 높음'