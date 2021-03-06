---
layout: post
title:  "TCP 송수신 과정(2)"
category: Network
tags: [Network]
comments: true
---



## TCP의 통신 과정 (2)



프로토콜 스택은 받은 데이터를 곧바로 송신하는 것이 아니라 일단 자체의 내부에 있는 송신용 버퍼용 메모리 영역에
저장하고 특정 요소에 따라 송신을 결정한다.



**프로토콜 스택이 송신하기 위한 요소**

> 1. **MTU**
> 2. **타이밍**





> **MTU**

- 프로토콜 스택은 MTU라는 매개변수를 바탕으로 송신을 결정한다.<br>
  MTU는 한 패킷으로 운반할 수 있는 디지털 데이터의 최대 길이로, 이더넷에서는 보통 1,500 바이트가 된다.
- **MTU에는 패킷의 맨 앞부분에 헤더가 포함되어 있으므로 여기부터 헤더를 제외한 것이 하나의 패킷으로 운반할 수 있는**
  **최대 길이가 되고, 이 것을 MSS라고 합니다.**





<img src="/assets/post-img/network/mtsMss.jpeg">







> **타이밍**

- 애플리케이션의 송신 속도가 느려지는 경우 MSS에 가깝게 데이터를 저장하면 여기에서 시간이 걸려 <br>
  송신 동작이 지연되므로 버퍼에 데이터가 모이지 않아도 적당한 곳에서 송신 동작을 실행해야 한다.<br>

  따라서 프로토콜 스택은 내부에 타이머가 있어서 이것으로 일정시간 이상 경과하면 패킷을 송신한다.






> **데이터가 클 때는 분할해서 보낸다**

- HTTP 리퀘스트 메시지 보통 길지 않으므로 한 개의 패킷에 들어가지만, 폼을 사용하여 긴 데이터를 보낼 경우 등<br>

  한 개의 패킷에 들어가지 않을 만큼 긴 것도 있다.

  이 경우 송신 버퍼에 들어있는 데이터를 맨 앞부터 차례대로 MSS 크기에 맞게 분할하고 <br>

  분할한 조각을 한 개씩 패킷에 넣어 송신한다.





<img src="/assets/post-img/network/divisionPacket.jpeg">





> **데이터 송∙수신 과정**





<img src="/assets/post-img/network/tcpNetwork.jpeg">





1. 서버측에서 애플리케이션이 동작하기 시작할 때 소켓을 만들고 접속 대기상태로 존재한다.
2. 클라이언트측에서 소켓을 만든다.
3. 그림 ① : SYN을 1로 만들고 시퀀스번호 **초기값[1]**, **윈도우[2**]로 TCP 헤더를 만들어 서버에 보낸다.

4. 그림 ② : 이 것이 서버에 도착하면 서버에서 SYN을 1로 만들고 시퀀스 번호와 윈도우, **ACK 번호[3]**로 TCP 헤더를 만들어 클라이언트의 요청에 응답한다.
5. 그림 ③ : 이 것이 클라이언트에 도착하면 TCP 헤더를 받은 것을 나타내는 ACK 번호를 기록한 TCP 헤더를 <br>
   클라이언트가 서버에 보낸다. 이것으로 접속 동작은 끝나고 데이터 송∙수신 단계에 들어간다.

6. 그림 ④ : 웹의 경우 클라이언트에서 서버에 리퀘스트 메시지를 보내는 것부터 시작한다.<br>

   TCP는 이것을 적당한 크기의 조각으로 분할하고 TCP 헤더를 맨 앞에 부가하여 서버에 보낸다.

7. 그림 ⑤ : TCP 헤더에 송신 데이터가 몇 번째 바이트부터 시작되는지를 나타내는 시퀀스 번호가 기록되어 있을 것(그림④)이고,  이 것이 서버에 도착하면 서버는 ACK 번호를 클아이언트에 반송한다. <br>

   최초의 데이터 조각인 경우 서버는 데이터를 받기만 하지만, 데이터 송∙수신이 진행되면 애플리케이션에 데이터를 건네주어수신 버퍼에 빈 영역이 생기는 장면이 나오는데, 이때 윈도우의 값도 기록하여 클라이언트에 통지한다.

8.  서버가 응답 메시지 보내기를 완료하면 데이터 송∙수신 동작이 끝나므로 연결 끊기 동작에 들어간다. 

   웹의 경우 서버에서 연결 끊기 동작에 들어간다.  <br>그림 ⑧ : 서버에서 먼저 FIN을 1로 만든 TCP 헤더를 클라이언트에 보낸다.

9. 그림 ⑨ : 이 것을 받았음을 나타내는 ACK 번호의 TCP 헤더가 클라이언트에서 서버로 돌아온다.

10. 그림 ⑩ : 이후 클라이언트가 FIN을 1로 만든 TCP 헤더를 서버에 보낸다.

11. 그림 ⑪ : 서버에 받았다는 의미의 ACK 번호의 TCP 헤더를 클라이언트에 반환하고 소켓이 말소된다.



**TCP는 통신 과정에서 ACK 번호가 돌아오지 않으면 패킷을 다시 보낸다.** <br>
**다른 곳(LAN 어댑터,라우터, 버퍼 등)에서 오류조치할 필요가 없다.**



[1] 시퀀스 번호

- 시퀀스 번호는 데이터를 조각으로 분할하여 송신할 때 몇번 째 바이트에 해당하는지를 나타내는 것으로써<br>

  보통 1부터 시작하지 않고 난수를 바탕으로 산출한 초기값으로 시작한다.<br>

  항상 1부터 시작한다면 악의적인 공격을 할 우려가 있기 때문이다.<br>

  

[2] 윈도우

- 송신 측에 수신 가능한 데이터 양을 통지하고, 수신측은 이 양을 초과하지 않도록 송신 동작을 진행하는데 <br>
  수신가능한 양을 윈도우라 한다.<br>



[3]ACK 번호

- 수신자가 예상하는 다음 시퀀스 번호이다. 이것은 모든 선행하는 바이트들(존재할 경우)에 대한 수신에 대한 확인응답이 된다.
- 한쪽이 보낸 최초의 `ACK`는 반대쪽의 초기 시퀀스 번호 자체에 대한 확인응답이 되며, 데이터에 대한 응답은 포함되지 않는다.



ref <a href="https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=163484025">성공과 실패를 결정하는 1% 네트워크 원리</a>

ref <a href="[https://ko.wikipedia.org/wiki/%EC%A0%84%EC%86%A1_%EC%A0%9C%EC%96%B4_%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C](https://ko.wikipedia.org/wiki/전송_제어_프로토콜)">wiki</a>

