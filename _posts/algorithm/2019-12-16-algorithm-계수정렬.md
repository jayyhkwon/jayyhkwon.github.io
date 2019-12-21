---
layout: post
title:  "계수정렬" 
category: Algorithm
tags: [Algorithm]
comments: true
---



## 계수정렬



> 계수정렬

- 원소 간 비교하지 않고 원소의 빈도 수를 세어 정렬하는 방법이다
- 모든 원소는 양의 정수여야 한다.
- 시간복잡도는 O(n+k)로 보통 k=O(n)일 때 계수정렬을 사용하고 이 경우 시간복잡도는 O(n)이다.
- <a href="[https://ko.wikipedia.org/wiki/%EC%A0%95%EB%A0%AC_%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98#%EC%95%88%EC%A0%95%EC%84%B1](https://ko.wikipedia.org/wiki/정렬_알고리즘#안정성)">안정성</a>을 가지는 정렬이다
- 정렬을 위해 추가 공간이 필요하다



> CountingSort



```java
//pseudocode
CountingSort(A,B,k){
  //C[0..k]를 새로운 배열로 한다
  for(i=0 to k)
    C[i]=0;
  
  //C[i]는 이제 i와 같은 원소의 개수를 나타낸다. 
  for(j=1 to A.length)
    C[A[j]]=C[A[j]] + 1;
  
  //C[i]는 이제 값이 i보다 작거나 같은 원소의 갯수를 나타낸다.
  for(i=1 to k)
    C[i]=C[i]+C[i-1];
  
  for(j=A.length downto 1){
    B[C[A[j]]]=A[j];
    C[A[j]]=C[A[j]]-1;
  }
  
}
```





> Java로 계수정렬 구현



- 테스트 코드

  ```java
  
  import org.junit.jupiter.api.BeforeEach;
  import org.junit.jupiter.api.Test;
  
  import static org.junit.jupiter.api.Assertions.assertArrayEquals;
  
  class CountingSortTest {
  
      private Integer[] input;
      private Integer[] output;
  
      @BeforeEach
      public void setUp(){
          input = new Integer[]{2,5,3,0,2,3,0,3};
          output = new Integer[]{0,0,2,2,3,3,3,5};
      }
  
      @Test
      public void test(){
  
          Integer[] result = CountingSort.sort(input);
          assertArrayEquals(result,output);
      }
  
  }
  ```

  

- 알고리즘

```java
import java.util.Arrays;
import java.util.Collections;

public class CountingSort {

    public static Integer[] sort(Integer[] input) {

        int max = Collections.max(Arrays.asList(input));
        Integer[] result = new Integer[input.length];
        Integer[] countArray = new Integer[max+1];
        Arrays.fill(countArray,0);

        // countArray[i]는 i와 같은 원소의 개수를 나타낸다.
        for(int i=0; i<input.length; i++){
            countArray[input[i]] = countArray[input[i]] + 1;
        }

        //countArray[i]는 이제 i보다 작거나 같은 원소의 개수를 나타낸다.
        for(int i=1; i<=max; i++){
            countArray[i] = countArray[i] + countArray[i-1];
        }

        for(int i=input.length-1; i>=0; i--){
            result[countArray[input[i]]-1] = input[i];
            countArray[input[i]] = countArray[input[i]] - 1;
        }
        return result;
    }
}
```





> 계수정렬 vs 퀵정렬

- 퀵정렬의 경우 평균적으로 O(nlogn)의 시간복잡도를 가지나, 일반적인 정렬 상황에서 가장 선호되는 알고리즘이다.

- 입력이 int인 배열이라면 최악의 시간복잡도 O(n+k)인 계수정렬을 우선 고려해볼 수 있겠다는 생각이 들었다. 하지만 스택오버플로우에서 특정조건이 아닌 이상 퀵 정렬이 선호되는 이유에 대해 찾을 수 있었다.

- 1. 계수정렬은 countArray를 사용하므로 max값이 크다면 배열의 크기가 커져 배열 생성이  많은 비용이 발생한다.

  2. 만약 largest, smallest 원소 차이가 크다면 countArray에 의미없는 작업을 수행 할 수있다.

     ```java
     // smallest = 1, largest = 99999이면 2~99998은 의미없는 루프를 돌게된다.
     for(int i=1; i<=max; i++){
       countArray[i] = countArray[i] + countArray[i-1];
     }
     ```

  3. 계수정렬은 숫자가 아닌 경우 적용할 수 없다



ref. <a href="https://stackoverflow.com/questions/47736838/why-is-quick-sort-better-than-counting-sort">계수정렬 vs 퀵정렬</a>

