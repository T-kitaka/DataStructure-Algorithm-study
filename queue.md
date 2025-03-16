# 1. 큐(Queue)
## 1.1. 큐의 개념과 특징
![](https://velog.velcdn.com/images/hueyjeong/post/41b4b5e2-81ab-4dc1-beac-fce5b8fa7587/image.png)

큐는 먼저 들어간 데이터를 먼저 내보내는(First In First Out, FIFO)  자료구조이며 일반적으로 배열이나 연결리스트로 구현된다. 이를 포함한 특징은 다음과 같다.
* 선입선출(FIFO) : 먼저 들어간 데이터가 먼저 나온다. 
* 제한된 접근 : 데이터는 뒤(rear)에서 삽입(Enqueue)되고 앞(front)에서 삭제(Enqueue)되며 중간의 데이터는 삭제나 수정을 할 수 없다.
* 구현 방식 : 배열, 연결리스트 등으로 구현하고, 경우에 따라 원형 큐(Circular Queue) 형태로 공간 효율성을 높인 경우도 있다.
* 활용 : 순차적인 처리가 필요한 곳(예: 프로세스 스케쥴링, 버퍼 등)에 활용된다.
---
## 1.2. 큐의 구현
* **생성자와 구조**
```java
public class MyQueue<T> {
    private final T[] array;
    private int front = 0;
    private int rear = 0;

    public MyQueue(Class<T> clazz, int capacity) {
        // java에서 new T[capacity]는 지원되지 않음.
        array = (T[]) java.lang.reflect.Array.newInstance(clazz, capacity);
    }
    public boolean enqueue(T item);
    public T dequeue();
    public boolean isEmpty();
}
```
![](https://velog.velcdn.com/images/hueyjeong/post/3a384e07-8ac3-4706-9aee-e9cc795e0e63/image.png)

* **Enqueue**
```java
    public boolean enqueue(T item) {
        if (rear == array.length) // full일 때 false를 반환
            return false;
        array[rear++] = item;
        return true;
    }
```
![](https://velog.velcdn.com/images/hueyjeong/post/9cfb5766-3e49-4c23-a8aa-f676abc41691/image.png)
![](https://velog.velcdn.com/images/hueyjeong/post/f8ed66b3-931c-4266-a516-a53adc9a13ae/image.png)

* **Dequeue**
```java
    public T dequeue() {
        if (front == rear) // 비어 있을 때 null을 반환
            return null;
        return array[front++];
    }
```
![](https://velog.velcdn.com/images/hueyjeong/post/f0ad6ff3-6b17-4d9d-8c5e-829a9ed9df2c/image.png)
![](https://velog.velcdn.com/images/hueyjeong/post/dc9555ce-5ab0-4b46-85d2-68984eeaab8e/image.png)

* **IsEmpty**
```java
    public boolean isEmpty() {
        return front == rear; // front와 rear가 같으면 비어있다.
    }
```
![](https://velog.velcdn.com/images/hueyjeong/post/2c42bd81-ad5a-48df-961c-2e8d5964de79/image.png)

* **Clear**
```java
    public void clear() {
        front = 0; // front와 rear을 0으로 되돌려 재사용 가능하게 함
        rear = 0;
    }
```
![](https://velog.velcdn.com/images/hueyjeong/post/80f15edb-bc21-4065-b891-7d0b4593b442/image.png)

---
## 1.3. 자바에서의 큐

자바에서 `Queue`는 인터페이스로 요소를 추가할 수 있는 메서드와 반환하고 삭제하는 메서드, 반환하고 삭제는 하지 않는 메서드, 상태를 알려주는 메서드로 구성된다.

### 1. **`add(E e)`**
*  **설명:** 큐의 **뒤쪽**에 요소를 추가한다. 큐가 가득 차면 `IllegalStateException`을 발생시킨다.
*  **예외:** 큐가 가득 차면 예외 발생.

   ```java
   boolean add(E e);
   ```

### 2. **`offer(E e)`**
*  **설명:** 큐의 **뒤쪽**에 요소를 추가한다. 큐가 가득 차면 `false`를 반환하고 예외는 발생하지 않는다.
*  **예외:** 예외 발생하지 않음. 큐가 가득 차면 `false` 반환.

   ```java
   boolean offer(E e);
   ```

### 3. **`remove()`**
*  **설명:** 큐에서 **앞쪽** 요소를 제거하고 반환한다. 큐가 비어 있으면 `NoSuchElementException`을 발생시킨다.
*  **예외:** 큐가 비어 있으면 예외 발생.

   ```java
   E remove();
   ```

### 4. **`poll()`**
*  **설명:** 큐에서 **앞쪽** 요소를 제거하고 반환한다. 큐가 비어 있으면 `null`을 반환한다.
*  **예외:** 큐가 비어 있으면 `null` 반환.

   ```java
   E poll();
   ```

### 5. **`peek()`**
*  **설명:** 큐의 **앞쪽** 요소를 반환하지만 제거하지는 않는다. 큐가 비어 있으면 `null`을 반환한다.
*  **예외:** 큐가 비어 있으면 `null` 반환.

   ```java
   E peek();
   ```

### 6. **`element()`**
*  **설명:** 큐의 **앞쪽** 요소를 반환하지만 제거하지 않는다. 큐가 비어 있으면 `NoSuchElementException`을 발생시킨다.
*  **예외:** 큐가 비어 있으면 예외 발생.

   ```java
   E element();
   ```

### 7. **`size()`**
*  **설명:** 큐에 있는 요소의 개수를 반환한다.
*  **예외:** 예외 발생하지 않음.

   ```java
   int size();
   ```

### 8. **`isEmpty()`**
*  **설명:** 큐가 비어 있으면 `true`를 반환하고, 그렇지 않으면 `false`를 반환한다.
*  **예외:** 예외 발생하지 않음.

   ```java
   boolean isEmpty();
   ```

### 9. **`clear()`**
*  **설명:** 큐의 모든 요소를 제거한다.
*  **예외:** 예외 발생하지 않음.

   ```java
   void clear();
   ```

---

### 요약

| 메서드          | 설명                                                    | 예외 상황 |
|-----------------|---------------------------------------------------------|----------|
| `add(E e)`      | 큐의 뒤쪽에 요소를 추가 (가득 차면 예외 발생)             | `IllegalStateException` |
| `offer(E e)`    | 큐의 뒤쪽에 요소를 추가 (가득 차면 `false` 반환)         | 예외 없음 |
| `remove()`      | 큐의 앞쪽 요소 제거 후 반환 (큐 비어 있으면 예외 발생)     | `NoSuchElementException` |
| `poll()`        | 큐의 앞쪽 요소 제거 후 반환 (큐 비어 있으면 `null` 반환)   | 예외 없음 |
| `peek()`        | 큐의 앞쪽 요소 반환 (제거하지 않음, 큐 비어 있으면 `null` 반환) | 예외 없음 |
| `element()`     | 큐의 앞쪽 요소 반환 (제거하지 않음, 큐 비어 있으면 예외 발생) | `NoSuchElementException` |
| `size()`        | 큐에 있는 요소의 개수 반환                               | 예외 없음 |
| `isEmpty()`     | 큐가 비어 있으면 `true` 반환                            | 예외 없음 |
| `clear()`       | 큐의 모든 요소를 제거                                   | 예외 없음 |

`Queue` 인터페이스는 큐의 기본 동작을 정의할 뿐 구현하지 않는다. 그렇기 때문에 다음과 같은 구현체들을 사용해야한다.

* **LinkedList**
  * **특징:** 
    * **연결리스트**로 구현한 큐.
    *  `List` 인터페이스도 구현하는 동시에 `Queue` 인터페이스도 구현한다.
    *  양쪽 끝에서의 삽입과 삭제가 효율적이다.

* **ArrayDeque**
  * **특징:**
     *  배열로 구현한 큐, **Deque**(Double Ended Queue) 인터페이스를 동시에 구현한다.
     *  스택과 큐 모두로 활용 가능하며, 메모리 재할당 없이 효율적인 연산이 가능하다.
     * 빠른 성능이 요구되는 큐나 스택 구현 시 사용한다.

이 외에도 우선순위를 가진 **Priority Queue**, **Thread-Safe**한 큐 구현체들이 존재한다.

---
