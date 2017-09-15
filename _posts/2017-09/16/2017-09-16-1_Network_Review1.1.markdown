---

layout: post
title: "(Network) Network 리뷰"
category: Network

---

# Network 리뷰
## 시작하면서
> 네트워크 수업을 들은지 시간이 꽤 지나 OS처럼 보자마자 기억이 날 것 같지 않아 시간이 많이 걸릴 것 같다. 그래도 기본을 다지고 이전에 놓쳤었던 중요한 개념들이 뭐가 있는지 볼 수 있는 시간이 되었으면 좋겠다.

## (흠?)은 뭐지
* 과연 여기까지 나올까 싶은 것들은 흠? 을 앞에 붙여봤다.. 물론 제 주관이니 아무 의미 없는 것이라고 말할 수 있다. 

## Chapter2(The OSI Model and the TCP/IP protocol suite)
1. TCP/IP protocol suite에 대해 설명해 보자(5 Layer)
    * 물리(Physical): 기계적 신호로 변환하고 전달하는 곳
    * 데이터링크(L2, Data link): router to router(`hop to hop`)전달이 이뤄짐. 헤더 안 Mac주소(Physical Addr, 제조사가 각 랜카드에 부여하는 번호)를 보고 전달. 
    * 네트워크(L3, Network): IP주소(logical Addr)가 헤더 안으로 들어가 라우팅 경로가 설정된다(`Source to Destination`), router
    * 전송(L4, Transport): port번호를 보고 전달(`Process to Process`)
    * 응용(Application): 자원을 받아들이고 전달, 관리 등이 이뤄짐

2. 그럼 패킷이 여러 네트워크와 라우터를 거쳐서 전달되는 과정을 설명해 볼 수 있을까?
    * 먼저 보내는 곳에서 데이터에 IP(보내는곳, 도착해야 하는 곳), 그리고 시작 맥주소, 다음 맥주소가 헤더에 담겨서 같이 보내지게 된다. 맥 주소를 비교하면서 다른 네트워크에 도착하게 되면 도착 IP주소를 비교하여 Destination을 확인하고 아닐 경우 MAC주소를 변경하여 전달하게 됩니다. 다음 맥주소는 Routing table을 통해 확인하게 됩니다. 아무튼 이러한 전송과정에서 MAC주소는 계속해서 변경되지만 PORT번호나 IP주소는 변경되지 않는다.

3. (흠?) IP만 보고서 전달이 되는거 아닌가 그럼? MAC주소는 왜 필요한가?
    * 애초에 네트워크가 처음 설계될 때 IP주소가 먼저 생긴 것이라 MAC주소부터 생겼다고..

## Chapter4(Introduction to Network Layer)
1. circuit switching, packet sitching 차이점은 뭐일까?
    * circuit switching: 중앙 통제하에 일어난다. 경로 설정을 set up과정 서 미리 해놓은 뒤 사용한다. 그 경로만 사용하며 손실은 적으나 비효율적이고 한 경로가 손상되면 사용할 수 없게된다. 패킷이 분리되지 않고 한번에 전달된다.
    * packet switching: 라우터들끼리 분산된 정보를 주고 받는다. 손실이 있을 수 있지만 유연하고 한 경로에 의존적이지 않게 된다. 패킷을 분리해서 보내고 destination의 transport계층에서 재 조립해서 사용하게 된다. 다음 경로를 담고 있는 table의 값이 바뀔 수 있다.(더 좋은 경로를 찾아)

## Chapter15(Transmission Control Protocol)
1. (흠?)Acknowledgement 방식에 대해 설명해보자
    * selective 방식: 손실된 Segment때문에 Ack을 다시 보낼 때 이미 받은 segment정보를 같이 보내줌
    * cumulative 방식: 손실된 Segment를 받기 전 여기까지 받았다 라는 것을 number로 알려줌. TCP가 이런 방식.

2. TCP Header에 어떤 정보들이 들어갈까?
    * Source port addr, Dest Port addr
    * Sequence number: packet 번호
    * Acknowledgement number
    * window size: 얼만큼 더 받을 수 있다 라는 것을 알려줄 때 사용
    * Checksum: 전송중에 비트가 바뀌는 경우 error detection용으로 가지고 다님. 반드시 체크를 하고 받아야 한다. 16비트씩 잘라서 더하고 보수를 취해서 나중에 checksum과 데이터를 더했을 때 0이 되면 오류가 없는 것으로 판단한다. 
    * Urgent pointer: 
    * 등등등...

