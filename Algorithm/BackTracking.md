# 1. 백트래킹(BackTracking)

>알고리즘 기법 중 하나로 재귀적으로 문제를 해결하되 현재 재귀를 통해 확인 중인 상태가 제한 조건에 위배가 되는지 판단하고, 해당 상태가 위배되는 경우 해당 상태를 제외하고 다음 단계로 넘어간다. <br>
간단하게 말하면 해를 찾는 도중 해가 절대 될 수 없다고 판단되면, 돌아가서 해를 찾는다고 생각하면 된다.

>백트래킹은 모든 경우의 수에서 조건을 만족하는 경우를 탐색하는 것이기 때문에 완전탐색기법인 DFS, BFS로 모두 구현이 가능하다. 백트래킹 특성상 조건에 부합하지 않으면 이전 수행으로 돌아가야 함으로 DFS가 구현하기 더 편해 DFS를 주로 사용한다.

EX) 만약 지갑을 놓고와서 집에 들러야 하는 상황이라고 가정했을 때

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fy07lF%2FbtsHXbkOuV7%2FSkVhvoW1aUatUAcKcxKNCK%2Fimg.png)

가능한 해가 아닌 경우를 배제함으로써 탐색 공간을 줄이고, 문제를 효율적으로 해결할 수 있도록 한다. 

## 2. 백트래킹 사용할 때
- 모든 조합/순열/부분집합을 탐색할 때
- 제약조건이 있는 문제에서, 조건을 만족하는 경우만 탐색할 때
-  경로 탐색(미로, 체스판등)
- 최적화 문제(가능한 해 중 조건에 맞는 최적해 찾기)

## 3. 백트래킹 알고리즘 절차
EX) [1,2,3,4] 중 2개를 뽑아서 합이 6을 초과하는 경우를 알아내는 과정을 백트래킹 과정으로 푼다고 해보자. <br>
   (뽑는 순서가 다르면 다른 경우의 수로 간주한다.)

   ### 이 경우처럼 N개의 숫자 중 M개 뽑는 순열은 시간복잡도가 O(N!)이지만, 가지치기로 줄일 수 있다. 

### 1. 유효한 해의 집합을 정의한다. <br>
[1, 2], [1, 3], [1, 4],  [2, 1], [2, 3], [2, 4] <br>
[3, 1], [3, 2], [3, 4],  [4, 1], [4, 2], [4, 3] <br>
정의한 집합을 그래프로 표현한다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FXGxES%2FbtsHXFr9B0b%2FmXJiKClKT0BDVIl7KtK2S1%2Fimg.png)

### 2.해당 해가 유망한지 아닌지를 판단할 수 있는 유망함수를 정의한다.
두 숫자 중 하나라도 3 미만이면 6을 초과할 수 없기 때문에 "첫번째 숫자가 3미만인 경우 백트래킹 한다"를 유망함수로 정의한다. (유망함수(Promising Function)는 백트래킹 알고리즘에서 중요한 역할을 합니다. 유망함수는 현재까지의 선택이 유망한 해로 이어질 가능성이 있는지를 판별하는 함수입니다)

### 3. 유망함수를 통해 해당 해가 유망한 해인지를 판단해 유망하다면 탐색하고, 유망하지 않다면 탐색하지 않는다.
##### 1과 2의 경우 3미만이므로 백트래킹한다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FTyIiU%2FbtsHVX19UXm%2FYtekU11Z2ih74JJz76qBpk%2Fimg.png)
##### 3과 4의 경우 유망하기 때문에 탐색한다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbwvU0n%2FbtsHW8BDzSz%2FNa8KNVJlGJOKLbhkjY7hTk%2Fimg.png)

```java
import java.util.Arrays;
public class TwoDigitPermutationWithSumGreaterThan6 {
    static int[] nums = {1, 2, 3, 4}; // 뽑을 숫자 목록
    static boolean[] visited = new boolean[4]; // 숫자를 썼는지 표시하기 위한 배열
    static int[] result = new int[2]; // 뽑힌 숫자를 저장할 배열

    public static void main(String[] args) {
        backtrack(0); //백트래킹 함수를 처음 호출할 때 depth=0부터 시작한다.
            // depth:백트래킹 함수가 현재 몇번째 숫자를 고르고 있는지 나타내는 깊이
    }

    static void backtrack(int depth) {
        if (depth == 2) { //숫자를 2개 다 고른 경우
            int sum = result[0] + result[1]; //합을 구함
            if (sum > 6) { //6초과 일 경우 출력한다.
                System.out.println(Arrays.toString(result));
            }
            return;
        }

        for (int i = 0; i < nums.length; i++) { //1,2,3,4를 순회하면서
            if (!visited[i]) { //이미 고른 숫자는 제외하고
                visited[i] = true; //현재 숫자 사용한걸 표시한다.
                result[depth] = nums[i]; //현재 숫자 자리에 저장
                backtrack(depth + 1); //다음 자릿수로 아동해서 다시 고르기
                visited[i] = false;  // 돌아와서 선택한 숫자 사용 해제
            }
        }
    }
}

```


## 4. 장점과 단점

- 장점 <br>
브루트포스처럼 모든 경우를 다 보지 않고, 가능성 없는 경로는 미리 자른다. <br>
복잡한 조합 문제, 퍼즐, 경로 탐색 등에 적합

-  단점 <br>
잘못 구현하면 시간 낭비 많음 <br>
가지치기 조건 (pruning logic) 없으면 성능 낮음 <br>
깊은 트리는 재귀 깊이 초과 위험

## 5. 백트래킹 vs 완전탐색

| 구분     | 완전탐색           | 백트래킹           |
|----------|--------------------|--------------------|
| 방식     | 모든 경우 다 탐색  | 유망하지 않으면 가지치기 |
| 효율     | 느릴 수 있음       | 상대적으로 빠름 (조건에 따라) |
| 조건     | 조건 없이 모든 경우 확인 | 제약 조건을 적극적으로 활용 |
| 구현     | DFS, BFS 등        | 주로 DFS 기반 재귀 |
