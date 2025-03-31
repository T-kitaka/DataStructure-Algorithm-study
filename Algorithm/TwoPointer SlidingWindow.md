# 투 포인터란?

- 투 포인터는 정렬된 배열이나 리스트에서 연속적인 구간에서 합이나 원소를 찾아내는데 유용한 알고리즘입니다.
- 특정한 두 원소의 합을 구한다고 가정하면 완전 탐색의 경우에는 O(n^2)의 시간 복잡도가 발생하지만 투 포인터로 이를 해결하면 **O(n)**의 시간 복잡도가 발생합니다.

## 기본 개념

- 투 포인터는 배열의 양 끝에 두개의 포인터를 이용하는 기법입니다.
- 좌우의 포인터는 양 끝에서 시작해서 특정 원소를 찾을때 까지 가운데로 이동하며 진행합니다.

# 예시

합이 M인 부분 연속 수열의 갯수를 구하시오

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FZ2hhL%2FbtrXIju0bb8%2FthAj9ig9KiESXvUnsho2jk%2Fimg.png)

### 해결하는 방법

1. 시작점, 끝점이 첫 번째 원소의 인덱스(0)을 가르킴
2. 현재 부분 합이 M과 같다면, 카운트 +1
3. 현재 부분 합이 M보다 작다면, end를 1증가시킨다.
4. 현재 부분 합이 M보다 크거나 같다면, start를 1 증가시킨다.
5. 모든 경우를 확인할 때 까지 2~4 과정을 반복

1. 시작점(start)과 끝점(end)이 첫 번째 원소의 인덱스(0)을 가리키도록 한다.
    - start, end의 부분합이 1이다.
    - 그러므로 카운트는 0이다.

   ![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb1AWlt%2FbtrXK69dzWp%2FZhFzcKkaQLkMB2zTVOxodk%2Fimg.png)

2. 이전 단계에서 부분합이 1이었기 떄문에 end를 1증가시킨다.
    - 이 부분도 3이기 때문에 카운트는 0이다.

   ![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F5rj2z%2FbtrXHTjfRm3%2FG2ZkZgGxL7gSOH9QzVtHb0%2Fimg.png)

3. 이전 단계에서의 부분합은 3이기 때문에 end를 1증가시킨다.
    - 현재의 부분합도 6이기 때문에 카운트는 0이다.

   ![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb5ZLcL%2FbtrXHAKZd6j%2Fgx6V8th3taUT9Mb6wURKiK%2Fimg.png)

4. 이전 단계에서의 부분합이 6이기 때문에 start를 1증가시킨다.
    - 현재의 부분합이 5이므로 카운트를 증가시킨다.
    - 현재 카운트: 1

   ![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FSoJlH%2FbtrXIx0OpeB%2Fq7o8gwI4iF17tv5aC9yDR0%2Fimg.png)

5. 이전 단계에서의 부분합이 5이었기 떄문에 start를 1증가 시킨다.
    - 현재의 부분합은 3이므로 무시한다.
    - 현재 카운트: 1

   ![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcaooQc%2FbtrXJ2srQLY%2F5IH9lxgaYHGn6LUBOHCFW1%2Fimg.png)


위 과정의 끝까지 반복하면 됩니다.

```java
public static void main(String[] args) {
	int n = 5; // 데이터의 개수
	int m = 5; // 찾고자 하는 부분합
	int[] arr = new int[]{1, 2, 3, 2, 5};
 
	int count = 0;
	int intervalSum = 0;
	int end = 0;
 
	// start를 차례대로 증가시키며 반복
	for (int start = 0; start < n; start++) {
  // end를 가능한 만큼 이동시키기
	  while (intervalSum < m && end < n) {
	    intervalSum += arr[end];
	    end += 1;
	  }
	  // 부분합이 m일 때 카운트 증가
	  if (intervalSum == m) {
	    count += 1;
	  }
	  
	  intervalSum -= arr[start];
		}
		
		System.out.println(count);
	}
	
}
```

---

# 슬라이딩 원도우란?

![](https://velog.velcdn.com/images/ninto_2/post/8e7c3787-d489-4433-b102-19b2e76bb71f/image.png)

![](https://blog.kakaocdn.net/dn/de2qeq/btsHk1K0YUb/tQboF6v5XzvNkFR81JkDe0/img.png)

슬라이딩 원도우는 투 포인터 알고리즘과 원리가 유사한 알고리즘입니다.

이 슬라이딩 원도우 알고리즘도 O(N^2)이상 걸릴 시간 복잡도도 부분 배열을 활용하여 O(N)으로 줄일 수 있다는 공통점이 있습니다.
투 포인터 알고리즘은 2개의 포인터를 활용하여 부분 배열의 길이를 유동적으로 활용하거나 2개의 특정 원소 값에 접근하지만 **슬라이딩 원도우**는 부분 배열의 길이가 고정적이라는 특징이 있습니다.

## 투포인터와 슬라이딩 원도우의 차이점

투포인터와 슬라이딩 함께 투 포인터는 자주 언급됩니다. 그러면 두개의 알고리즘은 차이점을 알아봅시다.

두 알고리즘의 차이점은 바로 부분 배열 길의 변화 여부이다.

투 포인터의 알고리즘은 부분 배열의 길이가 가변적이지만 슬라이딩 원도우 알고리즘은 부분 배열의 길이가 고정적이다.

## 예시

![](https://blog.kakaocdn.net/dn/Y1hRn/btrIdYGWFmy/It23g80iNdRjZqnbmTMLr0/img.png)

다음 과 같은 배열이 있습니다.

```java
[1, 3, 2, 6, -1, 4, 1, 8, 2]
```

연속적인 5개의 숫자중 합이 최대인 값을 구한다고 합시다.

그러면 다음과 같이 일일이 손으로 구하면 이런 값이 나옵니다.

```
[1,3,2,6,-1],4,1,8,2     합 :  11

1,[3,2,6,-1,4],1,8,2     합 :  14

1,3,[2,6,-1,4,1],8,2     합 :  12

1,3,2,[6,-1,4,1,8],2     합 :  18

1,3,2,6,[-1,4,1,8,2]     합 :  14
```

그러면 가장 큰 값은 18이 됩니다.

일단 간단히 생각하면 일일이 for문을 5번씩 돌면서 할 수 있습니다. 하지만 이런씩으로 하면 알고리즘이라고 할 수 없습니다.

### 푸는 방식

처음에 `1 + 3 + 2 + 6 + (-1)`을 한다고 해보십니다.
두번째는 `3 + 2 + 6 + (-1) + 4` 계산하면 됩니다. 그러면 `3 + 2 + 6 + (-1)` 이라는 중복적인 부분이 생깁니다.

그러면 중복적인 경우를 코드로 구현 후 처음 계산된 합에서 맨 앞 인덱스를 빼고, 마지막 인덱스를 더하면 됩니다.

```java
public class SlidingWindowMaxSum {
    public static void main(String[] args) {
        int[] numbers = {1, 3, 2, 6, -1, 4, 1, 8, 2};
        int n = numbers.length;
        int k = 5;

        int window = 0;
        for (int i = 0; i < k; i++) {
            window += numbers[i];
        }

        int answer = window;

        for (int i = k; i < n; i++) {
            window += numbers[i] - numbers[i - k];
            answer = Math.max(answer, window);
        }

        System.out.println(answer);
    }
}

```