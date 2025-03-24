# 트리란?
![자료구조](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhuFd33PgGqicD1rDojbZLrU2Xx7nv6739KxDbvcTxiWjnWVybQlx_CMD0hnuAOy7Qb-VL2ZMoo7sk58ZzUCBYE9P5i11TSo6giWOeNU6msVT004FvrQFXEi1tBZy78tzSbu_LsO4CLTszO/s1600/1111.PNG)

자료구조에는 크게 `선형`, `비선형` 으로 나눠집니다. <br/>
그중 `Tree`는 `비선형` 자료구조 중 하나입니다.

## 선형구조
자료간의 앞,뒤 관계가 1:1이 되면 `선형`구조입니다.
저희가 배운 `Stack`, `Queue`가 `선형` 자료구조에 속합니다.

![선형구조](https://velog.velcdn.com/images%2Fragnarok_code%2Fpost%2F059eda2b-aa18-465a-bf9d-a398c9850a91%2F%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202021-11-23%20%EC%98%A4%ED%9B%84%2012.11.50.png)

## 비선형 구조
비선형 구조는 아래와 같은 그림처럼 하나의 자료에 여러개의 자료가 존재 할 수 있는 느낌입니다.

![비선형 구조](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTNGGlWGRsPNtcIs2c0U0-gWgfoFZwNF36ifckD96hSs2YulfamOpx2NxiAZgBgM6VjVk8&usqp=CAU)

이런씩으로 트리는 하나의 공간(노드)에 원쪽 또는 오른쪽으로 퍼질 수 있습니다.



# 용어

---

> **루트(Root)**
> 
> 트리 구조 중 최상위에 존재하는 노드
---
> **노드(Node)**
> 
>각 노드는 데이터를 저장할 수 있으며, 연결된 선으로 다른 노드와의 관계를 가진다.


```java
class Node<T> {
    T data;
    Node<T> left; // 자기 자신을 참고
    Node<T> right;
}
```
---
> **레벨(Level)**
> 
> 트리에서 각각의 층을 나타내는 냄

![트리_레벨](https://farm5.staticflickr.com/4482/36997131684_89ddd642cf_o.png)

---
> **간선(Edge)**
> 
> 노드와 노드를 연결하는 선
---
> **부모 노드(parent node)**
> 
> 한 노드를 기준으로 바로 상위에 존재하는 노드
---
> **자식 노드(child node)**
> 
> 한 노드를 기준으로 바로 하위에 존재하는 노드
---
> **높이(heigh)**
> 
> 트리 중 최고 레벨
---



## 특징

- 루트 노드는 한개입니다.
  - 0개 이상의 하위 트리로 구성되어 있습니다.
- 노드 간에 부모 자식 관계를 갖고 있는 게층형 자료구조이며 모든 자식 노드는 하나의 부모 노드만 갖습니다.
- 노드가 n개인 트리는 항상 `n - 1`개의 간선을 가집니다.
  - 위에 예제 그림의 노드는 6개 입니다. 그러면 간선은 5개 입니다.
- 트리내에 또 다른 트리가 있는 재귀적 자료구조입니다.

예시) 트리가 아닌 경우

![트리가 아닌 경우](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F4pwtu%2Fbtq1By9I93O%2Fzz7ZRsYNpUbKfCwCf0Jno0%2Fimg.png)

위에 그림은 트리가 아닙니다. <br/>
6의 값을 가진 노드를 보면 6은 두개의 부모를 가지고 있습니다.<br/>
굳이 따지면 추후에 나오는 그래프 자료구조 입니다.

# 이진트리(Binary Tree)
트리의 개념에서 나온 `이진 트리`에 대해서 알아봅시다. <br/>
아래는 이진트리에서 파생된 자료구조, 알고리즘입니다.

- 이진트리
  - AVL-tree
  - 레드-블랙 트리
  - 스레드 이진 트리
  - 힙
  - B-tree
    - 2-3-4 tree
    - B+ tree
  - 포레스트
  - 트라이



## 이진트리란?
이진트리는 트리 중에서 최대 2개의 자식노드를 가질 때 이진트리(Binary Tree)라고 합니다.<br/>
자식이 있을 수도 있고 없을 수도 있고, 한개만 있을 수도 있습니다.<br/>
참고로 값이 같아도 다른 위치에 있으면 다른 트리로 칩니다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FPEvrB%2FbtrR1gqqTZR%2F7w5nQZ54VJD4V2hYvkKrl1%2Fimg.png)


