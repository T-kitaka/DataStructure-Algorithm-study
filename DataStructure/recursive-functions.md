# 재귀란?

![](https://velog.velcdn.com/images%2Fgeesuee%2Fpost%2Fa7324cc7-7101-4466-88d4-018663f46aba%2Fimage.png)

- 함수의 실행 과정에서 자기 자신을 호출하는 함수를 의미합니다.

## 특징

재귀함수에는 Head Recursion(머리재귀)과 Tail Recursion(꼬리재귀)가 존재합니다.

- Head Recursion은 재귀 함수가 맨 앞에 존재합니다.
- Tail Recursion은 재귀함수가 맨 마지막에 존재합니다.
- 스택과 비슷한 구조를 가졌습니다.
- 다양한 알고리즘에 사용합니다. 동적프로그램이나 병합정렬, 그래프탐색 알고리즘 부분에서 사용됩니다.

# 장점과 단점

### 장점

- 코드의 간결함, 가독성 증가, 변수의 사용을 줄여준다.
- 문제 해결의 직관성: 복잡한 문제를 간단한 하위 문제를 나누는 방식이기 때문에, 수학적 정의가 명확한 문제를 해결할 때 더 직관적입니다.

### 단점

- 성능 문제: 재귀는 함수 호출마다 스택 프레임을 생성합니다. 과도한 재귀 호출은 메모리 오버헤드를 유발할 수 있습니다.
- 디버깅: 재귀를 쓰고 버그나면 디버깅을 하는 과정도 매우 복잡합니다.
- 메모제이션 기법: 재귀를 너무 많이 반복해서 일어나는 문제를 해결하는 방법입니다. 이 기법은 DP 알고리즘에서 나오는 개념입니다. 예를 들어 피보나치 수열에서 너무 많은 중복계산이 발생이 되어 메모제이션을 적용하면 이를 피할 수 있습니다.

```java
public static int fibonacci(int n, int[] memo) {
    if (n <= 1) {
        return n;
    }
    if (memo[n] != -1) {
        return memo[n];
    }
    memo[n] = fibonacci(n-1, memo) + fibonacci(n-2, memo);
    return memo[n];
}

public static void main(String[] args) {
    int n = 10;
    int[] memo = new int[n + 1];
    Arrays.fill(memo, -1);
    System.out.println(fibonacci(n, memo));
}
```

---

# 구조

재귀는 자기자신을 호출하는 구조를 가졌습니다. 그러기에 무한 루프에 빠질 위험이 있어 재귀 종료 조건을 잘 걸어줘야 합니다.

그러므로 재귀를 쓸때는 상단에 종료 조건을 필수적으로 명시를 해줘서  무한 루프에 빠지지 않도록 해줘야 합니다.

그리고 재귀 함수는 해당 함수가 호출된 이후의 명령문이 수행되지 않습니다.

![](https://velog.velcdn.com/images%2Fgeesuee%2Fpost%2F1488d7ac-27bf-4c25-a3fb-1efaafafcb55%2Fimage.png)

---

# 재귀 함수 사용 대표 예시

## 1. 팩토리얼

```java
public static int factorial(int n) {
    if (n <= 1) {
   	   return 1;
    }
    else {
       return n * factorial(n-1);
    }
}
```

![](https://gptjs409.github.io/img/2019-08-01/Recursive-001-flow1.png)

## 2. 피보나치 수열

```java
public static int fibonacci(int n) {
	  if (n <= 1) {
	     return n;
	  }
	  else {
	     return fibonacci(n-1) + fibonacci(n-2);
	  }
}
```

![](https://blog.kakaocdn.net/dn/cyLVFa/btqZP2SsdBy/QgvICwpXtOcQAHDmRsmdMK/img.gif)

## 3. DFS

```java
import java.util.*;

class DFS {
    static ArrayList<Integer>[] adj; // adjacency list representation of the graph
    static boolean[] visited; // array to keep track of visited vertices

    public static void dfs(int v) {
        visited[v] = true;
        System.out.print(v + " ");

        for (int neighbor : adj[v]) {
            if (!visited[neighbor]) {
                dfs(neighbor);
            }
        }
    }

    public static void main(String[] args) {
        int n = 5; // number of vertices
        adj = new ArrayList[n];
        visited = new boolean[n];

        // initialize adjacency list and visited array
        for (int i = 0; i < n; i++) {
            adj[i] = new ArrayList<>();
            visited[i] = false;
        }

        // add edges to the graph
        adj[0].add(1);
        adj[0].add(2);
        adj[1].add(2);
        adj[2].add(0);
        adj[2].add(3);
        adj[3].add(3);

        for (int i = 0; i < n; i++) {
            if (!visited[i]) {
                dfs(i);
            }
        }
    }
}
```