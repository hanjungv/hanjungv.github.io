---

layout: post
title: "(CS) Network 리뷰"
category: CS

---

# Network 리뷰
## 시작하면서
> 네트워크 수업을 들은지 시간이 꽤 지나 OS처럼 보자마자 기억이 날 것 같지 않아 시간이 많이 걸릴 것 같다. 그래도 기본을 다지고 이전에 놓쳤었던 중요한 개념들이 뭐가 있는지 볼 수 있는 시간이 되었으면 좋겠다.

## (흠?)은 뭐지
* 과연 여기까지 나올까 싶은 것들은 흠? 을 앞에 붙여봤다.. 물론 제 주관이니 아무 의미 없는 것이라고 말할 수 있다. 

## Chapter 2(The OSI Model and the TCP/IP protocol suite)
1. TCP/IP protocol suite에 대해 설명해 보자(5 Layer)
    * 물리(L1, Physical): 기계적 신호로 변환하고 전달하는 곳
    * 데이터링크(L2, Data link): router to router(`hop to hop`)전달이 이뤄짐. 헤더 안 Mac주소(Physical Addr, 제조사가 각 랜카드에 부여하는 번호)를 보고 전달. 
    * 네트워크(L3, Network): IP주소(logical Addr)가 헤더 안으로 들어가 라우팅 경로가 설정된다(`Source to Destination`), router
    * 전송(L4, Transport): port번호를 보고 전달(`Process to Process`)
    * 응용(Application): 자원을 받아들이고 전달, 관리 등이 이뤄짐

2. 그럼 패킷이 여러 네트워크와 라우터를 거쳐서 전달되는 과정을 설명해 볼 수 있을까?
    * 먼저 보내는 곳에서 데이터에 IP(보내는곳, 도착해야 하는 곳), 그리고 시작 맥주소, 다음 맥주소가 헤더에 담겨서 같이 보내지게 된다. 맥 주소를 비교하면서 다른 네트워크에 도착하게 되면 도착 IP주소를 비교하여 Destination을 확인하고 아닐 경우 MAC주소를 변경하여 전달하게 됩니다. 다음 맥주소는 Routing table을 통해 확인하게 됩니다. 아무튼 이러한 전송과정에서 MAC주소는 계속해서 변경되지만 PORT번호나 IP주소는 변경되지 않는다.

3. (흠?) IP만 보고서 전달이 되는거 아닌가 그럼? MAC주소는 왜 필요한가?
    * 애초에 네트워크가 처음 설계될 때 IP주소가 먼저 생긴 것이라 MAC주소부터 생겼다고..

## Chapter 4(Introduction to Network Layer)
1. circuit switching, packet sitching 차이점은 뭐일까?
    * circuit switching: 중앙 통제하에 일어난다. 경로 설정을 set up과정 서 미리 해놓은 뒤 사용한다. 그 경로만 사용하며 손실은 적으나 비효율적이고 한 경로가 손상되면 사용할 수 없게된다. 패킷이 분리되지 않고 한번에 전달된다.
    * packet switching: 라우터들끼리 분산된 정보를 주고 받는다. 손실이 있을 수 있지만 유연하고 한 경로에 의존적이지 않게 된다. 패킷을 분리해서 보내고 destination의 transport계층에서 재 조립해서 사용하게 된다. 다음 경로를 담고 있는 table의 값이 바뀔 수 있다.(더 좋은 경로를 찾아)

## Chapter 15(Transmission Control Protocol)
1. (흠?)Acknowledgement 방식에 대해 설명해보자
    * selective 방식: 손실된 Segment때문에 Ack을 다시 보낼 때 이미 받은 segment정보를 같이 보내줌
    * cumulative 방식: 손실된 Segment를 받기 전 여기까지 받았다 라는 것을 number로 알려줌. TCP가 이런 방식.

2. (흠?)TCP Header에 어떤 정보들이 들어갈까?
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

6. (흠?)`Silly Window Syndrome`에 대해 설명해보자
    * 수신 측에서 데이터를 처리하는 속도가 늦어져 윈도우의 크기가 계속해서 감소되어 송신측으로 보내지게 된다.
    * 그러면 그 윈도우 크기를 보고 송신 측에서는 더 작고 더 자주 패킷을 쪼개 보내게 된다.
    * 이렇게 작은 패킷을 계속해서 보내게 되니 매우 비효율 적이라고 할 수 있다.

7. (흠?)그럼 어떻게 해결할까?
    * 송신 측에서는 `Nagle Algorithm`이라고 하는데 첫번째 packet은 일단 보내고 응답이 올때 까지 기다리면서 데이터를 모아서  패킷이 꽉차면 전송시킨다. 그리고 첫번째 것의 Ack이 올 때 까지 전송을 멈추게 된다.
    * 수신 측에서는 `Clark` 해결 방법이라고 하는데 윈도우의 크기가 MMS(Maximum Segment Size)나 버퍼의 크기가 반이 될 때까지 받을 수 없다고 ACK을 계속해서 보내게 된다.

