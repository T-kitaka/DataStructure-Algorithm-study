# 이진 탐색(Binary Search)란?

## 1. 이진 탐색 개념

이진 탐색은 **정렬된 배열 또는 리스트에 적합한 고속 탐색 방법**이다.

- 배열의 **중앙값**을 조사하여 찾고자 하는 항목이 **왼쪽** 또는 **오른쪽**에 있는지 확인한다.
- 탐색 범위를 **반으로 줄이는 방식**을 반복하여 원하는 값을 찾는다.
- 찾고자 하는 값이 없는 부분은 고려할 필요가 없으므로, **탐색 속도가 빠르다**.
- 하지만 **삽입이나 삭제가 빈번한 경우에는 부적합**하며, **고정된 데이터 탐색에 적합**하다.
- **이진 탐색을 사용하려면 반드시 정렬된 데이터여야 한다.**

## 2. 이진 탐색 구현

### 2-1. 배열에서 구현

탐색 대상이 `array[low]`에서 `array[high]`까지 들어있다고 가정한다.

1. **초기 범위 설정:**

   - `low = 0`, `high = n - 1`
   - `mid = (low + high) / 2` (정수로 계산)

2. **중앙값과 비교:**

   - `key > array[mid]` → `low = mid + 1` (오른쪽 탐색)
   - `key < array[mid]` → `high = mid - 1` (왼쪽 탐색)
   - `key == array[mid]` → 탐색 성공, `mid` 리턴

3. **반복하여 탐색 수행**

   - `low > high`가 될 때까지 반복

### 📌 예제 설명

#### 🔹 탐색 과정 (예: `key = 32` 찾기)

  ![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcqSVub%2Fbtq5lyj0hdx%2FuueqouAwXkPUcQGJrFgEo0%2Fimg.png)
1. **초기 상태:**
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F3SLNJ%2Fbtq5ffT6iar%2FWLKlWZO792tJTWVVNbXP5K%2Fimg.png)

   - `low = 0`, `high = 9` → `mid = (0+9)/2 = 4`
   - `array[mid] < key` → `low = mid + 1 = 5`

2. **두 번째 탐색:**
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcTdRoI%2Fbtq5fDmvXe8%2F5zi2DU9psPgWYAVaLcZvGK%2Fimg.png)

   - `low = 5`, `high = 9` → `mid = (5+9)/2 = 7`
   - `array[mid] > key` → `high = mid - 1 = 6`

3. **세 번째 탐색:**
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FKjVE5%2Fbtq5gvPmCiP%2FuTyoNRu1MuoKkgXpGb6ckK%2Fimg.png)
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F0vmuK%2Fbtq5gvBOldB%2FxeNJojg5kJyJpFNi3jL3t1%2Fimg.png)

   - `low = 5`, `high = 6` → `mid = (5+6)/2 = 5`
   - `array[mid] == key` → 탐색 성공 🎯



### 2-2. 반복문 & 재귀함수 구현

#### ✅ **반복문 방식** (메모리 효율적, 속도 빠름)

```java
public static int binarySearch(int[] arr, int target) {
    int low = 0, high = arr.length - 1;
    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (arr[mid] == target) return mid;
        else if (arr[mid] < target) low = mid + 1;
        else high = mid - 1;
    }
    return -1;
}
```

#### ✅ **재귀 방식** (직관적이지만 메모리 사용 多)

```java
public static int binarySearch(int[] arr, int low, int high, int target) {
    if (low > high) return -1;
    int mid = low + (high - low) / 2;
    if (arr[mid] == target) return mid;
    else if (arr[mid] < target) return binarySearch(arr, mid + 1, high, target);
    else return binarySearch(arr, low, mid - 1, target);
}
```

## 3. 종료 조건 & 시간 복잡도

### **🔹 종료 조건**

1. `array[mid] == key` → 탐색 성공
2. `low > high` → 탐색 실패

### **🔹 시간 복잡도**

- **최선의 경우 (O(1))**: 한 번에 중앙값이 정답인 경우
- **평균 & 최악의 경우 (O(log N))**: 탐색할 때마다 범위를 절반으로 줄이므로 **로그 시간 복잡도**를 가짐

## 4. 이진 탐색 트리 (BST)

이진 탐색 트리는 이진 탐색을 **효율적으로 수행할 수 있도록 설계된 자료구조**이다.

- **왼쪽 서브트리**: 부모 노드보다 작은 값
- **오른쪽 서브트리**: 부모 노드보다 큰 값

![](https://blog.kakaocdn.net/dn/ec9EZD/btqAOcsCkwF/6Q5kGtpUf6uiwgpDuxZ0jk/img.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FuDHQH%2FbtqAOcMY6EB%2Fvyb3LZDCgyiAlisXBcngu0%2Fimg.png)



### 4-1. 삽입 & 삭제 연산

#### ✅ **삽입 연산**

- 새로운 노드를 삽입할 때, BST의 규칙을 유지하도록 적절한 위치에 추가
- 탐색을 수행하며 **왼쪽 또는 오른쪽으로 이동하여 삽입**
![](https://hyeminnoh.github.io/Tech-Stack/assets/img/binarytree_add.7b47550b.jpg)

#### ✅ **삭제 연산**

1. **삭제할 노드가 리프(자식이 없는 경우)** → 바로 삭제
2. **삭제할 노드가 자식이 1개인 경우** → 삭제 후 자식 노드로 대체
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcBBe0S%2FbtqARx22gTs%2FzZkp7WaE93K2DMDyWV8N20%2Fimg.png)
3. **삭제할 노드가 자식이 2개인 경우** →
   - 왼쪽 서브트리의 **최대값** 또는 오른쪽 서브트리의 **최소값**으로 대체 후 삭제
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcqTzsm%2FbtqAQ39bwci%2FkZ7KJshiWY9t0VkB4weW5K%2Fimg.png)

4-2. 삽입 & 삭제가 필요한 이유

삽입 & 삭제가 빈번한 경우 이진 탐색 연산이 적합하지 않다고 했는데 이진 탐색 트리에서 삽입 & 삭제가 가능한 이유는 다음과 같다.

이진 탐색 트리의 특성상 노드의 값은 항상 정렬된 상태를 유지한다.

하지만 실제 애플리케이션에서는 데이터가 정적이지 않고 동적으로 변경될 수 있다. 예를 들어, 새로운 데이터를 추가하거나 기존 데이터를 삭제해야 할 수도 있다.

이 경우 이진 탐색 트리에서 삽입과 제거 연산이 필요하며, 트리의 구조를 유지하면서도 동적인 데이터 변경을 지원할 수 있도록 설계되었다.

즉, 이진 탐색 트리는 정렬된 데이터에 대한 효율적인 검색을 지원하는 동시에, 삽입과 삭제 연산도 가능하도록 설계된 자료 구조이다.

반면, 배열은 삽입 & 삭제가 발생할 시 다시 정렬해야 하기 때문에 성능이 저하된다. 따라서 배열은 검색 연산이 중요하고, 이진 탐색 트리는 삽입 & 삭제도 유연하게 처리할 수 있다는 점이 가장 큰 차이점이다.



## 5. 이진 탐색 변형 알고리즘

- **Lower Bound**: 찾고자 하는 값 이상 중 가장 작은 값 찾기
- **Upper Bound**: 찾고자 하는 값 초과 중 가장 작은 값 찾기
- **Ceiling**: 찾고자 하는 값 이상 중 최소 값 찾기
- **Floor**: 찾고자 하는 값 이하 중 최대 값 찾기

---

