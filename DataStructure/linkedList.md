# 연결리스트 (LinkedList)

## 1. 연결 리스트란?

앞서 공부한 배열은 구현이 간단하다는 장점이 있지만, 용량이 고정된다는 단점이 있다는 것을 알았다.

삽입과 삭제를 매우 자주 해야 하는 상황이면 배열은 비효율적인데, 이 때 나온 것이 **연결 리스트**라는 새로운 자료구조이다. 

연결리스트는 어떠한 데이터를 저장할 때, 그 다음 순서의 자료가 있는 위치를 데이터에 포함시키는 방식의 자료구조이다. 

연결리스트는 노드로 이루어져 있고, 각 노드는 데이터를 저장하는 데이터 필드와 다른 노드를 가리키는 참조 필드로 구성된다. 

즉, 연결 리스트란 노드가 여러 개 모여서 만들어지는 하나의 구조라고 할 수 있다.

<img src="https://github.com/user-attachments/assets/7c039a24-2370-487a-8bf4-b315366535b2" width="70%" height="50%" title="연결리스트1" alt="연결리스트1"></img>

위 그림과 같이 데이터 필드에는 값이 들어가고, 참조 필드에는 다음으로 연결된 노드의 주소가 저장된다.

<br>

이러한 연결 리스트의 종류로는 `단일 연결리스트`, `이중 연결리스트`, `원형 연결리스트` 3가지가 있다.

<br>
<br>

## 2. 연결리스트의 시간 복잡도

연결 리스트 사용 시 탐색은 느리지만, `삽입과 삭제 연산은 매우 빠르기 때문`에 삽입과 삭제가 잦은 상황에서 자주 사용한다.

| 종류 | 시간복잡도 | 설명 |
| --- | --- | --- |
| 접근 | O(n) | 인덱스 x에 있는 노드에 접근하려면 Head에서 다음 노드로 x번 이동하면 된다. |
| 탐색 | O(n) | 가장 앞 노드부터 다음 노드를 하나씩 보면서 원하는 데이터를 가진 노드를 찾는다. 노드가 n개 있다면 최악의 경우 시간 복잡도는 O(n) |
| 삽입, 삭제 | O(1) | 삽입, 삭제할 노드의 주변 노드들이 참조하는 연결만 수정해주면 된다. 따라서 삽입, 삭제가 실행되는 시간은 **항상 일정** |

** 삽입, 삭제가 O(1)인 것은 탐색을 제외하고 삽입, 삭제의 행위 그 자체만 고려하였을 때의 시간 복잡도이다.

<br>
<br>

## 3. 연결 리스트의 장단점

### 장점

- **삽입 및 삭제**: 데이터의 삽입과 삭제가 용이하다.
- **동적 크기**: 동적으로 크기를 변경할 수 있다.
- **메모리 효율성**: 필요한 만큼의 메모리만 할당하므로, 메모리의 효율적인 사용이 가능해진다.

### 단점

- **접근 시간**: 특정 요소에 접근하기 위해서는 최악의 경우 리스트 전체를 순회해야 할 수도 있다.
- **추가적인 메모리 사용**: 각 요소마다 다음 요소를 가리키는 포인터가 필요하기 때문에, 추가적인 메모리 사용이 발생한다.


<br>
<br>

## 4. 단일 연결리스트

단일 연결리스트는 연결 방향이 단방향인 가장 기본적인 형태의 연결 리스트이다.