8. `SYN Flooding`이란?
    * 악성적으로 계속해서 연결을 만들어 SYN을 보내고 스푸핑으로 IP를 변경시켜 SYN+ACK을 받지 않는다.
    * 이렇게 되면 서버쪽에서는 SYN+ACK을 보낸것에 대해 ACK을 기다리면서 연결요청 대기 큐에 쌓이게 되는데 
    * 이렇게 대기큐가 쌓이게 됨으로써 정상적인 사용자들의 일을 제대로 할 수 없게 한다.

9. (흠?)packet loss가 일어나면 어떻게 할까?
    1. 먼저 일반적으로 데이터를 전송한 것에 대한 응답으로 ACK이 오게 되는데 이 때 받은 ACK에서 다음 데이터를 원하게 된다고 치면
        * 보내줄 데이터가 아직 버퍼에 차지 않았을 경우 일정한 시간동안 기다렸다가 데이터가 오게 되면 보내준다.
        * 이 때 중간에 또 다른것도 보내달라는 요청이 오게 될 경우 이에 대한 응답으로 ACK을 보내준다.
    2. 근데 만약 이에 대한 응답으로 패킷을 전송했는데 먼저 보낸 패킷이 중간에서 전달이 안되고 다음 전송된 데이터가 먼저 도착할 경우 순서가 바뀌게 된 것이므로(out of order)이에 대해 이전 것이 안왔다고 packet loss를 알려주는 ACK을 바로 보내주게 된다. ACK을 받고 일정시간(time out)될 때까지 데이터가 왔다는 ACK이 안 올 경우 다시 재전송을 해준다. 
    3. 그 ACK을 수신한 측은 다시 데이터를 보내주고 이에대한 ACK을 송신한 쪽에 바로 보내준다. 
    4. `Fast retransmission`은 위 방법에서 time out이 될 때까지 기다리는 방법 대신 3번의 ACK(`Three duplicated Ack`)을 받게 될 동안 데이터가 안오게 되면 time out이 되지 않더라도 바로 전송해주는 방식이다. 3번을 받게 되는 이유는 한번에 바로 유실되었다고 판단하기에 무리가 있어 3번의 유예를 두는 것이라고 한다.
    5. 만약 송신이 제대로 되었는데 이것에 대한 ACK이 loss될 경우 일정시간동안 기다리다가 재 전송을 해주게 된다. 이 재전송한 데이터가 이미 온 것일 경우 수신측에서는 바로 ACK을 다시 전송해주고 반영시켜준다.

10. (흠?)congestion을 어떻게 control할까?
    * 처음에는 윈도우 크기만큼 전송을 했었지만 현재는 `Slow Start`로 exponential increase하여 전송한다. RTT(Rount Trip Time)동안 전송한 윈도우 크기만큼 송신측에서 감당이 된다면 2배씩 증가하면서 전송을 늘리게 된다.
    * Threshold 지점까지 exponential하게 증가하고 그 지점 이후부터는 하나씩 증가하면서 RTT내에 응답이 오는지 체크하며 증가하게 됩니다. 만약 3 duplcated ACK이 발생하게 되면 congestion이 발생한것으로 하고 threshold를 contestion이 발생한 윈도우 사이즈의 1/2로 줄인 뒤 다시 슬로우 스타트를 하게 됩니다. 

## Chapter 5(IPv4 Addresses)

1. IPv4와 IPv6의 차이점은?
    * IPv4는 총 32비트가 IP주소로 쓰임. 40억개 정도
    * IPv6는 총 128비트가 IP주소로 쓰임. 

2. 서브넷(`subnet`)으로 관리하는 이유는?
    * 만약 classB를 구매하여 하나의 스위치에 한 네트워크 주소로 연결이 되어있다면 이 스위치에는 6만5천개 정도가 한 스위치에 몰려있는 것을 의미한다. 이렇게 될 경우 broadcasting(s:0.0.0.0, d:255.255.255.255) 하게 될 때 매우 bandwidth활용이 낮아지고 관리 또한 힘들어진다. 또 스위치 하나가 고장나게 될 경우 모든 네트워크가 사용을 못하게 되는 문제가 발생한다.
    * 서브넷으로 관리하여 netid비트를 제외하고 hostid 비트에서 몇자리를 추출하여 앞자리를 netid에 더하여 subnetid로 만들어 관리하게 되면 네트워크 주소가 나눠지게 된다. 만약 뒤 2비트를 추가하여 subnetid를 만들 경우 4개의 서브넷이 만들어진다. 
    * 서브넷의 서브넷을 만들어 관리 할 수 있고 classless인 주소 체계에서도 서브넷을 만들어 관리 할 수 있다.

