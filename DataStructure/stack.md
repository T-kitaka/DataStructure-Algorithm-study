# 1. Stack이란?
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FVDUzr%2FbtsiPQL4WVv%2Fp0tPYOEX8J1xj0aokVwttK%2Fimg.png)
<li> 스택은 "쌓다"라는 의미로 데이터를 하나씩 쌓아 올린 형태의 자료구조로, LIFO(Last In First Out) 후입선출 형식의 자료구조이다. 위의 사진처럼 데이터가 순서대로 쌓이며, 가장 마지막에 삽입된 자료가 가장 먼저 삭제되는 구조를 가지고 있다. 
<br>

## 1-1. Java 라이브러리 Stack관련 메소드

<li>pop() : Stack의 가장 윗부분에 있는 자료를 제거한다. 스택이 비어 있을 시 에러가 발생한다.
<li>push(item) : Stack의 가장 윗부분에 item을 추가한다.
<li>peek() : Stack의 가장 윗부분에 있는 데이터를 반환한다.
<li>size() : Stack에 있는 요소 개수를 반환한다.
<li>isEmpty() : Stack이 비어있을 때에 true를 반환한다.
<li>clear() : Stack에 포함된 모든 데이터를 삭제한다.
<li>contatins(int value) : Stack에 값이 있으면 true를 반환한다.

<hr>
위에 메소드를 활용한 예제<br>

```java
    public static void main(String[] args){
        
        Stack<Integer> s = new Stack<>(); //int형  스택 선언

        s.push(5); // 5 추가
        s.push(2); // 2 추가
        s.peek(1); // 2가 가장 나중에 들어갔으니 2 반환
        s.pop(); // 가장 마지막에 들어간 2 제거 & 반환
    }
```

## 1-2. Stack 구현 방법
### 1. 배열 기반 스택 구현

```java
stack = new int[size]; //스택의 크기설정
capacity = size; //스택의 용량
top = -1; //처음에는 비어있음
```
특징: 고정된 크기의 배열을 사용하여 스택을 구현하기 때문에 가득 찼는데 push()하려고하면 Overflow가 발생한다.
<br> 하지만 push() & pop() 연산이 빠르다 시간복잡도 : O(1)

### 2. Stack 클래스 사용

```java
import java.util.Stack;

public class StackExample {
    public static void main(String[] args) {
        Stack<Integer> stack = new Stack<>(); //int형 스택 선언

        // push
        stack.push(10);
        stack.push(20);
        stack.push(30);

        // peek
        System.out.println("Top Element: " + stack.peek()); // 30

        // pop
        System.out.println("Popped: " + stack.pop()); // 30

        // isEmpty
        System.out.println("Is stack empty? " + stack.isEmpty()); // false

        // size
        System.out.println("Stack Size: " + stack.size()); // 2
    }
}
```
특징 : Java에서 제공하는 Java.util.Stack<T> 클래스를 사용한다. 내부적으로 Vector클래스를 상속하기에 Thread-Safe하다.
<br> push() & pop() 모두 시간복잡도 : O(1)

### 3. List활용 

![](https://blog.kakaocdn.net/dn/dZoWKB/btq5g5oMG07/5trCuDegjPwHtB7kdTUmkk/img.png)

```java
class Node {
    int data; //노드를 저장할 데이터
    Node next; // 다음 노드를 가리키는 포인터

    public Node(int data) {
        this.data = data;
        this.next = null; //새 노드는 기본적으로 다음 노드를 가리키지 않는다.
    }
}

class LinkedListStack {
    private Node top; //스택의 최상단 노드를 가리키는 포인터
    private int size; // 스택의 크기(현재 저장 요소)

    public LinkedListStack() {
        this.top = null; //처음에는 top 없음
        this.size = 0; //초기 크기는 0
    }

    // 스택이 비었는지 확인
    public boolean isEmpty() {
        return top == null; //top이 null이면 스택이 비어있음
    }

    // push 연산
    public void push(int item) {
        Node newNode = new Node(item); //노드 생성
        newNode.next = top; //새 노드의 다음을 top이 가리키는 노드로 설정
        top = newNode; //top을 새 노드로 변경
        size++; //크기 증가
    }

    // pop 연산
    public int pop() {
        if (isEmpty()) {
            System.out.println("Stack Underflow! 스택이 비어 있습니다.");
            return -1;
        }
        int poppedData = top.data; //top데이터 저장
        top = top.next; //top데이터를 다음 노드로 변경
        size--; //크기 감소
        return poppedData;
    }

    // peek 연산
    public int peek() {
        if (isEmpty()) {
            System.out.println("스택이 비어 있습니다.");
            return -1;
        }
        return top.data;
    }

    // 스택 크기 반환
    public int size() {
        return size;
    }

    public static void main(String[] args) {
        LinkedListStack stack = new LinkedListStack();
        stack.push(10);
        stack.push(20);
        stack.push(30);
        System.out.println("Top Element: " + stack.peek()); // 30
        System.out.println("Popped: " + stack.pop()); // 30
        System.out.println("Stack Size: " + stack.size()); // 2
    }
}

```

## 1-3. Java에서 Stack 특징
<ol>
<li> Java에서 Stack 클래스는 Vector 클래스를 상속받기에 Thread-Safe하다는 특징을 가지고 있다.

<li> Thread-Safe : 멀테스레드 환경에서 여러 개의 스레드가 동시에 접근해도 데이터가 꼬이지 않도록 하는것
                    즉 여러개의 스레드가 동시에 push(), pop()을 진행해도 데이터 손실 없이 동작한다는 것이다.

<li> Vector 클래스는 모든 메서드가 synchronized 되어 있어, 한 번에 하나의 스레드만 실행할 수 있도록 보장됨.

<br>

**synchronized : 여러 스레드가 동시에 실행하려고 하면 한 개의 스레드만 접근하도록 하는 것**

<li> Stack 클래스의 경우 ArrayList처럼 동적 공간이라 별도의 사이즈를 명시하지 않아도 된다. 처음 스택이 생성되었을때 10개의 데이터를 저장할 수 있는 공간이 할당이 된다. push()를 통해 데이터 10개가 넘어가면, 현재 스택 사이즈의 2배에 해당하는 공간을 할당하고 기존 데이터를 복사한다.
<hr>

## 1-4. Stack의 장점과 단점
>장점
- 빠른 연산 속도, push(), pop()연산이 O(1)의 시간복잡도를 가진다. 중간에 삽입/삭제하는 연산이 없어 처리 속도가 빠르다.
- 구현이 간단하다 : 배열, 연결 리스트로 쉽게 구현이 가능하다.
- 필요할 때만 메모리를 할당하기때문에 메모리를 효율적으로 사용한다.
>단점
- 데이터의 접근이 제한적이다 : 맨 위(top) 요소만 접근이 가능하다.
- 크기제한이 발생할 수 있다. : 배열 기반 스택의 경우 고정 크기를 가지므로 초기 크기 설정이 중요하다.
- 특정 요소를 찾으려면 pop()을 계속 수행해야 하기 때문에 데이터 검색이 비효율적이다.  
