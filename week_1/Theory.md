### 네트워크 구조
network edge
- 애플리케이션과 호스트

network core
- 라우터
- network of networks

access networks, physical media
- communication links

### 네트워크 엣지(network edge)
end systems(hosts)
- 컴퓨터 네트워크에 연결된 컴퓨팅 장치
- 이메일, 웹 브라우저 같은 인터넷 응용 프로그램을 실행시킴

client/server model
- 클라이언트 호스트가 요청하면 상시 가동 중인 서버에서 서비스를 받음
- ex) Web browser/server , email/server

peer-peer model
- 서버이자 클라이언트
- ex) Skype, BitTorrent, KaZaA

### 네트워크 엣지: connection-oriented service
- Goal : end system 간에 데이터 전송

### TCP
- reliabe, in-order byte-stream data transwer
  - 신뢰성, 메시지가 유실되지 않고 전송됨, 순서 지켜줌
- flow control
  - sender가 보내는 속도를 receiver 능력에 맞춰서 알맞게 조절해줌
- congestion control
  - 네트워크 상황에 맞추어서 보내줌

→ 비용이 비쌈 (컴퓨팅 자원, 네트워크 자원 많이 소모)

### Network Core
수많은 라우터들이 그물처럼 얽혀있는 구조

네트워크를 통해 데이터를 전달하는 방식

1. circuit switching
- 출발지에서 목적지까지 가는 길을 미리 예약해놓고 특정 사용자만이 사용하게 만들어놓음
2. packet switching
- 유저가 보내는 패킷을 패킷 단위로 받아서 그때 그때 올바른 방향으로 포워딩 해줌
- 인터넷에서는 이 방식 사용! (속도 때문)

### packet delay (패킷 전송에서의 시간 지연)
1. nodal processing delay

    라우터에서 패킷을 받아서 검사하는데 소요되는 시간
    
    ► 라우터 성능을 개선해서 딜레이를 줄일 수 있다.

2. queueing delay

    나가는 속도보다 들어오는 속도가 빨라서 queue에 임시 저장되는데, 큐에서 기다리는 시간 

    ► 인터넷 사용 패턴에 영향을 받으므로 어쩔 수 없다. 사용자가 몰리다보면 패킷 유실이 일어남

3. transmission delay

    첫번째 bit가 나가는 순간부터 마지막 bit가 링크로 나가는 순간까지 걸리는 시간
    
    ► bandwidth를 늘려서 딜레이를 줄일 수 있다. (케이블 공사)
> R = link bandwidth (bps)
L = packet length (bits)
**time to send bits into link = L/R**


4. propagation delay
마지막 bit가 다음 라우터까지 도달하는데 걸리는 시간
> d = length of physical link
s = propagation speed in medium (빛의 속도)
**propagation delay = d/s**


### 네트워크 계층
네트워크 계층 별로 갖는 대표적인 프로토콜
- APP : HTTP
- Transport : TCP, UDP
- Network : IP
- Link : WIFI, LTE
- Physical Layer

### 클라이언트-서버 구조
server
- 상시 가동 중이어야 함
- 고정된 IP 주소를 가지고 있어야 함

client
- IP 주소가 가변적임

네트워크는 클라이언트 프로세스와 서버 프로세스 사이의 통신이다.

### 소켓 (socket)
프로세스는 프로세스별로 소켓을 만들어서 소켓을 통해서 통신함
클라이언트 프로세스에 있는 소켓에서 메시지를 보내면, 서버 프로세스에 있는 소켓에서 그 메시지를 받는 식

**소켓의 주소**를 알아야 연결할 수 있음
- IP address(어떤 컴퓨터인지) + Port number(어떤 프로세스인지)

#### transport 계층에서 제공해주었으면 하는 기능(희망사항)
data integrity
- 보내는 데이터가 유시되지 않고 온전하게 목적지까지 도착
- 실제로는 이것만 제공해줌! (TCP)

throughput
- 얼마나 많은 데이터가 단위 시간 내 목적지에 전달될 수 있는지

timing
- ex) 보내는 데이터가 10ms 내에 도착했으면 좋겠다.

security
- encryption, data integrity


### HTTP
>**HyperText Transfer Protocol** 의 약자
- 하이퍼텍스트: 웹 페이지에서 볼 수 있는 웹 페이지

HTTP는 하이퍼텍스트를 전달하는 프로토콜

웹에서 클라이언트와 서버는 **HTTP request**와 **HTTP response** 이 두 개의 메시지만으로 통신하게 된다.

#### 특징
1. TCP 사용
	- 클라이언트가 웹에 접속하면 TCP 연결을 생성함
  
2. Stateless (상태가 없다)
	- 서버는 클라이언트 상태에 대한 정보를 기억하지 않음

#### HTTP 연결 방법
- TCP Connection을 만들고 request, response 메시지를 주고 받은 후에 
		1. TCP connection을 끊으면 ▶ **non-persistent HTTP**
    	2. TCP connection을 끊지 않고 계속 유지하면서 재사용 ▶ **persistent HTTP**


---

### 소켓이란?
- 프로세스는 socket을 통해 message를 주고받음
- 소켓이란 OS에서 제공해주는 API 중 하나

#### 타입
1. TCP
	- **reliable delivery**
    : 애플리케이션에서 내려온 메시지가 하나도 유실되지 않고 에러 없이 전달됨
    - in-order guaranteed
    - connection-oriented
    - bidirectional
2. UDP
	- unreliable delivery
    - no order huarantees
    - can send or receive

#### Socket Function (TCP)

