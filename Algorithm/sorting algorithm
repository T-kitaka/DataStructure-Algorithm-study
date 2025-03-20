# 정렬 알고리즘(sorting algorithm)

## 정렬 알고리즘이란??

정렬은 임의의 순서대로 주어진 데이터를 특정한 순서(오름차순/내림차순)로 재배열하는 과정이다.

## 선택 정렬(Selection Sort)

- 정렬되지 않은 데이터들에 대해 가장 작은 데이터를 찾아 가장 앞의 데이터와 교환해 나가는 방식
- 전체 요소를 순차적으로 탐색
- 가장 직관적인 접근 방법으로, 정렬 알고리즘의 기초로 사용된다.
- 최선, 평균, 최악의 경우 비교연산이 많기 때문에 시간복잡도는 O(n²)

### 선택정렬의 정렬 과정

- 주어진 리스트 중에 최소값을 찾는다.
- 그 값을 맨 앞에 위치한 값과 교체한다.
- 맨 처음 위치를 뺀 나머지 리스트를 같은 방법으로 교체한다.
    
    ![Image](https://github.com/user-attachments/assets/46885ec8-f4b2-42eb-a9a7-320b1ff68737)
    
    ```java
    //SelectionSort 클래스 선언
    public class SelectionSort {
        // 선택 정렬 알고리즘을 수행하는 함수
        public static void selectionSort(int[] arr){
            int n = arr.length;
            // 바깥 루프: 배열의 각 원소에 대해 반복
            for(int i =0; i < n-1; i++){
                // 최소값의 인덱스를 저장하는 변수
                int minIndex = i;
                // 안쪽 루프 : 현재 인덱스보다 큰 원소들 중에서 최소값을 찾음
                for (int j = i+1; j<n; j++){
                    if (arr[j] < arr[minIndex]){
                        minIndex = j;
                    }
                }
                
                // 최소값을 찾은 후 현재 인덱스의 원소와 교환
                int temp = arr[minIndex];
                arr[minIndex] = arr[i];
                arr[i] = temp;
            }
        }
    }
    ```
    
    ```java
    // 메인 함수
    public static void main(String[] args) {
        // 정렬할 배열
        int[] arr = {7,3,2,8,9,4,6,1,5};
        // 정렬 전 배열 출력
        System.out.println("정렬 전 배열 출력 : ");
        for (int value : arr){
            System.out.println(value + " ");
        }
        
        // 선택 정렬 실행
        selectionSort(arr);
        
        // 정렬 후 배열 출력
        System.out.println("정렬 후 배열 출력 : ");
        for (int value : arr){
            System.out.println(value + " ");
        }
    }
    ```
    

## 삽입 정렬 (Insertion Sort)

- 모든 요소를 앞에서부터 차례대로 이미 정렬된 배열 부분과 비교하여, 자신의 위치를 찾아 삽입하는 정렬
- 즉, 현재 비교하고자 하는 타겟과 그 이전의 원소들과 비교하여 자리를 교환하는 정렬 방법
- 구현이 간단하지만 배열이 길어질수록 효율이 떨어진다.
- 정렬된 부분이 많을 수록 빠르다.
- 최선의 경우(이미 정렬된 경우) O(n), 최악의 경우(역순 정렬된 경우) O(n²)

### 삽입정렬의 정렬 과정

- 첫 번째 타겟은 두 번째 원소부터 시작한다.
- 타겟이 된 숫자가 이전 위치에 있던 원소보다 작다면 위치를 서로 교환한다.
- 그 다음 위치로 이동하여 이 과정을 반복한다.
    
    ![Image](https://github.com/user-attachments/assets/06965dce-0ba0-4e97-adc2-b42dfc8281d4)
    
    ![Image](https://github.com/user-attachments/assets/31cc2424-b587-4b38-823f-bf0058f338d6)
    
    ![Image](https://github.com/user-attachments/assets/0545e0f3-75c0-4701-9520-ca3e0b817381)
    
    ```java
    // InsertionSort 클래스 선언
    public class InsertionSort {
        // 삽입 정렬 알고리즘을 수행하는 함수
        public static void insertionSort(int[] arr){
            int n = arr.length;
            // 바깥 루프 : 배열의 두 번째 원소부터 마지막 원소까지 반복
            for (int i = 1; i<n; i++){
                // 현재 인덱스의 값을 key 변수에 저장
                int key = arr[i];
                int j = i-1;
                // 안쪽 루프 : key 값보다 큰 원소들을 오른쪽으로 이동
                while (j>=0 && arr[j] > key){
                    arr[j+1] = arr[j];
                    j--;
                }
                // key 값을 적절한 위치에 삽입
                arr[j+1] = key;
            }
        }
    }
    ```
    
    ```java
    // 메인 함수
    public static void main(String[] args) {
        // 정렬할 배열
        int[] arr = {7,3,2,8,9,4,6,1,5};
        // 정렬 전 배열 출력
        System.out.println("정렬 전 배열 출력 : ");
        for (int value : arr){
            System.out.println(value + " ");
        }
        
        // 삽입 정렬 실행
        insertionSort(arr);
        
        // 정렬 후 배열 출력
        System.out.println("정렬 후 배열 출력 : ");
        for (int value : arr){
            System.out.println(value + " ");
        }
    }
    ```
    

## 버블 정렬 (Bubble Sort)

- 서로 인접한 두 원소를 비교하여 정렬하는 방식
- 코드가 단순하여 구현하기 좋다.
- 큰 값은 점점 뒤로 이동하고 작은 값은 앞쪽으로 이동한다.
- 원소의 이동이 거품이 수면으로 올라오는 듯한 모습을 보이기 때문에 지어진 이름이다.
- 최선의 경우(이미 정렬된 경우) O(n), 최악의 경우 O(n²)

### 버블정렬의 정렬 과정

- 배열의 인접한 원소를 비교하여 큰 값을 뒤로 이동
- 배열 끝까지 비교 하면 가장 큰 원소가 배열의 끝으로 이동 된다.
- 다시 처음부터 과정을 반복한다.
    
    ![Image](https://github.com/user-attachments/assets/ef5ce5f0-a400-4225-bf1f-1495ae58406f)
    

```java
// BubbleSort 클래스 선언
public class BubbleSort {
    // 버블 정렬 알고리즘을 수행하는 함수
    public static void bubbleSort(int[] arr){
        int n = arr.length;
        // 바깥 루프 : 배열의 각 원소에 대해 반복
        for (int i = 0; i < n-1; i++){
            // 현재 원소가 다음 원소보다 크면 교환
            if (int j = 0; n < n-1-i; j++){
                // 현재 원소가 다음 원소보다 크면 교환
                if (arr[j] > arr[j+1]){
                    int temp = arr[j];
                    arr[j] = arr[j+1];
                    arr[j+1] = temp;
                }
            }
        }
    }
}
```

```java
// 메인 함수
public static void main(String[] args) {
    // 정렬할 배열
    int[] arr = {8,3,7,5,4,2};
    // 정렬 전 배열 출력
    System.out.println("정렬 전 배열 출력 : ");
    for (int value : arr){
        System.out.println(value + " ");
    }
    
    // 버블 정렬 실행
    bubbleSort(arr);
    
    // 정렬 후 배열 출력
    System.out.println("정렬 후 배열 출력 : ");
    for (int value : arr){
        System.out.println(value + " ");
    }
}
```
