## URI ⊃ URL, URN

- **URI(Uniform Resource Identifier)**
URI는 자원의 고유 식별자로 URL과 URN을 포함하는 개념이다.

- **URL(Uniform Resource Locator)**
자원의 위치를 나타낸다. 위치가 변경되면 기존 URL을 더이상 사용하지 못한다는 단점이 있다.

- **URN(Uniform Resource Name)**
자원의 고유한 이름으로 자원의 위치와는 독립적이다.   
URL이 가지는 위치 의존적인 단점을 극복할 수 있다. 사용 예시중 하나로 도서 식별 번호인 ISBN이 있다.

## URI와 URL 구분하기
주소에 식별자가 있으면 URI
리소스 위치까지만 나타내면 URL

1) http://eqqmayo.co.kr/category
category라는 자원의 위치를 나타내므로 URL이다.

2) http://eqqmayo.co.kr/category/3 (Path Variable 방식, 특정한 자원)
/3 부분이 식별자이므로 URI이다. (URL을 포함)

3) http://torang.co.kr/category?id=107 (Query Parameter 방식, 자원 필터링)
쿼리스트링 식별자(?id=107)를 포함하므로 URI이다. (URL을 포함)

![image](https://github.com/user-attachments/assets/1f47e11d-af42-40f3-963f-81bbfd774c4c)