![Image](https://github.com/user-attachments/assets/1187accf-7526-42db-b317-b49f557580f6)

연결 리스트의 첫 번째 값을 알기 위해 우리는 연결 리스트의 첫 번째 값에 head라고 명시해주며, 마지막 값에는 Tail 이라고 명시할 수 있다.

탐색은 첫 노드(head)부터 순차적으로 이루어지게 된다

<br>

### 4.1 단일 연결리스트의 삽입

<img width="734" alt="Image" src="https://github.com/user-attachments/assets/cbea2778-a4b9-499c-bf8c-d325105b81a9" />
<img width="734" alt="Image" src="https://github.com/user-attachments/assets/0d5955f5-43f7-45a8-a524-819224bc1dc5" />

<br>
<br>

원하는 위치에 노드를 삽입하기 위해서는 다음과 같은 과정을 거친다.

1. 새 노드를 생성한다.
2. 삽입할 위치의 이전 노드를 찾아준다.
3. 새 노드가 이전 노드가 가리키고 있던 다음 노드를 가리키게 한다.
4. 이전 노드는 새 노드를 가리키게 한다.

<br>

### 4.2 단일 연결리스트의 삭제

<img width="734" alt="Image" src="https://github.com/user-attachments/assets/3eb4a372-bb42-456d-80a9-f59f661bf0d3" />
<img width="734" alt="Image" src="https://github.com/user-attachments/assets/081c85dc-060c-4bcf-abc5-36c2ca7fc95b" />

<br>
<br>

원하는 노드를 삭제하기 위해서는 다음과 같은 과정을 거친다.

1. 삭제할 노드의 이전 노드를 찾는다.
2. 이전 노드가 삭제할 노드의 다음 노드를 가리키게 한다.
3. 삭제할 노드를 메모리에서 해제한다.

<br>
<br>

## 5. 이중 연결리스트

이중 연결리스트는 연결 방향이 양방향으로 연결되어 있어 노드가 서로를 가리키고 있는 구조이다.

<img width="642" alt="Image" src="https://github.com/user-attachments/assets/03c663fc-c5e2-470d-8008-ca805fe31926" />


맨 앞에 있는 노드는 head가 되고 맨 끝에 있는 노드를 tail이라고 추가적으로 명시해주게 된다면, 탐색 시 좀 더 효율적으로 탐색을 할 수 있게된다.

단일 연결리스트에서 추가적으로 반대 방향에 있는 노드를 가리키는 것 이외에는 큰 차이가 없다.

<br>

### 5.1 이중 연결리스트의 삽입

<img width="734" alt="Image" src="https://github.com/user-attachments/assets/b3a23bdd-4611-43c5-bf06-ff156ddf8c96" />
<img width="734" alt="Image" src="https://github.com/user-attachments/assets/2294e10a-8f33-4962-918e-e716216dc4df" />


이중 연결리스트의 삽입 과정은 단일 연결리스트와 거의 동일하며 차이점이 있다면, 노드를 삽입할 때 노드 서로가 양방향으로 가리킬 수 있도록 한다.

<br>

### 5.2 이중 연결리스트의 삭제

<img width="734" alt="Image" src="https://github.com/user-attachments/assets/2ba46087-cb99-4639-8db3-b8e48d1ddbfb" />
<img width="734" alt="Image" src="https://github.com/user-attachments/assets/4d78c5c0-8027-4418-bfce-866c37166c58" />


이중 연결리스트의 삭제 또한 단일 연결리스트와 거의 동일하다. 고려할 점은 삭제할 노드가 가리키는 양쪽 방향의 참조를 끊어내주고, 삭제할 노드의 앞 뒤 노드를 양방향으로 참조할 수 있도록 한다.

<br>
<br>

## 6. 원형 연결리스트

원형 연결리스트는 마지막 노드가 다시 앞을 가리키는 구조로 되어있어 원형으로 연결된 리스트이다. 원형으로 연결되어 있기 때문에 데이터 구조를 순환적으로 탐색할 수 있게 해준다.

<img width="580" alt="Image" src="https://github.com/user-attachments/assets/936aa064-ee66-4970-a0ff-69b45e3e4311" />

단일 연결리스트와 이중 연결리스트로 원형 연결리스트를 모두 구현해줄 수 있다.

<br>
<br>

## 7. Java의 LinkedList

자바에서는 기본적으로 LinkedList 클래스를 제공한다. 이는 java.util 패키지에 포함되어 있어 사용하고 싶다면 `import java.util.LinkedList;` 를 해주어야 한다.

자바에서 LinkedList는 **이중 연결 리스트로 구현**되어 있고, List, Deque, Queue와 같은 인터페이스 또한 구현하고 있어 다양한 데이터 구조와 기능을 제공한다.

<br>

### 7.1 LinkedList의 주요 메소드

LinkedList의 메소드는 정말 많지만 그 중 주요한 메소드는 아래와 같다.

| 종류 | 설명 |
| --- | --- |
| addFirst(E) | 맨 앞에 데이터 E를 추가한다. |
| addLast(E) | 맨 뒤에 데이터 E를 추가한다. |
| pollFirst() | 맨 앞에 있는 데이터를 반환하며, 동시에 그 데이터를 list에서 삭제한다. |
| pollLast() | 맨 뒤에 있는 데이터를 반환하며, 동시에 그 데이터를 list에서 삭제한다. |
| size() | 현재 list에 들어있는 데이터의 수를 반환한다. |
| isEmpty() | 현재 list가 비어있으면 true, 아니면 false |
| peekFirst() | 맨 앞에 있는 데이터를 반환한다. |
| peekLast() | 맨 뒤에 있는 데이터를 반환한다. |

<br>

**예시 코드**

```java
import java.util.LinkedList;

public class Main {
    public static void main(String[] args) {
        LinkedList<Integer> l = new LinkedList<>(); //LinkedList 선언 => 빈 이중연결리스트

        l.addFirst(3);                         // 맨 앞에 3을 추가
        l.addFirst(5);                         // 맨 앞에 5를 추가
        System.out.println(l.peekFirst());     // 맨 앞에 적혀있는 숫자인 5가 출력
        System.out.println(l.peekLast());      // 맨 뒤에 적혀있는 숫자인 3이 출력
        l.addLast(9);                          // 맨 뒤에 9를 추가
        System.out.println(l.peekLast());      // 맨 뒤에 적혀있는 숫자인 9가 출력
        l.pollFirst();                         // 맨 앞 숫자(5)를 제거
        System.out.println(l.peekFirst());     // 맨 앞에 적혀있는 숫자인 3이 출력
        System.out.println(l.size());          // 원소의 개수를 출력 => 2
    }
}
```

<br>
<br>

## 8. ArrayList vs LinkedList

우리가 자바에서 자주 사용하는 ArrayList와 LinkedList를 비교해보겠다.

<br>

### 8.1 ArrayList
----------------------------

*ArrayList의 특징*

- 내부적으로 배열을 사용하여 데이터를 저장한다.
- ArrayList는 가변 길이 배열로, 크기를 지정하지 않고 동적으로 값을 삽입하고 삭제할 수 있다.

<br>

*ArrayList의 조회*

-> ArrayList는 각 데이터의 index를 가지고 있고 무작위로 접근이 가능하기 때문에, 해당 index의 데이터를 한번에 가져올 수 있다.

<br>

*ArrayList의 삽입 및 삭제*

-> ArrayList에서 데이터를 삽입하고 싶거나 삭제하고 싶다면 위치를 맞춰주어야 한다.

예를 들어 5개의 데이터가 있는 ArrayList에서 맨 앞의 요소를 삭제했다면, 나머지 뒤에 있던 4개의 요소를 앞으로 한 칸씩 이동해 주어야 한다.

즉, 삽입 및 삭제가 많다면 비효율적이다.

<br>

### 8.2 LinkedList
-------------------------------

*LinkedList의 특징*

- 이중 연결리스트를 사용하여 데이터를 저장한다.
- 각 노드가 데이터와 이전 노드 및 다음 노드에 대한 참조를 가진다.

<br>

*LinkedList의 조회*

-> LinkedList는 순차적 접근이기 때문에 검색의 속도가 느리다.

<br>

*LinkedList의 삽입 및 삭제*

-> LinkedList는 데이터를 삽입, 삭제 시 가리키고 있는 참조값만 변경해주면 되기 때문에 ArrayList에 비해 효율적이다.

<br>

> 정리하자면 소량의 데이터를 가지고 사용할 때는 큰 차이가 없지만, 
>
> 정적인 데이터를 활용하면서 조회가 빈번하다면 ArrayList를 사용하는 것이 좋고, 
>
> 동적으로 삽입, 삭제가 빈번하다면 LinkedList를 사용하는 것이 좋다.
