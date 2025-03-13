# 힙(heap)

힙(Heap)은 **최대값 또는 최소값을 빠르게 찾기 위해 설계된 완전이진트리(Complete Binary Tree) 기반의 자료구조**이다.

우선순위 큐(Priority Queue)와 밀접한 관련이 있으며, **우선순위 큐를 구현하는데 자주 사용된다.**

## 힙 종류

- 최대 힙
- 최소 힙

### 최대 힙(Max Heap)

![Image](https://github.com/user-attachments/assets/76ca3f52-ef76-484b-ba91-a65f179ca064)

- 부모 노드의 키 값이 자식 노드의 키 값보다 항상 큰 힙
- 즉, 루트 노드가 가장 큰 값을 가진다.
- 왼쪽, 오른쪽 자식 노드끼리는 크기 관계가 없다.

```java
import java.util.PriorityQueue;
import java.util.Collections;

public class MaxHeapExample {
    public static void main(String[] args) {
        // 최대 힙 구현 (내림차순 Comparator 사용)
        PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());

        // 요소 삽입
        maxHeap.add(10);
        maxHeap.add(30);
        maxHeap.add(20);
        maxHeap.add(5);

        // 최대 힙 요소 출력 (가장 큰 값부터)
        while (!maxHeap.isEmpty()) {
            System.out.println(maxHeap.poll()); // 30 → 20 → 10 → 5
        }
    }
}
```

- PriorityQueue<Integer> : 최대 힙을 구현
- Collections.reverseOrder() : 내림차순 정렬
- poll() : 호출할 때마다 **가장 큰 값이 제거**
- 출력 결과

```java
30  
20  
10  
5  
```

### 최소 힙(Min Heap)

![Image](https://github.com/user-attachments/assets/95cda4ba-36ba-4588-ad29-39c2290bbe24)

- 부모노드의 키 값이 자식 노드의 키 값보다 항상 작은 힙
- 즉, 루트 노드가 가장 작은 값을 가진다.
- 형제 노드끼리는 크기 관계가 없다.

```java
import java.util.PriorityQueue;

public class MinHeapExample {
    public static void main(String[] args) {
        // 기본적으로 PriorityQueue는 최소 힙을 지원함
        PriorityQueue<Integer> minHeap = new PriorityQueue<>();

        // 요소 삽입
        minHeap.add(10);
        minHeap.add(30);
        minHeap.add(20);
        minHeap.add(5);

        // 최소 힙 요소 출력 (가장 작은 값부터)
        while (!minHeap.isEmpty()) {
            System.out.println(minHeap.poll()); // 5 → 10 → 20 → 30
        }
    }
}

```

- PriorityQueue<Integer> : 자동 최소 힙 유지
- poll() : 호출할 때마다 **가장 작은 값이 제거**
- 출력 결과

```java
5  
10  
20  
30  
```

### 힙 특징

- 키 값의 대소관계는 오로지 부모노드와 자식 노드 간에만 성립
- 특히 형제 사이에는 대소 관계가 정해지지 않는다.
- 각 노드의 자식 노드의 최대 개수는 힙 종류에 따라 다르지만 대부분의 경우는 자식 노드의 개수가 최대 2인 이진 힙(binary heap)을 사용한다.
- 힙에서는 가장 높거나 낮은 우선 순위를 가지는 노드가 항상 뿌리노드에 오게 되는 특징이 있다. → 이를 응용하면 우선순위 큐와 같은 추상적 자료형을 구현할 수 있다.

## 완전이진트리와 힙의 차이

### 완전이진트리

- 모든 노드가 왼쪽에서부터 차례대로 채워지는 트리 형태
- 부모-자식 간의 크기 관계는 없다.
- 마지막 레벨을 제외한 모든 레벨이 노드로 가득 차 있어야 한다.

### 힙

- 완전 이진 트리 기반으로 부모-자식 간 크기 관계를 유지하는 자료구조
- 최대 힙은 부모가 자식보다 크고, 최소 힙은 부모가 자식보다 작다

즉, 완전이진트리는 형태적 특징만을 의미하지만, 힙은 추가적인 정렬 조건을 만족해야 한다!

### 힙의 시간 복잡도

- 힙은 트리 구조이므로 삽입과 삭제가 O(log N)이다.
- 최대값이나 최솟 값은 항상 루트에 위치 하므로 조회하는 연산이 O(1)으로 빠르다.

## **힙의 데이터 저장/삭제 개념**

### 최소 힙에서 저장될때

![Image](https://github.com/user-attachments/assets/d91804a9-8469-4e1b-89c9-fc5cdccf2c62)

- 새로운 노드를 마지막 노드 위치에 삽입
- 부모 노드와 비교하여 크기가 더 작으면 교환(상향 조정)
- 루트까지 이동하며 올바른 위치를 찾음

### 최소 힙에서 삭제할 때

![Image](https://github.com/user-attachments/assets/98f006b0-1355-4488-b20b-057855c5560c)

- 루트 노드 삭제
- 마지막 노드를 루트로 이동
- 자식 노드와 비교하여 작은 값과 교환 수행
- 교환을 반복하면서 올바른 위치를 찾는다.

### 최대 힙에서 저장될 때

![Image](https://github.com/user-attachments/assets/30a68d6a-16a8-4e26-b51f-ad03a62a894b)

- 새로운 노드를 삽입하면 마지막 위치에 추가
- 부모 노드와 비교하여 크기가 더 크면 교환(상향 조정)
- 루트까지 이동하여 올바른 위치는 찾는다.

### 최대 힙에서 삭제할 때

![Image](https://github.com/user-attachments/assets/599192a7-3e48-4719-b120-e32bdb30fdf4)

- 루트 노드 삭제
- 마지막 노드를 루트로 이동
- 자식 노드와 비교하여 큰 값과 교환
- 교환을 반복한면서 올바른 위치는 찾는다.

## 배열(Array) 기반 힙 구현

- 배열을 사용하여 힙을 표현하면 **트리 구조를 1차원 배열로 변환**
- 이 방식에서는 **부모-자식 간 인덱스 관계**를 이용하여 빠르게 접근할 수 있다.

### 배열 인덱스를 이용한 부모-자식 관계

부모 노드 인덱스 = i

| 왼쪽 자식 노드 | 2 * i + 1 |
| --- | --- |
| 오른쪽 자식 노드 | 2 * i + 2 |
| 부모 노드 | (i - 1) / 2 |

### 배열 기반 힙 구현(Java)

```java
import java.util.Arrays;

class ArrayHeap {
    private int[] heap;
    private int size;
    private int capacity;

    public ArrayHeap(int capacity) {
        this.capacity = capacity;
        this.heap = new int[capacity];
        this.size = 0;
    }

    // 요소 삽입 (Heapify-Up)
    public void insert(int value) {
        if (size == capacity) {
            System.out.println("힙이 가득 찼습니다!");
            return;
        }
        heap[size] = value;
        int index = size;
        size++;

        // Heapify-Up (부모보다 크면 Swap)
        while (index > 0 && heap[index] > heap[(index - 1) / 2]) {
            int temp = heap[index];
            heap[index] = heap[(index - 1) / 2];
            heap[(index - 1) / 2] = temp;
            index = (index - 1) / 2;
        }
    }

    // 루트 요소 삭제 (Heapify-Down)
    public int remove() {
        if (size == 0) {
            throw new IllegalStateException("힙이 비어 있습니다!");
        }
        int root = heap[0];
        heap[0] = heap[size - 1]; // 마지막 노드를 루트로 이동
        size--;

        // Heapify-Down
        int index = 0;
        while (2 * index + 1 < size) {
            int leftChild = 2 * index + 1;
            int rightChild = 2 * index + 2;
            int largerChild = leftChild;

            if (rightChild < size && heap[rightChild] > heap[leftChild]) {
                largerChild = rightChild;
            }

            if (heap[index] > heap[largerChild]) {
                break;
            }

            // Swap
            int temp = heap[index];
            heap[index] = heap[largerChild];
            heap[largerChild] = temp;

            index = largerChild;
        }
        return root;
    }

    public void printHeap() {
        System.out.println(Arrays.toString(Arrays.copyOf(heap, size)));
    }

    public static void main(String[] args) {
        ArrayHeap maxHeap = new ArrayHeap(10);
        maxHeap.insert(10);
        maxHeap.insert(20);
        maxHeap.insert(15);
        maxHeap.insert(30);
        maxHeap.insert(40);

        maxHeap.printHeap(); // [40, 30, 15, 10, 20]
        System.out.println("삭제된 루트: " + maxHeap.remove()); // 40
        maxHeap.printHeap(); // [30, 20, 15, 10]
    }
}

```

- 출력 결과

```java
[40, 30, 15, 10, 20]
삭제된 루트: 40
[30, 20, 15, 10]
```

## 연결 리스트(Linked List) 기반 힙 구현

### 연결 리스트 기반 힙 구조

- 동적으로 크기를 조절할 수 있다.
- 부모-자식 간 이동이 느릴 수 있다.

### 연결 리스트 노드 정의

```java
class Node {
    int value;
    Node left, right, parent;

    public Node(int value) {
        this.value = value;
        this.left = this.right = this.parent = null;
    }
}
```

### 연결 리스트 기반 힙 구현(Java)

```java
class LinkedListHeap {
    private Node root;

    public void insert(int value) {
        Node newNode = new Node(value);
        if (root == null) {
            root = newNode;
            return;
        }

        Node node = findInsertPosition();
        if (node.left == null) {
            node.left = newNode;
        } else {
            node.right = newNode;
        }
        newNode.parent = node;

        heapifyUp(newNode);
    }

    private void heapifyUp(Node node) {
        while (node.parent != null && node.value > node.parent.value) {
            int temp = node.value;
            node.value = node.parent.value;
            node.parent.value = temp;
            node = node.parent;
        }
    }

    private Node findInsertPosition() {
        // BFS를 사용하여 빈 자리를 찾음
        Queue<Node> queue = new LinkedList<>();
        queue.add(root);
        while (!queue.isEmpty()) {
            Node node = queue.poll();
            if (node.left == null || node.right == null) {
                return node;
            }
            queue.add(node.left);
            queue.add(node.right);
        }
        return null;
    }

    public void printHeap(Node node) {
        if (node == null) return;
        System.out.print(node.value + " ");
        printHeap(node.left);
        printHeap(node.right);
    }

    public void print() {
        printHeap(root);
        System.out.println();
    }

    public static void main(String[] args) {
        LinkedListHeap maxHeap = new LinkedListHeap();
        maxHeap.insert(10);
        maxHeap.insert(20);
        maxHeap.insert(15);
        maxHeap.insert(30);
        maxHeap.insert(40);

        maxHeap.print(); // 40 30 15 10 20
    }
}

```

- 출력 결과

```java
40 30 15 10 20
```

## 자바에서 힙 구현하는 방법

```java
import java.util.PriorityQueue;
import java.util.Collections;

public class HeapExample {
    public static void main(String[] args) {
        PriorityQueue<Integer> minHeap = new PriorityQueue<>(); // 최소 힙
        PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder()); // 최대 힙

        minHeap.add(10);
        minHeap.add(5);
        minHeap.add(20);
        minHeap.add(1);

        maxHeap.add(10);
        maxHeap.add(5);
        maxHeap.add(20);
        maxHeap.add(1);

        System.out.println("최소 힙: " + minHeap.poll()); // 1
        System.out.println("최대 힙: " + maxHeap.poll()); // 20
    }
}

```

- PriorityQueue를 이용한 힙 구현
- Java의 PriorityQueue 클래스를 사용하면 힙을 쉽게 구현 가능
- 기본적으로 최소 힙(Min Heap)이 기본 설정
- Collections.reverseOrder()를 사용하면 최대 힙(Max Heap)으로 변환 가능
