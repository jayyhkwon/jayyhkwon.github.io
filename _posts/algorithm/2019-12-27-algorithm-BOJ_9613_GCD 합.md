---
layout: post
title:  "BOJ 9613번 GCD 합" 
category: Algorithm
tags: [Algorithm]
comments: true
---



```java
package BOJ;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;

/**
 * BOJ 9613
 * GCD 합
 * https://www.acmicpc.net/problem/9613
 */

public class GCDSum_9613 {

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());

        while(n-- > 0){
            int[] line = Arrays.asList(br.readLine().split("\\s")).stream().mapToInt(Integer::parseInt).toArray();
            long sum=0; // int는 작아서 long으로 변경
            for(int i=1; i<line.length; i++){
                for(int j=i+1; j<line.length; j++){
                    sum += gcd(line[i], line[j]);
                }
            }
            System.out.println(sum);
        }
    }

    private static int gcd(int a, int b){
        if(b == 0)
            return a;

        return gcd(b, a%b);
    }

    private static int gcd2(int a, int b){
        int gcd = 0;
        for(int i=2; i<=Math.min(a,b);i++){
            if(a%i == 0 && b%i == 0)
                gcd = i;
        }
        return gcd;
    }
}

```

