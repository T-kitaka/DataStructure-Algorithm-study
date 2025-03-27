# 동적 계획법(Dynamic programming)

## DP란?

큰 문제를 작은 문제로 나눠서 푸는 알고리즘 기법

- 주어진 문제를 풀기 위해서, 문제를 여러 개의 하위 문제(subproblem)로 나누어 푼 다음, 결과를 저장해 놓고 결합하여 최종적인 목적에 도달하는 것

## 재귀적 호출?

자신을 정의할 때 자기 자신을 재참조하는 방법

## 재귀 호출의 한계!

일반적인 재귀 호출 방식은 DP와 매우 유사

→ but, 재귀는 함수를 반복 호출해서 문제를 해결하지만, 같은 함수를 여러 번 중복 호출하게 되어 매우 비효율적

특히 피보나치의 경우 각 함수를 1번씩 호출하면 동일한 값을 2번씩 구하게 되고 입력이 커질 수록 호출되는 함수의 횟수는 기하급수적으로 증가

→ 컴퓨터 다운의 결과..

## DP의 사용 조건

- 중복 부분 문제 (Overlapping Subproblems)
- 최적 부분 구조 (Optimal Substructure)

### 중복 부분 문제 (Overlapping Subproblems)

동일한 작은 문제들이 여러 번 발생

- 이 문제들의 해결하기 위해서  결과를 저장해두고 재사용
    
    ![Image](https://github.com/user-attachments/assets/00dc5980-2104-4dbd-a830-48d80dab16f9)
    
- 피보나치의 입력값  n = 5
- f(3), f(2), f(1)과 같이 동일한 부분 문제가 중복
- 이 부분을 1회 계산했을 때 저장된 값을 재활용할 수 있게 된다!

### 최적 부분 구조 (Optimal Substructure)

부분 문제의 최적 결과 값을 사용해 전체 문제의 최적 결과를 낼 수 있는 경우

- 특정 문제의 정답은 문제의 크기에 상관없이 항상 동일!
    
    ![Image](https://github.com/user-attachments/assets/926bf340-0fb5-48f7-ba4d-fe03755f2dd7)
    
- A → B까지 최단 경로 찾기
- 중간에 X가 존재하면 A → X → B 가 많은 경로 중 가장 짧은 경로
- A - X 사이의 최단거리 : AX2 , X - B 사이의 최단거리 : BX2
- 만약 다른 경로를 택한다고 해서 전체 최단 경로가 변할 수 없다.
- 피보나치 수열도 동일하게 이전의 계산 값을 그대로 사용하여 전체 답을 구할 수 있어 최적 부분 구조를 갖고 있다( 작은 문제들의 정답으로 큰 문제들의 정답을 만든다.)

## DP 문제 해결 방식

- **Bottom-Up** (Tabulation 방식) - 반복문 사용
- **Top-Down** (Memoization 방식) - 재귀 사용

### **Bottom-Up** (Tabulation 방식)

아래부터 계산을 수행하고 누적시켜 전체 큰 문제를 해결하는 방식

- 아래부터 시작하여 반복문을 통해 점화식으로 결과를 내어 상단까지 그 값을 전이시켜 재활용하는 방식
- Tabulation : 도표, 도표 작성 → 문제들을 테이블로 시작화, 입력값을 토대로 테이블 크기를 지정

### **Top-Down** (Memoization 방식)

상단에서 부터 바로 호출을 시작하여 아래까지 내려간 다음 해당 결과 값을 재귀를 통해 전이시켜 재활용하는 방식

- 이미 이전에 계산을 완료한 경우 단순히 메모리에 저장되어 있던 내역을 꺼내서 활용
- Memoization : 결과값을 저장해 놓고 같은 입력 반복될 때 저장 값을 반환

## DP 문제 풀 때 3단계

- 문제에서 점화식이 떠오를 수 있는가? → DP로 풀 수 있는 문제인지 확인
- 배열(테이블)을 만들어서 작은 문제부터 채워나갈 수 있는가?
- 중복 계산을 줄이기 위해 저장할 공간을 설계했는가?

## 피보나치 수열

### 재귀

- return f(n) = f(n-1) + f(n-2)

### **Bottom-Up** (Tabulation 방식)

- 입력 값 n 만큼 배열 arr 생성, n = 6
    
    ![Image](https://github.com/user-attachments/assets/22c44b9e-172f-4cdf-96ba-e2a667584e33)
    
- 빈 arr에 초기값 0, 1 세팅
- 점화식 dp[i] = dp[i-1] + dp[i-2]을 통해 배열을 채워나간다.
    
    ![Image](https://github.com/user-attachments/assets/c6568a76-af90-418f-96d5-10ad8150ea98)
    
- 최종 배열
    
    ![Image](https://github.com/user-attachments/assets/3469f8a7-c661-41b9-963e-c3ea8588af5f)
    

```java
public class FibonacciBottomUp {

    public static void main(String[] args) {
        int n = 6;  // 원하는 피보나치 인덱스 (0부터 시작)
        int[] dp = new int[n + 1];  // dp 테이블 (index 0부터 n까지)

        // 1. 초기값 설정
        dp[0] = 0;
        if (n >= 1) dp[1] = 1;

        // 2. Bottom-Up 방식으로 테이블 채우기
        for (int i = 2; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }

        // 3. 결과 출력
        System.out.println("피보나치 수열 결과:");
        for (int i = 0; i <= n; i++) {
            System.out.print(dp[i] + " ");
        }
    }
}

```

### **Top-Down** (Memoization 방식)

![Image](https://github.com/user-attachments/assets/1cc2daec-035d-458d-9c08-41b22157e04c)

```java
public class FibonacciTopDown {
    public static void main(String[] args) {
        int n = 6;

        Map<Integer, Integer> memo = new HashMap<>();

        int result = topDown(n, memo);

        System.out.println("Fibonacci(" + n + ") = " + result);
        System.out.println("메모 상태: " + memo);
    }

    public static int topDown(int n, Map<Integer, Integer> memo) {
        if (n == 0) return 0;
        if (n == 1) return 1;

        //  null 체크
        Integer cached = memo.get(n);
        if (cached != null) return cached;

        int result = topDown(n - 1, memo) + topDown(n - 2, memo);
        memo.put(n, result);
        return result;
    }
}
```

![Image](https://github.com/user-attachments/assets/af079435-ec69-492d-ae72-b2ef6993133e)

## 대표  문제

피보나치, 계단 오르기, 연속합 등..
