---
layout: post
title:  "기수정렬" 
category: Algorithm
tags: [Algorithm]
comments: true
---



## 기수정렬



> 기수정렬

- 가장 낮은 자리부터 가장 높은 자리까지 순차적으로 정렬하는 알고리즘
- 안정적인 정렬 알고리즘(stable sort)
- 다른 안정된 정렬을 사용하여 자리별로 정렬한다
- 정렬을 위해 추가 공간이 필요하다



```java
//pseudocode

RadixSort(A,d){
  for(i=1 to d)
    // 안정된 정렬을 사용해 배열 A를 i자리를 기준으로 정렬한다
}
```



> Java로 기수정렬 구현

- 테스트 코드

```java
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;

import static org.junit.jupiter.api.Assertions.assertArrayEquals;


class RadixSortTest {

    private int[] input;
    private int[] output;
    @BeforeEach
    public void setUp(){
        input = new int[]{329,457,657,839,436,720,355};
        output = new int[]{329,355,457,436,657,720,839};
    }

    @Test
    public void test(){
        int[] result = RadixSort.sort(input);
        assertArrayEquals(result,output);
    }

}

```

- 기수정렬 코드

```java

public class RadixSort {

    public static int[] sort(int[] src){
        int[] output = new int[src.length];
        int max = getMax(src);

        // 1의 자리, 10의 자리 ... 별로 계수정렬한다.
        for(int exp=1; max/exp>0; exp*=10){
            output = countSort(src, exp);
        }
        return output;
    }

    private static int getMax(int[] src) {
        int max = src[0];

        for(int i=0; i<src.length; i++){
            if(src[i] > max)
                max = src[i];
        }
        return max;
    }

    public static int[] countSort(int[] src, int exp){
        int[] output = new int[src.length];
        int[] count = new int[10]; // 0~9 count를 위한 배열

        for(int i=0; i<src.length; i++){
            count[(src[i]/exp)%10]++;
        }

        for(int i=1; i<10; i++) {
            count[i] += count[i-1];
        }

        for(int i=src.length-1; i>=0; i--){
            output[count[(src[i]/exp)%10]-1]=src[i];
            count[(src[i]/exp)%10]--;
        }
        return output;
    }
}

```

