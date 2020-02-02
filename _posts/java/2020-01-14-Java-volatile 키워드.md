---
layout: post
title:  " volatile 키워드 "
category: Java
tags: [Java]
comments: true
---





## volatile 키워드

> **volatile은 변수의 가시성을 보장한다**

- Java volatile 키워드는 멀티스레딩 환경에서 사용되는 변수의 변화(값의 변화) 에 대한 가시성을 보장한다. 이 말이 좀 추상 적으로 느껴질 수 있는데 자세하게 설명하자면 **non-volatile 변수들로 운영되는 멀티 쓰레드 어플리케이션에서 각 쓰레드들은 성능적인 이유로 메인 메모리로 부터 변수를 읽어 CPU 캐시에 복사하고 작업하게 된다.** 만약 컴퓨터에 하나 이상의 CPU로 구성되어 있다면 각 쓰레드들이 서로 다른 CPU에서 실행 될수 있다. 이 말은 각 쓰레드들이 서로 다른 CPU들의 CPU 캐시에 값을 복사할 수 있다는 것으로 아래의 다이어그램이 이를 설명해주고 있다.

  <br>

  ![0308.jpg](http://thswave.github.io/assets/media/0308.jpg)

  <br>

  

- non-volatile 변수들은 어느 시점에 Java Virtual Machine(JVM)이 메인 메모리로 부터 데이터를 읽어 CPU 캐시로 읽어 들이거나 혹은 CPU 캐시들에서 메인 메모리로 데이터를 쓰는지(write) 보장해 줄 수 없다.

  

> **volatile 키워드는 언제 사용하는 가?**

- Multi Thread 환경에서 하나의 Thread만 read & write하고 나머지 Thread가 read하는 상황에서 `가장 최신의 값을 보장`한다

<br>

2개의 스레드가 하나의 객체를 공유하는 경우를 생각해보자.

- 아래의 객체 StoppableTask는 2개의 메서드를 가지고 있다
  - run() : tellMeToStop()이 호출되기 전까지 무한 루프를 돈다
  - tellMeToStop() : 무한 루프를 끝내는 메서드

```java
    public static class StoppableTask {
        private boolean pleaseStop; 
      
        public void run() {
            while (!pleaseStop) {
                // do some stuff...
                System.out.println("running");
            }
        }

        public void tellMeToStop() {
            pleaseStop = true;
        }
    }
		public static void main(String[] args){
   			StoppableTask task = new StoppableTask();
      	new Thread(() -> task.run()).start(); // 별도의 스레드에서 run() 호출
      	task.tellMeToStop(); // main thread에서 호출
    }
```

- pleaseStop 프로퍼티를 volatile 키워드 없이 선언한다면 JVM은 pleaseStop의 값을 cpu 캐시에서 우선적으로 읽어올 것이다. 따라서 tellMeToStop()이 호출된 직후 바로 무한 루프가 종료되지 않을 수 있다.
- volatile 키워드를 사용한다면, tellMeToStop()이 호출되는 즉시 메인 메모리에 값이 써질 것이고,  별도의 스레드는 그 값을 읽어 while문을 종료할 것이다.

<br>

예제를 하나 더 보자. 싱글턴 패턴 중 DCL을 이용하여 구현한 코드이다

```java
// DCL 
public class MyBrokenFactory {
  private static MyFactory instance;
  private int field1, field2 ...

  public static MyBrokenFactory getFactory() {
1    if (instance == null) {
2      synchronized (MyBrokenFactory.class) {
3        if (instance == null)
4          instance = new MyBrokenFactory();
      }
    }
    return instance;
  }

  private MyBrokenFactory() {
    field1 = ...
    field2 = ...
  }
}
```

- 2개의 스레드가 동시에 getFactory()에 접근하고 thread-1이 먼저 synchronized 블럭에 진입했다고 하자
- thread-1이 1-3까지 실행하고 4번을 실행하는 과정에서 jvm이 다음과 같이 리오더링 할 수 있다.

```java
instance = new MyBrokenFactory();
// jvm이 리오더링(컴파일시 위치최적화)하여 다음과 같이 코드가 변경될 수 있다
// 1) space = MyBrokenFactory를 할당하기 위한 공간
// 2) instance = space
// 3) space = new MyBrokenFactory();
```

- 만약 thread-1이 2)까지 진행한 후 thread-2가 getFactory()에 진입하면 instance는 공간이 할당되어 있으므로 null이 아닐 것이다. 따라서 instance가 리턴될 것이고 instance를 이용한 메서드가 호출되면 에러가 발생할 것이다.
- **volatile로 instance객체를 선언한다면 jvm이 리오더링을 하는 것을 막을 수 있어 해당 문제를 막을 수 있다**



ref. <a href="https://jusungpark.tistory.com/4">블로그</a><br>

ref. <a href="https://www.javamex.com/tutorials/double_checked_locking.shtml">https://www.javamex.com/tutorials/double_checked_locking.shtml</a>