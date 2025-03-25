<aside>
🔎 &nbsp; 목차

    1. 그래프 탐색이란?
    2. DFS
    3. BFS
    4. DFS와 BFS의 사용
</aside>

# 1.  그래프 탐색이란?

그래프 탐색은 그래프 구조에서 정점(Vertex)과 간선(Edge)을 따라 이동하는 과정이다.

그래프 탐색은 주로 시작 정점에서 출발하여 인접한 정점을 탐색하는 방법을 사용하며,

탐색의 대표적 종류로는 깊이 우선 탐색(DFS)과 너비 우선 탐색(BFS)이 있다.

이러한 그래프 탐색은 문제 해결, 경로 찾기, 연결 요소 찾기 등 다양한 부분에서 활용된다.

<br>
<br>
<br>

# 2. 깊이 우선 탐색 (DFS: Depth First Search)

**DFS**는 Depth First Search의 약자로, 깊이 우선 탐색이라고도 부른다.

DFS는 그래프 탐색 시 먼저 깊게 탐색을 하고 나서 이전으로 돌아가는 과정을 거친다.

탐색 시 중요한 점은 이미 방문했던 지점을 또 방문하게 되면 탐색 효율이 떨어지므로 다시 방문하지 않아야 한다는 점이다.

DFS는 **재귀를 활용**해 구현하게 되는데, 방문할 수 있는 지점이 있다면 그 지점을 방문하는 함수를 재귀적으로 호출하고, 더 이상 방문할 곳이 없다면 함수를 종료하게 된다.

- 동작 원리: 스택
- 구현 방법: 재귀 함수 사용

<br>
<br>

## 2-1.  DFS 탐색 예시

