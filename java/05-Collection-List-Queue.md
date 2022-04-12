## 1. 개념

- 목록성 데이터를 처리하는 자료구조를 통칭하는 용어
- 종류
    - List: 순서가 있는 목록
    - Set: 순서가 중요하지 않은 목록
    - Queue: 선입선출형 목록
    - Map: K-V 형으로 저장되는 목록
    


## 2. List

- 순서가 있는 Collection
- 종류
    - ArrayList: 확장가능한 배열. 여러명이 달려들어 값을 변경하려면 문제 발생(Thread safe 하지 않음)
    - Vector: 확장가능한 배열. 여러명이 달려들어 값을 변경 가능(Thread safe함)
    - stack: vector 클래스를 확장한 LIFO(Last in first out) 형식의 배열

### 2.1. ArrayList

- ArrayList 에는 어떤 객체도 넣을 수 있지만 되도록 한가지 객체만 저장하자
- 여러 종류의 객체를 넣고싶으면 DTO라는 객체를 만들어 담는것이 좋다
- 메서드
    - 생성
        - ArrayList() : 객체 저장할 공간 10개 생성
        - ArrayList(Collection<? Extends E> c) : 매개변수(컬렉션)이 저장되어 있는 ArrayList 생성
        - ArrayList(int initialCapacity): 매개변수만큼 저장공간 생성
    - 추가

  | 리턴 | 메소드명 | 설명 |
      | --- | --- | --- |
  | boolean | add(E e) | 가장 끝에 추가 |
  | void | add(int index, E e) | 지정된 index에 추가 |
  | boolean | addAll(Collection<? extends E> c) | 컬렉션 데이터를 가장 끝에 추가 |
  | boolean | addAll(int index, Collection<? extends E> c) | 컬렉션 데이터를 지정된 index에 추가 |
    - 꺼내기

  | 리턴 | 메소드명 | 설명 |
      | --- | --- | --- |
  | int | size() | 데이터 개수 |
  | E | get(int index) | 해당 index의 데이터 리턴 |
  | int | indexOf(Object o) | 매개변수와 동일한 데이터의 index 리턴 |
  | int | lastIndexOf(Object o) | 매개변수와 동일한 마지막 데이터의 index 리턴 |
  | Ojbect[] | toArray() | ArrayList 객체에 있는 값들을 Object[] 배열로 만듦 |
  | <T> T[] | toArray(T[] a) | ArrayList 객체에 있는 값들을 매개변수로 넘어온 T타입의 배열로 만듦 |

  > toArray()는 Object로 리턴하고 toArray(T[] a)은 리턴타입을 특정할 수 있다. 제네릭을 사용하여 선언한 ArrayList 객체를 배열로 생성할 때에는 후자를 사용하는것이 좋다. (그래야 배열 안에 있는 타입을 알아서 그 값으로 또 뭔가를 할 수 있다)
  >
    - 삭제

  | 리턴 | 메소드명 | 설명 |
      | --- | --- | --- |
  | void | clear() | 전체삭제 |
  | E | remove(int index) | 해당 위치 삭제, 삭제한 데이터 리턴 |
  | boolean | remove(Object o) | 매개변수와 동일한 첫번째 데이터 삭제 |
  | boolean | removeAll(Collection<?> c) | 매개변수(컬렉션)와 동일한 모든 데이터 삭제 |
    - 수정

  | 리턴  | 메소드명 | 설명 |
      | --- | --- | --- |
  | E | set(int index, E element) | 해당 인덱스 데이터를 E로 바꿈, 원래 있던 데이터 리턴 |

<aside>
💡 Shallow copy: 원본 객체의 주소만 할당해서 복사. 원본 객체가 변하면 복사본 객체도 변함.

</aside>

<aside>
💡 Deep copy: 원본 객체의 모든 값을 복사. 서로 값을 변경해도 영향이 없음

</aside>

### 2.2 Stack

- LIFO(Last In First Out) 기능 구현할 때 사용
- Stack vs ArrayDeque
    - 둘다 LIFO
    - ArrayDeque가 더 빠름
    - Stack 이 쓰레드에 더 안전
- 생성자
    - stack() : 아무 데이터도 없는 Stack 객체 만들기
- 메소드

### 2.3 LinkedList

- List이면서 Queue, Deque인터페이스도 구현함
    - Queue: FIFO를 구현한 자료구조
    - Deque: Queue 인터페이스의 확장버전. Queue 기능 + 맨 앞/맨 뒤에 값을 넣거나 빼는 작업 용이
- 연결된 노드들의 집합인데, 각 노드는 데이터와 포인터(다음 노드를 가리키는) 로 이루어져 있다.
- 데이터 추가시 새로운 데이터 노드를 만들고 이전 노트의 포인터를 새 노드를 가리키게 만든다
- 즉, 각 노드는 앞 뒤의 노드의 위치를 저장한다.