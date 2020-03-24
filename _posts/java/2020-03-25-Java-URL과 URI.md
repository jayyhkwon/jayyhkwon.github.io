---
layout: post
title:  " URL과 URI "
category: Java
tags: [Java]
comments: true
---



## URL과 URI



>  **URI (Uniform Resource Identifier)**

- 추상적이거나 또는 물리적인 자원을 완전히 완전히 구분할 수 있는 문자열





>  **URL (Uniform Resource Locator)**

- URI의 부분집합. 
- URL + 자원이 어디에 위치하는 지 나타낸다



**모든 URL은 URI이지만 역은 성립하지 않는다**



#### 예시

![difference between a uri and a url](https://res.cloudinary.com/practicaldev/image/fetch/s--lrbx3qNQ--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/j4bka41nypm4do1f3e5b.JPG)



​	이름은 URI이지만, URL은 아니다. 이름을 안다고 해서 어디에 위치하는지 알 수 없기 때문이다.

​	반면 주소는 URI이면서 URL이다. 주소를 알면 내가 누군지 알 수 있으며, 어디에 위치하는지 또한 알 수 있기 때문이다





>  **Syntax**
>
> ​	모든 URI는 다음 형태를 가진다.
>
> ​	scheme: [//authority] [/path] [?query] [#fragment]



- **scheme**
  - URL의 경우 이것은 자원에 접근하기 위한 프로토콜에 해당한다
- **authority**
  - authority   = [ userinfo "@" ] host [ ":" port ]
  - 유저 권한정보(옵션), 호스트(필수), 포트(옵션)으로 구성된다
- **path**
  - scheme와 authority에서 자원을 구별하는 역활을 한다
- **query**
  - path 뒤에 오는 추가적인 정보로 자원을 구별하는 역활을 한다.
- **fragment**
  - 특정 부분의 자원을 나타내는 옵션





> **URI, URL class in JAVA**
>
> ​	URI 클래스만이 모든 syntax 구성요소에 대한 생성자를 가진다



```java
@Test
public void whenCreatingURIs_thenSameInfo() throws Exception {
    URI firstURI = new URI(
      "somescheme://theuser:thepassword@someauthority:80"
      + "/some/path?thequery#somefragment");
     
    URI secondURI = new URI(
      "somescheme", "theuser:thepassword", "someuthority", 80,
      "/some/path", "thequery", "somefragment");
 
    assertEquals(firstURI.getScheme(), secondURI.getScheme());
    assertEquals(firstURI.getPath(), secondURI.getPath());
}
 
@Test
public void whenCreatingURLs_thenSameInfo() throws Exception {
    URL firstURL = new URL(
      "http://theuser:thepassword@somehost:80"
      + "/path/to/file?thequery#somefragment");
    URL secondURL = new URL("http", "somehost", 80, "/path/to/file");
 
    assertEquals(firstURL.getHost(), secondURL.getHost());
    assertEquals(firstURL.getPath(), secondURL.getPath());
}
```





ref. <a href="https://tools.ietf.org/html/rfc3986#section-3.1">RFC 3986</a><br>

ref. <a href="https://www.baeldung.com/java-url-vs-uri">baeldung</a>