![Image](https://github.com/user-attachments/assets/2433941e-5c39-427b-bb70-ff422a67954b)


위 그래프를 DFS로 탐색해보겠다.

1번에서 출발하고, 노드의 번호가 작은 것부터 탐색한다고 가정한다.

방문 순서는 **1 → 3 → 2 → 6 → 5 → 4** 가 된다.

<br>

**설명**

- 1에 연결된 노드 중 가장 작은 수를 가진 노드로 이동 : 1 → 3


- 3에 연결된 노드 중 가장 작은 수를 가진 노드로 이동 : 1 → 3 → 2


- 2에 연결된 노드 중 가장 작은 수를 가진 노드로 이동. 이때 3은 이미 방문 했으므로 방문하지 않음 : 1 → 3 → 2 → 6


- 6에 연결된 노드 중 가장 작은 수를 가진 노드로 이동. 2는 이미 방문 했으므로 방문하지 않음 : 1 → 3 → 2 → 6 → 5


- 5에 연결된 노드 중 방문할 수 있는 노드가 없기 때문에 다시 이전 호출로 돌아간다.


- 다시 3에 연결된 노드 중 아직 방문하지 않은 노드로 이동 : 1 → 3 → 2 → 6 → 5 → 4


- 모두 다 방문 했으므로 탐색 종료

<br>
<br>

![Image](https://github.com/user-attachments/assets/d6c51e5a-f708-480d-a861-e23efc899613)

만약 위 그래프와 같이 연결 요소가 여러 개 있는 경우, DFS를 진행하다가 그 이후에 아직 방문하지 않은 정점 중 번호가 가장 낮은 지점을 시작으로 다시 탐색을 이어가면 된다.

방문 순서는 **1 → 2 → 5 → 3 → 6 → 7 → 4 → 8 → 9** 가 된다.

<br>
<br>

## 2-2. DFS 코드

앞서 말했듯이 DFS로 그래프를 탐색할 때는 재귀 호출로 탐색한다고 하였다.

![Image](https://github.com/user-attachments/assets/22a918e9-0199-49bd-b0db-85773292e221)

위 그래프를 DFS로 탐색하는 코드를 구현한 것은 다음과 같다.

```java
public class Main {

    //방문처리에 사용할 배열
    static boolean[] visited = new boolean[9];

    //그림에 있는 그래프를 2차원 배열로 표현
    //인덱스 번호가 각각의 노드 번호가 될 수 있게 0번 인덱스는 빈 상태로 구현
    //표현 방법: 1번 노드에 연결된 노드들은 2,3,8이므로, 1번 인덱스 배열에 2,3,8을 넣어준다.
    static int[][] graph = {{},{2,3,8},{1,6},{1,5}
                            ,{5},{3,4,7},{2,8},{5},{1,6}};

    public static void main(String[] args) {
        dfs(1); //1번 노드부터 수행
    }

    public static void dfs(int nodeIndex){
        //방문 처리
        visited[nodeIndex] = true;

        //방문 노드 출력
        System.out.print(nodeIndex + " -> ");

        //방문한 노드에 인접한 노드 찾기
        for (int node : graph[nodeIndex]) {
            //인접한 노드가 방문한 적이 없으면 dfs 수행
            //방문한적 없는 노드일 경우 수행
            if (!visited[node]) {
                dfs(node); //재귀 호출
            }
        }
    }
}
```
<br>

실행 결과:

![Image](https://github.com/user-attachments/assets/a7d2eba9-5d5d-4211-854c-d9d22c6efe3e)

<br>
<br>

## 2-3. DFS의 장단점

- 장점
    - 최선의 경우에는 빠르게 해를 찾을 수 있다.
    - 재귀를 이용해 쉽게 구현할 수 있기 때문에 코드가 간결 해진다.



- 단점
    - 찾은 해가 최적 해가 아닐 가능성이 있다.
    - 최악의 경우 해를 찾는데 가장 오랜 시간이 걸릴 수 있다,
    - 재귀 호출을 이용하기 때문에 깊이가 매우 깊은 그래프일 경우 스택 오버플로우가 발생할 수 있다.

<br>
<br>
<br>

# 3. 너비 우선 탐색 (BFS: Breadth First Search)

**BFS**는 Breadth First Search의 약자로, 너비 우선 탐색이라고도 부른다.

BFS는 재귀(스택)을 활용했던 DFS와 달리 **큐를 사용**한다.

하나의 노드에 방문하게 되면, 그 노드와 인접한 노드 중 방문한적이 없는 다른 노드를 모두 큐에 넣는다.

큐는 FIFO(First In First Out)를 따르는 구조이므로, 처음 넣었던 노드의 이웃 노드를 순차적으로 방문하게 된다.

- 동작 원리: 큐
- 구현 방법: 큐 자료 구조 사용

<br>
<br>

## 3-1. BFS 탐색 예시

![Image](https://github.com/user-attachments/assets/a8888c24-68f2-48e8-86d4-0fe6c64483ea)

예를 들어 위와 같은 그래프를 BFS 방식으로 탐색해 보겠다.

DFS와 마찬가지로 1번 노드에서 부터 출발하여 가장 작은 수를 먼저 탐색한다고 가정한다.

방문 순서는 **1 → 2 → 3 → 4 → 5 → 6 → 7** 이 된다.

<br>

**설명**

(큐: 뒤 | 앞)

- 큐에 1이 들어간다.

  Queue : 1

  방문 상태 :


- 큐에서 1이 나오며 (방문) 인접 노드인 2, 3, 4가 순차적으로 큐에 들어간다.

  Queue : 4,3,2

  방문 상태 : 1


- 큐에서 2가 나오며 인접 노드인 5가 큐에 들어간다. (큐: 5,4,3)

  Queue : 5,4,3

  방문 상태 : 1 → 2


- 큐에서 3이 나오며 인접 노드인 6이 큐에 들어간다. (큐: 6,5,4)

  Queue : 6,5,4

  방문 상태 : 1 → 2 → 3


- 큐에서 4가 나온다. (큐: 6,5)

  Queue : 6,5

  방문 상태 : 1 → 2 → 3 → 4


- 큐에서 5가 나온다. (큐: 6)

  Queue : 6

  방문 상태 : 1 → 2 → 3 → 4 → 5


- 큐에서 6이 나오며 인접 노드인 7이 큐에 들어간다. (큐: 7)

  Queue : 7

  방문 상태 : 1 → 2 → 3 → 4 → 5 → 6


- 큐에서 7이 나온다.

  Queue : 7

  방문 상태 : 1 → 2 → 3 → 4 → 5 → 6 → 7


<br>
<br>

## 3-2. BFS 코드

DFS로 탐색해 보았던 그래프를 똑같이 BFS의 방법으로 탐색해 보겠다.

![Image](https://github.com/user-attachments/assets/dd66ebcb-0633-4778-94a5-4e1566ac3cc3)

위 그래프를 BFS로 탐색하는 코드를 구현한 것은 다음과 같다.

```java
import java.util.LinkedList;
import java.util.Queue;

public class Main {
    public static void main(String[] args) {
        //그림에 있는 그래프를 2차원 배열로 표현
        //인덱스 번호가 각각의 노드 번호가 될 수 있게 0번 인덱스는 빈 상태로 구현
        int[][] graph = {{},{2,3,8},{1,6},{1,5}
                            ,{5},{3,4,7},{2,8},{5},{1,6}};

        boolean[] visited = new boolean[9]; //방문처리 배열

        System.out.println(bfs(1, graph, visited));
    }

    static String bfs(int start, int[][] graph, boolean[] visited) {
        //탐색 순서를 출력하기 위해 StringBuilder 선언
        StringBuilder sb = new StringBuilder();
        //BFS에서 사용할 큐 생성
        Queue<Integer> q = new LinkedList<Integer>();

        //큐에 BFS를 시작할 노드 번호를 넣어준다.
        q.offer(start); 
        //시작 노드 방문 처리
        visited[start] = true;

        //큐가 빌 때까지 반복
        while (!q.isEmpty()) {
            int nodeIndex = q.poll(); 
            sb.append(nodeIndex + " -> ");

            //큐에서 꺼낸 노드와 연결된 노드들을 체크
            for (int i = 0; i < graph[nodeIndex].length; i++) {
                int temp = graph[nodeIndex][i];

                //방문하지 않았으면 방문처리 후 큐에 넣기
                if (!visited[temp]) {
                    visited[temp] = true;
                    q.offer(temp);
                }
            }
        }

        //탐색 순서 리턴
        return sb.toString();
    }

}
```
<br>

실행 결과:

![Image](https://github.com/user-attachments/assets/561130ef-2f11-4e8d-be43-cbb522ff88b9)

<br>
<br>

## 3-3. BFS의 장단점

- 장점
    - 최적해를 찾는 것을 보장한다.
    - 최단 경로가 존재한다면, 어느 한 경로가 무한히 깊어진다고 해도 최단 경로를 반드시 찾을 수 있다.


- 단점
    - 모든 노드를 큐에 저장하기 때문에 메모리 사용량이 많아질 수 있다.
    - 최소 실행시간보다는 오래 걸리는 것이 거의 확실하다.
    - 명시적인 큐 자료구조를 사용하기 때문에 DFS에 비해 코드 구현이 복잡하다.

<br>
<br>
<br>

# 4. DFS 와 BFS의 사용

- DFS
    - **경로 찾기**: 경로의 존재 여부를 판단할 때 사용된다.
    - **미로 탐색**: 미로의 출구를 찾거나 모든 가능한 경로를 탐색하는데 활용한다.
    - **사이클 탐지**: 그래프 내에 사이클을 탐지할 때 사용된다.
    - 찾아야하는 노드가 깊은 단계에 있을 때
      

- BFS
    - **최단 경로 찾기**: 가중치가 없는 그래프의 **최단 경로를 탐색**할 때 사용된다.
    - 노드 수가 적고 깊이가 얕은 해가 존재할 때