![](https://velog.velcdn.com/images/ryujm/post/c6c3c435-ecc2-4f2f-95bf-e421340ba127/image.png)![](https://velog.velcdn.com/images/ryujm/post/3bceb280-98e0-4075-83ba-17179f7c44a0/image.png)

- socket(): 소켓 생성
- bind() : 방금 생성한 소켓을 특정 포트에 bind
- accept() : 클라이언트로부터 connection 될때까지 block 됨
- close() : 데이터 교환이 끝난 후 socket close 해주어야 함

### Multiplexing / demultiplexing
#### Multiplexing 이란?
- Sender 측에서 Application Process 들이 전송하고자 하는 Messages를 TCP implementation 하나에게 보내는 과정
- 여러 개의 메시지가 한 곳으로 감
- Transport Header를 붙여 나중에 Demultiplexing 가능하도록 함

#### Demultiplexing 이란?
- 헤더 정보를 사용하여 수신된 세그먼트를 올바른 소켓에 전달

#### How demultiplexing works
- 호스트는 IP datagram을 받음
  - 데이터 그램에는 source IP 주소, destination IP 주소가 있음
  - datagram은 하나의 전송 계층 세그먼트를 전달
  - 각 세그먼트에는 source Port 번호, destination Port 번호가 있음
- 호스트는 IP 주소 및 포트 번호를 사용하여 세그먼트를 적절한 소켓으로 보냄
> UDP 
>  - dest IP & dest Port (2개 사용)
> 
> TCP
> - src IP & src Port & dest IP & dest Port (4개 사용)

### 네트워크 계층
|계층|프로토콜|
|------|---|
|APP|HTTP|
|Transport|TCP, UDP|
|Network|IP|
|Link|WIFI, LTE|
|PHY||

- TCP, UDP는 Transport 프로토콜로서 기본적으로 상위 레이어인 APP 레이어한테 서비스해주는 기능이 있음 -> Multiplexing & Error checking

   - Error Checking
   Transport 레이어를 사용해서 전달한 메시지는 에러가 있을 경우에 위로 안 올려보냄
   
- 각 레이어는 자신의 상위 레이어에게 서비스를 제공해줌, 하위 레이어로부터 서비스를 제공 받음

   
### Reliable Data Transfer의 원리
- Transfer Layer : Reliable Channel
- Network Layer : Unreliable Channel

Unreliable Channel에서 발생하는 상황
- Message Error
- Message Loss
→ 이 두가지 상황만 잘 처리하면 reliable하게 만들 수 있는 거다!

### Reliable Data Tranfer Protocol
🔹 simple
- 한번에 패킷 하나씩만 보냄
- 하나씩 보내고 잘 받았는지 확인한 후 다음 패킷 보내기

🔹 RDTv1.0
> 가정 : underlying channel이 모두 reliable 하다면 (error도 발생하지 않고, 유실도 발생하지 않는다면) 

- 따로 할 일이 없다. 패킷을 만들어서 그냥 보내면 된다
- 하지만 굉장히 비현실적인 상황

🔹 RDTv2.0
> 가정 : underlying channel이 패킷 error가 발생 가능한 채널이다. 

▶ Error Detection, Feedback, Retransmission

- **Error detection**
  - 보내는 패킷에 **checksum**이라는 부가적인 정보를 헤더에 담아서 보냄
- **Feedback**
	패킷을 받을 때마다 피드백을 주어야 함
  - Acknoledgements (ACKs) : 잘 받았다
  - Negative acknoledgements (NAKs) : 에러가 있어서 잘 못 받았다
- **Retransmission**
  - receiver가 NAK을 보내면 sender가 패킷 재전송

#### What happens when ACK or NAK has errors?
- 현재 패킷을 재전송함
- receiver 입장에서 새로운 패킷인지, 중복된 패킷인지 구별할 필요가 있음

#### Handling Duplicate Packets
중복된 패킷 구별
- 패킷에 번호를 붙임 : sequence number
- sequence number는 헤더 부분에 들어감
- sequence number 필드를 최소화하는 게 좋다.
한개씩 보내는 상황에서는 sequence number 두 개면 충분함


🔹 RDTv2.1
> 가정 : underlying channel이 패킷 error가 발생 가능한 채널이다. 

▶ Error Detection, Feedback, Retransmission, Sequence #

Sender 
- 패킷에 sequence # 추가
- 받은 ACK/NAK에 에러가 있는지 체크
- NAK이나 에러가 있는 피드백인 경우 Retransmit

Receiver
- 중복된 패킷인지 체크
- 받은 패킷에 에러가 있으면 NAK 전송, 에러가 없으면 ACK 전송

🔹 RDTv2.2 : a NAK-free protocol
> NAK를 없앤 프로토콜

- 원리는 RDTv2.1과 동일
- ACKs 만 사용함
- NAK 대신에, receiver는 ACK에 가장 마지막으로 제대로 받은 sequence 번호를 보냄

🔹 RDTv3.0
> 가정 : underlying channel이 패킷 error와 loss가 발생 가능한 채널이다. 

- 가장 현실적인 가정
- reliable transfer 항상 보장

Timer
- 패킷 유실을 위해 필요한 mechanism
- Timer를 어떻게 설정하냐가 중요한 이슈
- 길게 하면 → 네트워크 오버헤드는 적어짐, loss가 발생했을 때 반응이 늦음
- 짧게 하면 → recovery는 빠름, 네트워크 오버헤드 큼

### 정리
#### unreliable channel에서 발생하는 현상
- Packet error, packet loss

#### packet error를 위한 매커니즘
- Error detection, feedback, retransmission, sequence #

#### packet loss를 위한 매커니즘
- Timeout

RDT라는 프로토콜은 매우 단순
- 한번에 하나의 패킷밖에 못 보냄
- sender가 패킷 보내고 피드백을 받을 때까지 아무것도 안함
- 실제로 TCP는 여러개 패킷을 한번에 보내고 피드백도 한번에 받는 식으로 동작

