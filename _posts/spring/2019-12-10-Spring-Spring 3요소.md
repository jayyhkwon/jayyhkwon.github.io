---
layout: post
title:  "Spring 3요소"
category: Spring
tags: [Spring]
comments: true
---



## Spring의 3요소 



### 1. IoC Container



> **Inversion of Control** 

- 의존 관계 주입이라고도 하며, 어떤 객체가 사용하는 의존 객체를 직접 만들어 사용하는게 아니라 
  주입받아 사용하는 방법을 말한다.



>  **스프링 IoC 컨테이너**

- BeanFactory
- 애플리케이션 컴포넌트의 중앙 저장소
- 빈 설정 소스로부터 빈 정의를 읽어들이고, 빈을 구성하고 제공한다.





![container magic](https://docs.spring.io/spring-framework/docs/current/spring-framework-reference/images/container-magic.png)



> **Bean**

- 스프링 IoC 컨테이너가 관리하는 객체
- 스프링이 의존성 관리를 해준다
- Scope
  - Singleton(default)
  - Prototype : 매번 다른 객체를 생성한다
- 라이프사이클 인터페이스를 가진다



> **ApplicationContext**

- BeanFactory
- 메시지 소스처리 기능(i18n)
- 이벤트 발행 기능
- 리소스 로딩 기능
- 구현체
  - [`ClassPathXmlApplicationContext`](https://docs.spring.io/spring-framework/docs/5.2.2.RELEASE/javadoc-api/org/springframework/context/support/ClassPathXmlApplicationContext.html)
  - [`FileSystemXmlApplicationContext`](https://docs.spring.io/spring-framework/docs/5.2.2.RELEASE/javadoc-api/org/springframework/context/support/FileSystemXmlApplicationContext.html)
  - AnotationConfigApplicationContext



> **Configuration Metadata**

- Xml 기반 Config
- Java 기반 Config

- 최근에는 Java Config를 많이 사용하는 추세



---



### 2. AOP

> **AOP 구현방법 **

- 컴파일
  - A.java ---(AOP) --- > A.class (AspectJ)
- 바이트코드 조작
  - A.java -> A.class ---(AOP) ---> 메모리(AspectJ)
- 프록시 패턴
  - 스프링 AOP
    - @Transactional 애노테이션을 사용하면 해당 인터페이스 또는 클래스의 메서드 앞뒤에 부가적인 코드를 추가한 프록시 객체를 생성하여 빈으로 대신 등록하고 스프링이 호출한다



AOP 적용예제

@LogExecutionTime으로 메서드 처리 시간 로깅하기



**@LogExecutionTime 애노테이션 (어디에 적용할지 표시 해두는 용도)**

```java
@Target(ElementType.METHOD) // 애노테이션 적용 대상
@Retention(RetiontionPolicy.RUNTIME) // 애노테이션을 유지 기간
public @interface LogExecutionTime{
}
```



**실제 Aspect (@LogExecutionTime 애노테이션 달린 곳에 적용)**

```java
@Component
@Aspect
public class LogAspect{
  
   Logger logger = LoggerFactory.getLogger(LogAspect.class);

    @Around("@annotation(LogExecutionTime)")
    public Object logExecutionTime(ProceedingJoinPoint joinPoint) throws Throwable{
        StopWatch stopWatch = new StopWatch();
        stopWatch.start();

        Object proceed = joinPoint.proceed();

        stopWatch.stop();
        logger.info(stopWatch.prettyPrint());

        return proceed;
    }
  
}
```



---

<br>

### 3. PSA 

- @GetMapping, @PostMapping과 같은 애노테이션을 사용하면 HttpServlet 클래스를 상속받은 Servlet을 구현한 클래스를 작성할 필요가 없다. 네티 기반 webflex도 코드의 변경없이 사용가능하다.
- 이처럼 추상화 계층을 이용하여 개발하면 구현체가 무엇이든 신경쓸 필요가 없다. 스프링이 알아서 처리하여 주기 때문이다
- @Transactional 애노테이션도 마찬가지이다. JPA, Hibernate, JDBC를 사용하든 스프링이 알아서 처리해준다.



ref. <a href="https://docs.spring.io/spring-framework/docs/current/spring-framework-reference/core.html">spring.io</a><br>

ref. <a href="https://www.inflearn.com/course/spring-framework_core/lecture/15506">스프링 프레임워크 핵심 기술</a>