3. Three-way handshake에 대해 설명해보자
    * TCP프로토콜에서 장치들 끼리 논리적인 접속을 성립하기 위해 3 way handshake를 사용하게 된다.
    * 먼저 client에서 server쪽으로 연결을 하게 될 때 `SYNchronized` packet을 보낸다.
    * 서버쪽에서 수신을 한 뒤 동의할 경우 `SYNchronized` packet과 `Acknowledgement` packet을 한 묶음으로 같이 보낸다. 
    * 이에 대한 응답으로 서버측에 `Acknowledgement` packet을 보내 서로 연결을 확립한다.
    * 이 과정에서 데이터를 주고 받을수는 없지만 서로 필요한 데이터들의 sequence #를 확인할 수 있다.

4. Four-way handshake에 대해 설명해보자
    * 연결 종료시 사용되는 방법입니다.
    * 먼저 클라이언트가 연결을 종료하겠다는 `FIN` packet을 보내게 됩니다.
    * 서버는 이러한 메세지를 받았다는 `ACK` packet을 보내주고 자신의 통신이 끝날때 까지 TIME_WAIT상태에 빠져듭니다.
    * `ACK`을 받은 클라이언트는 전송을 하는 버퍼를 지우고 수신만 할 수 있는 상태가 됩니다.(이 경우 ACK은 보낼 수 있습니다.)
    * 서버가 통신이 종료되면 클라이언트 쪽으로 `FIN` packet을 보내주게 됩니다.
    * 그리고 클라이언트는 이 패킷을 받고 서버쪽으로 `ACK` packet을 보내고 클라이언트는 TIME_WAIT 시간 동안 기다리며 늦게 도착하는 패킷이 있는지 기다린 후 종료를 하게 됩니다. `ACK`을 받은 서버는 바로 연결을 종료하게 됩니다. 

5. TCP에서 window에 대해 설명해봐라
    * 기본적으로 stop & wait 방식(데이터를 보내고 응답이 다음것을 보내주고..)이 너무 비효율적이어서 나온 방법이다.
    * 첫번째 데이터를 보낸것에 대해 응답이 오기 전까지 window크기가 허락하는만큼 계속해서 데이터를 보내준다. ACK이 오지않아도 계속 보낸다.
    * 이 window의 크기는 수신하는 곳의 버퍼에서 일을 가져가는 속도와 보낼 수 있는 것, 받는 버퍼의 크기 등을 고려해서 정해진 뒤 헤더에 담겨서 오게 된다. 그럼 좀 더 효율적으로 데이터를 보낼 수 있게 되겠지!

6. `Silly Window Syndrome`에 대해 설명해보자
    * 수신 측에서 데이터를 처리하는 속도가 늦어져 윈도우의 크기가 계속해서 감소되어 송신측으로 보내지게 된다.
    * 그러면 그 윈도우 크기를 보고 송신 측에서는 더 작고 더 자주 패킷을 쪼개 보내게 된다.
    * 이렇게 작은 패킷을 계속해서 보내게 되니 매우 비효율 적이라고 할 수 있다.

7. 그럼 어떻게 해결할까?
    * 송신 측에서는 `Nagle Algorithm`이라고 하는데 첫번째 packet은 일단 보내고 응답이 올때 까지 기다리면서 데이터를 모아서  패킷이 꽉차면 전송시킨다. 그리고 첫번째 것의 Ack이 올 때 까지 전송을 멈추게 된다.
    * 수신 측에서는 `Clark` 해결 방법이라고 하는데 윈도우의 크기가 MMS(Maximum Segment Size)나 버퍼의 크기가 반이 될 때까지 받을 수 없다고 ACK을 계속해서 보내게 된다.

8. `SYN Flooding`이란?
    * 악성적으로 계속해서 연결을 만들어 SYN을 보내고 스푸핑으로 IP를 변경시켜 SYN+ACK을 받지 않는다.
    * 이렇게 되면 서버쪽에서는 SYN+ACK을 보낸것에 대해 ACK을 기다리면서 연결요청 대기 큐에 쌓이게 되는데 
    * 이렇게 대기큐가 쌓이게 됨으로써 정상적인 사용자들의 일을 제대로 할 수 없게 한다.

## 부수적인 HTTP 공부

## 마치며

<br/><br/>