## chapter 6(Delevery and Forwarding of IP packets)
1. `Longest mask matching`이란 개념은?
    * IP 경로가 매칭되는 곳이 여러개일 경우 network ID가 가장 길게 매칭되는 곳으로 보내버리는것을 의미한다.

## chapter 7(Internet Protocol version4)
* IP헤더에도 checksum이 존재한다..작동원리는 같다

## chapter 8(Address Resolution Protocol)
1. ARP의 역할은?
    * IP주소를 통해 MAC주소를 알아낼 수 있음. Network계층에서 작동된다. Next hop에 대한 정보를 알기 위해 쓰인다.  
    * broadcast로 리퀘스트를 보내고 reply는 unicast로 온다.
    * 먼저 캐싱테이블에 있는 MAC주소를 찾아보고 없으면 request를 보낸다.

## chapter 9(Internet Control Message Protocol Version 4)
1. ICMP의 역할은?
    * 인터넷은 중앙 통제이기 때문에 모니터링이 힘들다.
    * 에러가 발생할 경우 리포팅이 필요한데 원래 소스로 에러 코드를 담아 보내주는 역할을 ICMP가 한다. IP와 같은 Network계층에서 작업이 된다.

## 그 외..
* TCP랑 UDP랑 차이점?
    * TCP(Transmission Control Protocol) : 연결형 서비스를 지원하는 전송계층 프로토콜, 호스트간 신뢰성 있는 데이터 전달과 흐름제어 및 혼잡제어 등을 제공하는 전송계층
        - 가상 회선 연결 방식, 연결형 서비스를 제공
        - 높은 신뢰성(Sequence Number, Ack Number를 통한 신뢰성 보장)
        - 데이터 흐름 제어(수신자 버퍼 오버플로우 방지) 및 혼잡 제어(네트워크 내 패킷 수가 과도하게 증가하는 현상 방지)

    * UDP(User Datagram Protocol)
        * 비연결형 서비스를 지원하는 전송계층 프로토콜
        * 보내는 쪽에서 일방적으로 데이터를 전달하는 통신 프로토콜
        - 비연결형(port만 확인하여 소켓을 식별하고 송수신)
        - 비신뢰성
        - 오류검출(헤더에 오류 검출 필드를 포함하여 무결성 검사)
        - UDP는 TCP와 달리 데이터의 수신에 대한 책임을 지지 않는다.

## 부수적인 HTTP 공부
* 참조[https://developer.mozilla.org/ko/docs/Web/HTTP/Overview](https://developer.mozilla.org/ko/docs/Web/HTTP/Overview)
* HTTP가 뭘까?
    * HTTP(HyperText Transfer Protocol)의 줄임말이다. 클라이언트(사용자)와 서버단의 통신은 HTTP를 통해 request, response가 이루어진다. HTTP는 응용계층에서 사용되는 프로토콜이다.
* HTTP 메세지에는 어떤 것들이 포함 될 수 있을까?
    * 참조링크[https://developer.mozilla.org/ko/docs/Web/HTTP/Messages](https://developer.mozilla.org/ko/docs/Web/HTTP/Messages)
    * HTTP/2 이전에는 모든 메세지는 ASCII로 인코딩 된 정보로 이루어져 있었습니다. HTTP/2 부터는 인간이 읽을 수 있는 메세지로 인코딩 된다고 합니다.
        * 그럼 이게 왜 성능을 더 올리지?
    * 헤더를 보면
    ```
    HTTP 메서드, URL(request target), HTTP버전
    (req일 경우)
    host : 호스트 주소
    User-Agent: 요청을 보낸 곳의 브라우저 환경, OS같은거..
    Accept: 받아들일 타입들을 한정 시킬 수 있다. Language, encoding등을 한정 시킬 수 있다.
    (req일 경우)
    (res일 경우)
    Server: 서버이름
    Set-Cookie: 쿠키설정
    Access-Control-Allow-origin: 받아들일 곳
    (res일 경우)
    Connection: keep-alive
    Content-Encoding: gzip
    ...
    ```

* HTTP Method에 어떤것들이 있는지 설명해 볼 수 있을까?
    * GET, POST, PUT, DELETE 그리고 멱등성(idempotence)?
    * POST vs PUT, 그리고 PUT과 PATCH?
        * [PUT과 PATCH, 참조](http://weblog.rubyonrails.org/2012/2/26/edge-rails-patch-is-the-new-primary-http-method-for-updates/)

    * DELETE는 Body가 없다?

* 세션이랑 쿠키랑 차이점이 뭘까?
* 그럼 세션이랑 쿠키랑 어디에 쓰이는가?
* 프록시는 뭘까?
    * Application 계층에서 HTTP 메세지들과 여러 컴퓨터들을 릴레이 하는 곳을 프록시라고 합니다. 프록시를 통해 여러 요청을 수행할 수 있습니다. 
        * 캐싱, 로드밸런싱, 보안인증 등등..
* CDN은 뭐야?


## 마치며

<br/><br/>
