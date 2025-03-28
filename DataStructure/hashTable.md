# 1. 해시 테이블이란?

**(Key, Value)로 데이터를 저장하는 자료구조입니다.**

### 특징

- 내부적으로 배열을 사용해서 데이터를 저장함
- Key값에 해시함수를 적용해 고유한 index를 생성함

장점

- 빠른 검색 속도: 한번만 조회하면 됨
- O(1)의 속도

단점

- 순서를 보장하지 않음
- 데이터가 pseudo-random(유사 난수) 위치에 저장되기 때문에 데이터를 정렬된 순서로 접근 할때 비용이 높다
- 반목문을 돌면서 탐색하는 능력이 떨어짐
    - 빈 버킷도 순회하기 때문

### 예시

![iamge](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb1zOw1%2FbtqL6HAW7jy%2FjpBA5pPkQFnfiZcPLakg00%2Fimg.png)

| Key | Value |
| --- | --- |
| `John Smith` | `“521-1234”`  |
| `Lisa Smith`  | `“521-8976”` |
| `Sandra Dee`  | `“521-9655”` |

---

### 해시란?

![image.png](https://velog.velcdn.com/images/colorful8315/post/73ddda9f-1a4a-4bd3-8998-5c3e50883424/image.png)

> 다양한 길이를 가진 데이터를 고정된 길이를 가진 데이터로 매핑
>단, 하나의 글자만 바뀌더라도 전혀다른 데이터로 바뀜
 
>`”안녕하세요”` → 해시 함수(`”안녕하세요”`) →  해시 값 : `AFDID&SDJKFJKSNK342`

>`”안녕하세요!”` → 해시 함수(`”안녕하세요!”`) →  해시 값 : `dofkaopk3@dkkfsl3`

---

해시값을 이용해서 `index`를 생성한 후, 이 `index`을 통해 해시 테이블에 `Value`를 저장합니다.

예를 들어 `John Smith` 의 길이가 16이라고 해봅시다.
그러면 다음과 같은 연산이 돌아갑니다.

```java
// Division Method
index = hash_function("John Smith") % 16;
arr[index] = “521-1234”;
```

이런씩으로 `index` 구하고 해시테이블에 넣습니다.

### Hash 함수(해시 함수)

대표적인 해시 함수는 3가지가 있습니다.

1. Division Method: 나눗셈을 이용하는 방법

   입력값을 테이블의 크기로 나누어 게산합니다. (주소 = 입력값 % 테이블의 크기)

2. Digit Method: ASCII 코드로 바꾸는 방법

   Key의 문자열을 ASCII 코드로 바꾸고 값을 합한 데이터를 테이블 내의 주소를 사용합니다.

3. Univeral Hashing: 무작위 해시함수를 사용하는 방법

   여러개의 해시함수를 집합에 넣어둔 뒤 무작위로 사용하는 방식


---

# 2. 해시값 충돌

Key값을 돌리다 같은 해시값이 나올수도 있습니다.

그러면 크게 두가지 방법이 있습니다.

`분리 연결(Separate Chaining)`, `개방 주소법(Open Addressing)` 입니다.

### 분리 연결법

![image.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbTF67c%2FbtqL7xx3OGw%2FDM8KEKU5x7dx6Nks4JR7K1%2Fimg.png)

같은 해시값이 나오면 추가 메모리 사용해서 전 데이터의 다음 주소에 저장하는 방식입니다.
위의 그림을 보시먄 동일한 버킷에 접근을 한다면 2개의 데이터가 연결된 모습입니다.

- 장점

  해시 테이블을 확장할 필요없이 간단히 구현 가능, 손쉽게 삭제도 가능합니다.

- 단점

  데이터의 수가 많아지면 동일한 버킷에 연결된(chaining)되는 데이터가 많아지면 캐시의 효율성이 떨어집니다.


>Java8의 Hash테이블은 Self-Balancing Binary Search Tree(**자가 균형 이진 탐색 트리**) 자료구조를 사용해 Chaining 방식을 구현하였다.
>

### 개방 주소법

추가적인 메모리를 사용하지 않고 비어있는 해시 테이블을 활용하는 방법입니다.

1. 선형 프로빙(Linear Probing): 중복된 해시값 위치에서 고정폭 만큼 이동해서 비어 있는 버킷에 데이터를 저장하는 방식
2. 이차 초사(Quadratic Probing): 저장순서를 제곱으로 저장하는 방식
    1. 충돌! → 1만큼 이동 후 저장 → 2차 충돌! → 2^2 만큼 이동 후 저장 →  3차 충돌! → 2^3 ...
3. 이중 해싱(Double Hashing Probing): 해시된 값을 또 해시하는 방식입니다.
    1. 다른 방법보다 많은 연산이 필요함

![image.png](https://ajroot5685.github.io/assets/img/240419/linear,%20quardratic.png)

---

# 3. 해시테이블 시간 복잡도

추후 알고리즘을 풀게 된다면 `Big-O`라는 개념을 배워야 되지만 간단히 설명하겠습니다. (이미 아는 개념이면 넘어가시면 됩니다)

![image.png](https://images.velog.io/images/gillog/post/1506c01a-ba40-4255-b549-03c8bb038049/1.png)

O(1), O(log n) → O(n) → O(n log n) → O(n^2) → O(2^n) → O(n!)

> 메서드 A는 한 번 실행될 때 O(N) 연산을 수행한다. (예: N=10일 때 10번 연산)
메서드 B는 한 번 실행될 때 O(N²) 연산을 수행한다. (예: N=10일 때 100번 연산)
>

헷갈리시면 그냥 아주 빠르게 돌아가는 프로세스라고 생각해주시면 됩니다.

---

해시테이블은 조회 하는 평균 시간복잡도가 `O(1)` 입니다. 
하지만 데이터의 충돌이 일어나면 연결된 리스트들까지 검색을 해야되니 `O(N)`까지 시간복잡도가 증가할 수 도 있습니다.
한마디로 공간을 많이 사용하면 치명적인 단점이 발생합니다.
그리고 또 테이블이 꽉차면 확장시켜야 되며 이런 경우에도 심각한 성능 저하가 발생합니다.

> 테이블의 공간 사용률이 70% ~ 80%가 되면 점점 성능이 저하됨
>

효율적으로 해시테이블을 사용하는 방법: 자주 사용하는 데이터을 해시테이블에 적용하면 효율이 좋습니다. 바로바로 찾아서 바로 적용할 수 있기 때문입니다.

---

# 4. JAVA에서 비슷한 자료구조 HashMap, HashTable

둘다 비슷한 자료구조로 ket, value방식으로 저장됩니다.

차이점이 뭘까요?

해시 테이블

```java
public synchronized V put(K key, V value) {
	...
}
```

해시 맵

```java
public V put(K key, V value) {
	...
}
```

`synchronized`라는 키워드가 있고 없고의 차이점입니다

`병렬 처리`를 하면서 자원의 동기화를 고려해야되는 상황이면 해시테이블(HashTable)을 사용,

`병렬 처리`를 하지 않거나 자원의 동기화를 고려하지 않은 상황이라면 해시맵을 사용하면 됩니다.

**synchronized**

`int data = 0;`라는 변수가 있을 때, 두 개의 스레드가 이 변수에 접근한다고 가정해봅시다.

- **스레드 1**: `data++` 연산을 수행합니다.
- **스레드 2**: `data = 0`으로 초기화합니다.

이 두 스레드가 동시에 실행되면, `data`의 최종 값은 예측할 수 없습니다. 왜냐하면 두 스레드가 동시에 `data`에 접근하므로, 실행 순서에 따라 결과가 달라질 수 있기 때문입니다.

하지만 **synchronized** 키워드를 사용하면, 예를 들어 `스레드 1`이 먼저 `data++`를 실행하면 `스레드 2`는 그 이후에야 `data = 0`을 실행하게 됩니다.

즉, `스레드 1`이 작업을 끝낸 후에 `스레드 2`가 동작을 시작하므로, 두 스레드가 동시에 `data`에 접근하는 것을 막을 수 있습니다.

다만, `synchronized`를 남용하면 성능 저하가 발생할 수 있습니다. 이는 한 스레드가 `synchronized` 블록에 진입하면 다른 스레드는 기다려야 하기 때문에 병렬 처리의 효율성이 떨어지기 때문입니다.