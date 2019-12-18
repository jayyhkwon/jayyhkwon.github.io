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

  

- 계수정렬 코드

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



