## List vs. Array
- 다트는 배열이 아니라 리스트를 지원한다.
- 다트와 배열과 같은 역할을 하지만 차이점이 있다.
    - List는 다양한 타입의 요소 포함 가능
    - Array는 요소들이 메모리에 연속적으로 할당되어 있어 삽입, 삭제시 모든 요소를 옮겨야하므로 느리다.
    - List는 해당 연결만 끊고 새 메모리를 할당하므로 빠르다.
    
## etc.
- List.any(condition): 리스트의 모든 요소가 조건을 만족하면 true 리턴