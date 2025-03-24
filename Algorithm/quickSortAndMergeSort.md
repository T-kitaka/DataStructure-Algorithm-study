# 퀵 정렬과 병합 정렬
![image](https://github.com/user-attachments/assets/fd1ebf8c-86cd-4b7a-981b-2652006087a8)

## 1. 퀵 정렬
---
### 1.1. 퀵 정렬의 특징
평균적인 시간 복잡도가 O(n log n)인 정렬 알고리즘으로 병합 정렬과 함께 대표적인 분할 정복 알고리즘에 기반한 정렬 방법이다.
퀵 정렬은 배열에서 원소 하나를 pivot으로 두고 (오름차순인 경우) 피벗보다 작은 원소를 왼쪽으로, 큰 원소를 오른쪽으로 배치하며 이를 반복해나가 정렬을 하는 알고리즘이다.
![](https://velog.velcdn.com/images/hueyjeong/post/6bb63ded-d627-4a97-a558-6a8cf8957812/image.png)

### 1.2. 퀵 정렬의 구현
```java
quickSort(arr, 0, arr.length - 1);


// 퀵 정렬 메서드: 배열의 특정 구간을 정렬합니다.
public static void quickSort(int[] arr, int low, int high) {
    if (low < high) { // 종료 조건 - 배열의 원소가 1개 초과일 때
        // partition 메서드를 통해 피벗의 최종 위치를 구합니다.
        int pivotIndex = partition(arr, low, high);
        // 피벗 기준 왼쪽 부분 배열 정렬
        quickSort(arr, low, pivotIndex - 1);
        // 피벗 기준 오른쪽 부분 배열 정렬
        quickSort(arr, pivotIndex + 1, high);
    }
}

// partition 메서드: 배열의 마지막 요소를 피벗으로 하여
// 피벗보다 작은 값은 왼쪽, 큰 값은 오른쪽으로 재배치합니다.
public static int partition(int[] arr, int low, int high) {
    int pivot = arr[high];  // 피벗 설정
    int i = low - 1;        // 작은 값의 인덱스
    
    for (int j = low; j < high; j++) {
        if (arr[j] <= pivot) {
            i++;
            swap(arr, i, j);  // 작은 값끼리 위치 교환
        }
    }
    swap(arr, i + 1, high);   // 피벗을 올바른 위치로 이동
    return i + 1;             // 피벗의 인덱스 반환
}

// 배열 내 두 요소의 위치를 교환하는 메서드
public static void swap(int[] arr, int i, int j) {
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}
```
![](https://velog.velcdn.com/images/hueyjeong/post/7b07e601-5c9e-4ce2-a74c-9b430da9969a/image.png)

## 2. 병합 정렬
### 2.1. 병합 정렬의 특징
배열을 반씩 나누어 더 이상 나눌 수 없을 때까지 분할한 후 배열을 2개씩 합쳐 나가며 정렬된 상태로 병합한다. 이 과정을 모두 반복하여 다시 하나가 되면 정렬이 완료된다. O(n log n)인 알고리즘으로 안정적인 정렬이 가능하다.

### 2.2. 병합 정렬의 구현
```java
private static void sort(int[] arr) {
    if (arr.length == 1) {
        return;
    }
    int[] a = Arrays.copyOfRange(arr, 0, arr.length / 2);
    int[] b = Arrays.copyOfRange(arr, arr.length / 2, arr.length);
    sort(a);
    sort(b);
    int i = 0;
    int cursorA = 0, cursorB = 0;
    // arr[i]는 a, b 중에 작은 값(오름차순)
    while (cursorA < a.length && cursorB < b.length) {
        arr[i++] = (a[cursorA] < b[cursorB]) ? a[cursorA++] : b[cursorB++];
    }
    // 남은 게 없다면 둘 중 하나의 for문은 작동하지 않음
    // 남은 게 있는 쪽은 이미 정렬 되어 있으니 arr에 순서대로 추가
    for (int j = cursorA; j < a.length; j++) {
        arr[i++] = a[j];
    }
    for (int j = cursorB; j < b.length; j++) {
        arr[i++] = b[j];
    }
}
```
![](https://velog.velcdn.com/images/hueyjeong/post/f942ab35-8a87-4764-ab8f-9cace233d743/image.png)


## 자바에서의 퀵 정렬과 병합 정렬

**자바**에서는 원시 자료형의 정렬 알고리즘은 Arrays.sort의 기본 자료형의 경우 퀵 정렬 기반의 듀얼 피벗 퀵 정렬을 이용하고(2개가 아닌 3개로 나눔) 리스트나 객체의 정렬의 경우 삽입 정렬과 병합 정렬 기반의 팀 정렬이라는 알고리즘을 사용한다.
즉 완전한 형태의 퀵 정렬과 병합 정렬이 구현되어 있지는 않지만 이를 변형한 형태의 알고리즘들을 사용하고 있다.
