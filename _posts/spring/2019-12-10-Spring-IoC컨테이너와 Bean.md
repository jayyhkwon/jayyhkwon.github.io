

### IoC Container와 Bean

----



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





ref. <a href="https://docs.spring.io/spring-framework/docs/current/spring-framework-reference/core.html">spring.io</a><br>

ref. <a href="https://www.inflearn.com/course/spring-framework_core/lecture/15506">스프링 프레임워크 핵심 기술</a>