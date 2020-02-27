---
layout: post
title: "Race Condition"
category: OS
tags: [OS]
comments: true
---



> **Race Condition**

- 하나의 공유 데이터에 2개 이상의 연산이 발생하여 결과에 영향을 줄 수 있는 상태를 말한다
  - count라는 변수에 2개의 스레드가 접근하여 1을 증가시키는 연산을 하는 경우

<br>

> **Race Condition in Kernel**

- P(a)가 시스템콜을 호출하여 커널의 count 변수를 증가시키는 연산을 한다고 가정하자
- P(a)의 시스템콜 (user -> kernel 모드로 전환하고 count 변수의 값을 레지스터로 읽어들인다)
- 컨텍스트 스위칭( P(a) - > P(b) )
- P(b)의 시스템콜하여 count++ 연산 수행하고 저장
- 컨텍스트 스위칭 ( P(b) - > P(a) )
- P(a) count++ 연산 수행하고 저장
- **count는 최종적으로 1만 증가함 -> load,write,save 연산이 atomic하지 않으므로**
- 해결책
  - 커널 모드에서 수행 중일 때는 CPU를 선점하지 못하도록 하고, kernel -> user mode로 돌아갈때 CPU를 넘겨준다

<br>

> **Race Condition in Multi-Processor's shared memory**

- 해결책
  - 한번에 하나의 CPU만 커널에 들어갈 수 있게 하는 방법
    - 비효율적
  - 커널 내부에 있는 각 공유 데이터에 접근할 때마다 그 데이터에 대한 lock/unlock를 수행

<br>

ref. <a href="http://www.kocw.net/home/search/kemView.do?kemId=1226304&ar=relateCourse">KOCW</a>