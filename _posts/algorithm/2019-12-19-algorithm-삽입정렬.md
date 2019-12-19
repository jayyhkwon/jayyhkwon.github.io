---
layout: post
title:  "삽입정렬" 
category: Algorithm
tags: [Algorithm]
comments: true
---



## 삽입정렬



> 삽입정렬

- 기준이 되는 원소보다 앞에 존재하는 원소들과 비교하여 정렬하는 알고리즘
- 최선의 경우 시간복잡도는 O(n) : 이미 정렬되어 있는 경우
- 최악의 경우 시간복잡도는 O(n^2) : 반대로 정렬되어 있는 경우
- 추가 공간이 필요하지 않다



```java
//pseudocode
InsertionSort(A){
  for(i=2 to A.length){
    key = A[i];
    // A[i]를 정렬된 배열 A[1..j-1]에 삽입한다
    j=i-1;
    while(j>0 && A[j] > key){
      A[j+1]=A[j];
      j--;
    }
    A[j+1]=key;
  }
}
```



> 최악의 경우 시간복잡도가 O(n^2)인 이유는 while절 연산 횟수 때문이다.



<img src="/assets/post-img/algorithm/insertionSort_timeComplexity.png">





> **Java로 삽입정렬 구현**



- 테스트 코드

```java
import org.junit.jupiter.api.Test;
import java.util.Arrays;
import static org.junit.jupiter.api.Assertions.assertArrayEquals;

class InsertionSortTest {

    @Test
    public void testBestTimeComplexity(){

        int[] input = new int[]{1,2,3,4,5};
        int[] answer = Arrays.copyOf(input,input.length);
        Arrays.sort(answer);

        InsertionSort.insertionSort(input);
        assertArrayEquals(input,answer);
    }

    @Test
    public void testUnsortedArray(){

        int[] input = {64,34,25,12,22,11,90};
        int[] answer = Arrays.copyOf(input,input.length);
        Arrays.sort(answer);

        InsertionSort.insertionSort(input);
        assertArrayEquals(input,answer);
    }

    @Test
    public void testWorstTimeComplexity(){

        int[] input = {5,4,3,2,1};
        int[] answer = Arrays.copyOf(input,input.length);
        Arrays.sort(answer);

        InsertionSort.insertionSort(input);
        assertArrayEquals(input,answer);
    }
}
```



- 알고리즘

```java

public class InsertionSort {

    public static void insertionSort(int[] src) {
        for (int i = 1; i < src.length; i++) {
            int key = src[i];
            int j = i - 1;
            while (j >= 0 && src[j] > key) {
                src[j + 1] = src[j];
                j--;
            }
            src[j + 1] = key;
        }
    }
}


```

