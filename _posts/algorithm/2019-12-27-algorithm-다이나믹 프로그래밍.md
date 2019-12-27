---
layout: post
title:  "다이나믹 프로그래밍" 
category: Algorithm
tags: [Algorithm]
comments: true
---



## 다이나믹 프로그래밍

> **다이나믹 프로그래밍 정의**

- 동적 계획법(DP)라고도 한다

- 큰 문제를 작은 문제로 나눠서 푸는 알고리즘
  - DP
    - 작은 문제 중복o
  - D&C(분할정복)
    - 작은 문제 중복x



<br>

<br>

> **두 가지 속성을 만족해야 다이나믹 프로그래밍으로 문제를 풀 수 있다**

1. **Overlapping Subproblem (겹치는 작은 문제)**
   - 피보나치 수열
     - F(4) = F(3) + F(2), F(3) = F(2) + F(1)
     - F(3),F(2)가 중복된다
2. **Optimal Substructure (최적 부분구조)**
   - 부분 문제의 답으로 문제의 답을 구할 수 있다.
     - F(n) = F(n-1) + F(n-2) (n>=2)
     - F(n)의 답을 F(n-1)와 F(n-2)로 구할 수 있다.
   - Optimal Substructure를 만족한다면, 문제의 크기에 상관없이 어떤 한 문제의 정답은 일정하다.
     - F(4)는 F(6), F(5)을 구할 때마다 일정하다.

<br>

<br>

> **다이나믹 프로그래밍  풀이**

- 다이나믹 프로그래밍에서 각 문제는 한 번만 풀어야 한다
- Optimal Substructure를 만족하기 때문에, 같은 문제는 구할 때마다 정답이 같다
- 따라서 정답을 한 번 구했으면 어딘가에 메모해 놓는다.
- 이를 Memoization이라고 한다.

<br>

> 예제(피보나치 수열)

```java
//f(5)를 구하려면?
f(5) = f(4) + f(3);
f(4) = f(3) + f(2);
f(3) = f(2) + f(1);
f(2) = f(1) + f(0);
f(1) = 1;
f(0) = 0;

//f(3), f(2), f(1)이 중복된다
int memo[100];
int fibonacci(int n){
  if(n<=1)
    return n;
  else{
    if(memo[n] > 0)
      return memo[n];
    memo[n] = fibonacci(n-1) * fibonacci(n-2);
    return memo[n];
  }
}

// 시간복잡도 -> 모든 문제를 1번씩 푼다
// 문제의 갯수 (n) * 문제 1개를 푸는 시간 (1)
// -> O(n)
```



> **다이나믹 프로그래밍 구현방식**

1. Top-down (재귀)

2. Bottom-up (반복문)

   - 문제를 크기가 작은 문제부터 차례로 푼다

   - 문제의 크기를 조금씩 크게 만들면서 문제를 순차적으로 풀어나간다

   - 반복하다 보면 가장 큰 문제를 풀 수 있다

     ```java
     int f[100];
     int fibonacci(int n){
       f[0]=0;
       f[1]=0;
       for(int i=2; i<=n; i++){
         f[i] = f[i-1] + f[i-2];
       }
       return f[n];
     }
     ```

3. **Top-down vs Bottom-up 시간 차이**

   - 재귀보다 반복문이 빠르니 Bottom-up이 빠를것이다?

     - 알 수 없다!

   - 문제에 따라 따르다

     ```java
     f(0)=0;
     f(1)=0;
     f(2)=0;
     f(3)=0;
     ...
     f(9)=0;
     
     f(n) = f(n-5) + f(n-10) (n>=10)
     
     // f(10)을 구해라
     // 1. 재귀
     f(10) = f(5) + f(0); // 연산 1번
     // 2. 반복문
     f(10) = f(0)+f(1)+...f(10); // 연산 10번
     
     
     ```

     