---
layout: post
title:  "Queue,Deque"
category: DataStructure
tags: [DataStructure]
comments: true
---







## Queue(큐)



> Queue

- 한 쪽 끝에서만 자료를 넣고 다른 한쪽 끝에서만 뺄 수 있는 자료구조
- 먼저 넣은 것이 가장 먼저 나오기 때문에 FIFO 라고도 한다
- **BFS에서 주로 사용한다**



> Queue 연산

- push
  - 큐에 자료를 넣는 연산
- pop
  - 큐에 자료를 빼는 연산
- front
  - 큐의 가장 앞에 있는 자료를 보는 연산
- back
  - 큐의 가장 뒤에 있는 자료를 보는 연산
- empty
  - 큐가 비어있는지 확인하는 연산
- size
  - 큐에 저장된 자료의 갯수를 알아보는 연산





## Deque(덱)



> Deque

- 양 끝에서 자료를 넣고 양 끝에서 뺄 수 있는 자료구조

- Double-ended queue의 약자이다

- Deque을 구현하면 Stack, Queue를 구현했다고 볼 수 있다.

  

>  Deque 연산

- push_front
  - 덱의 앞에 자료를 넣는 연산
- push_back
  - 덱의 뒤에 자료를 넣는 연산
- pop_front
  - 덱의 앞에서 자료를 빼는 연산
- pop_back
  - 덱의 뒤에서 자료를 빼는 연산
- front
  - 덱의 가장 앞에 있는 자료를 확인하는 연산
- back
  - 덱의 가장 뒤에 있는 자료를 확인하는 연산

