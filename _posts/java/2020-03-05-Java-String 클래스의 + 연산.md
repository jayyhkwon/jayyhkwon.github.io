---
layout: post
title:  " String클래스의 + 연산 "
category: Java
tags: [Java]
comments: true
---





## String 클래스의 + 연산



백준 <a href="https://www.acmicpc.net/problem/15651">15651번</a> 문제를 풀다가 코드 한줄로 복잡도 차이가 크게 나서 (특히 공간복잡도) 찾아본 내용을 정리한다.

<br>

<img src="/assets/post-img/java/StringBuilder_Result.png"/>

 <br>

사진을 보면 거의 공간복잡도가 2배 가까이 차이가 나는 것을 볼 수 있다.<br>

그 이유를 아래 사진을 보며 알아보자.<br>

<br>

###사진1

<img src="/assets/post-img/java/StringBuilder(1).png"/>

<br>

###사진2

<img src="/assets/post-img/java/StringBuilder(2).png"/>

<br>

> **차이점**

- 위 사진을 보면 차이가 나는 것은 단 한 줄이다.

  ```java
  // arr[i]는 String 타입이다
  
  // 사진 1
  sb.append(arr[i] + " "); 
  // 사진 2
  sb.append(arr[i]);
  sb.append(" ");
  ```

- **String은 immutable한 객체이므로 + 연산을 할 경우** 컴파일러가 런타임에 StringBuilder 또는 StringBuffer로 append 한 후 새로운 String 객체를 반환한다. 이로 인해 + 연산을 할 때마다 메모리에 새로운 String 객체가 생성되어 더 많은 공간복잡도를 차지하게 되는 것이다. 

<br>

ref. <a href="https://docs.oracle.com/javase/6/docs/api/java/lang/String.html">doc</a>

