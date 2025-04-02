# 그리디 알고리즘
![image](https://github.com/user-attachments/assets/804898c8-2d69-49fa-aade-e9fb297cea5b)

![image](https://github.com/user-attachments/assets/f9cede42-cb4e-49df-8183-5dffb1d2810f)

## 그리디 알고리즘이란?
그리디(탐욕적) 알고리즘은 문제 해결 과정에서 매 순간마다 **가장 좋은 선택**을 하는 전략을 말한다. 즉 현재 단계에서 가장 최적이라고 판단되는 해를 선택하고 그 선택이 전체 문제 해결에도 최적이라는 가정하에 최종해에 도달하고자 하는 알고리즘이다.
### 기본 개념
1. 현재 상황에 당장 최적으로 보이는 해를 선택한다.
2. 해당 선택에 따라 선택지를 줄여나가 계속 비슷한 방식으로 최적의 선택을 반복한다.
3. 전체 해를 구할 때까지 이런 선택을 반복한다.
### 예시
1. 거스름돈 문제
   * 가장 대표적인 예시로 거스름돈으로 줄 최소 동전 갯수를 구하는 문제
   * 500원, 100원, 50원, 10원 같은 단위의 동전이 있을 때 거스름돈 12340원의 최소 동전 갯수를 구한다면?
   * 가장 큰 단위(500원)부터 가장 작은 단위(10원)까지 최적의 선택을 반복한다.
   
```java
public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int remain = Integer.parseInt(br.readLine());

        // 각 순간마다 500, 100, 50, 10원 순서로 동전을 주는 것이 가장 최적의 선택
        int[] coins = new int[] { 500, 100, 50, 10 };

        int selectedCoin = 0;
        int coinCount = 0;
        while (remain > 0) { // 거스름돈의 잔액이 0원보다 많다면 반복
            if (selectedCoin >= coins.length) { // 10원으로 나누어떨어지지 않는다면 이 경우 문제를 해결할 수 없음
                System.out.println("구할 수 없는 단위의 금액입니다.");
                return;
            }
            coinCount += remain / coins[selectedCoin]; // {500}원부터 차례로 동전 갯수를 더해나감
            remain = remain % coins[selectedCoin]; // {500,100,50,10}원으로 거슬러줄 수 없는 나머지 금액을 구함
            selectedCoin++; // 다음 코인 선택
        }
        System.out.println(coinCount);
    }
}
```

2. [회의실 배정 (1931번)](https://www.acmicpc.net/problem/1931)
   * 여러 회의가 있고, 각 작업에 시작 시간과 종료 시간이 정해져 있을 때 겹치지 않으면서 배정할 수 있는 최대 갯수의 작업을 찾는다.
   * 접근 : 종료 시간이 가장 빠른 회의부터 차례대로 배정한다 -> 먼저 종료되는 회의을 우선 선택하고, 겹치지 않는 다음 작업중 종료 시간이 가장 빠른 회의를 선택한다.
   * 추가 조건 : 시작 시간과 종료 시간이 같은 경우 시작과 동시에 회의는 종료 되고 바로 다음 회의를 진행할 수 있다.
   * 수정 된 접근 : 종료 시간이 가장 빠른 회의를 선택하되 시작 시간이 가장 빠른 회의를 우선 선택하고 이 선택을 반복한다.
```java
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        long[][] arr = new long[n][2];
        for (int i = 0; i < n; i++) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            arr[i][0] = Long.parseLong(st.nextToken());
            arr[i][1] = Long.parseLong(st.nextToken());
        }
        // 가장 종료가 빠른 회의를 선택하되 시작 시간도 가장 빠른 회의를 선택한다. 이를 정렬로 구현
        Arrays.sort(arr, Comparator.comparingLong((long[] a)-> a[1]).thenComparingLong(a-> a[0]));
        long[] cur = arr[0];
        int cnt = 1;
        for (int i = 1; i < n; i++) {
            if (arr[i][0] < cur[1]) { // 현재 진행중인 회의보다 먼저 시작되는 회의는 선택될 수 없음
                continue;
            }
            cur = arr[i];
            cnt++;
        }
        System.out.println(cnt);
    }
```
이 외에도 최소 신장 트리를 찾는 알고리즘에서 프림 알고리즘, 크루스칼 알고리즘 등이 그리디한 방식으로 간선을 선택한다.
### 장점
* 구현이 간단하고 빠르다.
* 분할 정복, DP 등에 메모리를 적게 사용한다.
### 단점
* 항상 최적해를 보장하지는 못한다.
* 그리디 알고리즘으로 접근 시 부분 해는 최적이더라도 결국 전체 해에서 멀어질 수 있음
* 그리디 알고리즘으로 풀 수 있는 문제인지 확인 해야함