### 이진트리의 종류

이진 트리에서도 3개의 종류가 있습니다. 

1. 정 이진트리(Full Binary Tree) or 엄격한 이진트리(Strcit Binary Tree)
   2. 영어 뜻을  `Full`말이 있습니다. 이 뜻대로 <u> 모든 노드가 2개의 자식을 가지고 있거나 없는 경우를 뜻합니다. </u>
2. 포화 이진트리(Perfect Binary Tree)
   3. 영어 뜻을 보면 `Perfect`라는 말이 있습니다. 이 뜻대로 모든 노드가 2개의 가지고 있어야 되고 자식노드들이 모두 같은 레벨이어야 됩니다. 
3. 완전 이진트리(Complete Binary Tree)
   4. 마지막 레벨을 제외하고 모든 노드가 채워져 있어야 합니다. 마지막 레벨의 노드는 다 채워져 있을 수도 있고 아닐 수도 있습니다.
   5. 노드는 왼쪽에서 오른쪽 방향으로 채워져야 합니다.
   6. 포화이진트리도 완전 이진트리입니다.


1. 정 이진트리<br/>
    ![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbJnMpB%2FbtrRYxmdrSi%2F0g52O6c06nDQhe0Nn3Hti0%2Fimg.png)
2. 포화 이진트리 <br/>
    ![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FSxnzv%2FbtrR3d7hmYL%2FSdkGvG5J1de9D3ypB2IYd1%2Fimg.png)
   포화이진트리에서는 모든 레벨(level)의 노드가 꽉차있기 때문에 노드 갯수는 2의 k+1 제곱 -1의 특징을 갖습니다.
3. 완전이진트리 <br/>
   ![완전이진트리](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbOEc8T%2FbtrR2w7Bx03%2FN4LkDJXvsS2RZsfAK4VOw0%2Fimg.png)
   ![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FOqfFu%2FbtrR2SoQSw7%2F627xyyi27Jj7NbOAs07mZk%2Fimg.png)


### 이진트리 순회 방식

- 전위 순회: 루트 노트를 항상 먼저 순회를 하며 왼쪽 -> 오른쪽으로 순회하는 방식
- 중위 순회: 왼쪽 가장 하위 노드를 먼저 순회한 이후 -> 바로 상위 노드 -> 오른쪽 노드 
- 후위 순회: 왼쪽 가장 하위 노드를 먼저 순회한 이후 -> 오른쪽 하위 노드 -> 바로 상위 노드

![](https://blog.kakaocdn.net/dn/SA71w/btrTHO7twEq/gZ9mV2pYlvHNW0odpOGjM1/img.png)


## 1차원 배열로 트리구조 나타내기

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FqX1r8%2FbtqMARP7ACw%2FVHcTg5NA690ZemH9J55fP0%2Fimg.png)
```java
import java.util.Arrays;
import java.util.Scanner;

public class Tree1Matrix {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		int n = sc.nextInt();
		int[] parent = new int[n+1]; //tree 저장을 위한 1차원 배열, 루트는 1부터 시작하기 때문에 n+1
		
		for(int i = 2; i <= n; i++) { //1은 루트이기 때문에 2부터 시작 (tree[1] = 0)
			parent[i] = i/2; //노드i의 부모 노드 인덱스 = i/2
		}
		
		System.out.println(Arrays.toString(parent));
	}
}

```