# 무선네트워크
Link Layer를 이야기할 때 '첫 홉인 Gateway 라우터까지 어떻게 갈 것인가'에 대해서 이야기함

Network Layer를 이야기할 때에는 개념적인 하나의 전용 링크가 있어서 패킷을 전송하면 게이트웨이 라우터에 도착한다고 이해하였다. 

Link layer를 공부하면서 알게 된 사실
- 개념적인 하나의 전용 링크가 사실은 자신 주변의 host들과 공유를 하는 하나의 broadcast medium 이다. 
- 내가 이야기하면 다른 사람에게 들리고 다른 사람이 이야기하면 나에게 들리기 때문에 충돌이 발생할 수 있다. 
- 그러면 medium에 어떻게 접근하는지에 대한 control이 중요하고 이를 위해서 **MAC(Medium Access Control) 프로토콜**이 필요하다.
    - 유선 이더넷 (케이블): CSMA/CD 
    - 점점 기술이 발전하면서 무선인 상황이 존재한다!

### Wireless and Mobile Networks
- 결국은 Link layer의 연속이다.

> 개념적으로 비슷
- 유선 이더넷 사용
    - '링크' 라는 하나의 broadcast를 공유해서 생긴 현상
- 무선 링크
    - '공기' 라는 하나의 공유된 medium을 통해서 전달하는 상황이기 때문에 충돌이 발생한다.

## Wireless
- 선이 없다.

### Wireless network 기본 개념
무선 네트워크
- **첫 홉만 무선**이고 나머지는 유선이다.

![](https://velog.velcdn.com/images/ryujm/post/cddc14d8-3a2e-4337-bf6b-8875d0189e14/image.png)

x축 : 전송반경  
y축 : 데이터 속도

### Wireless network taxonomy
- 흔히 보는 90% 이상의 무선 네트워크는 infrastructure가 있으면서 single hop인 경우이다.
- WiFi, cellular

### 무선 링크의 특성
- 거리에 따라서 signal 크기 확 줄어든다.
- 보호받지 못하고 외부로부터 간섭을 많이 받는다.

#### 생기는 문제점
Hidden terminal problem
- A에서 보낸 내용이 C에게 안 들린다.
- C에서 보낸 내용이 A에게 안 들린다.

Collision detection이 불가능함
- 자신이 이야기를 하기 시작하면 반경 내에 있다고 하더라도 주변에서 하는 이야기를 듣지 못함
- 자신이 무언가 이야기하기 시작하면 자신의 소리는 크게, 주변에서 나는 소리는 엄청 작게 들린다.
    - 전송 거리에 따라서 신호세기가 엄청나게 줄어들기 때문

### IEEE 802.11 Wireless LAN
WiFi 
- Wireless Fidelity의 약자
- 무선이지만 유선링크에 가까울정도로 충실하겠다.

나온 버전
```
802.11b
802.11a
802.11g
802.11n (가장 최근)
```
- Data rate가 점점 개선되고 있음

### 802.11 LAN architecture

![](https://velog.velcdn.com/images/ryujm/post/3f5efd5d-cf3c-4f61-81e0-b73265f250f7/image.png)


- Access Point가 존재하고 AP는 유선 이더넷 케이블이 꽂혀 있어 그 뒤에 스위치가 존재한다.
- AP(Access Point)가 Basic Service Set(BSS)를 구성한다

### 802.11: passive/active scanning
- beacon에 자기 자신의 AP 정보를 담아서 주기적으로 자신의 정보를 broadcast 함
- point들이 그 정보를 보고 판단한다.
- beacon 정보에는 각 AP의 이름과 MAC address 가 담겨있다.

### 801.11: multiple access
Wifi는 어떤 MAC 프로토콜을 사용하는지, 어떻게 동작하는지

충돌 발생은 하는데 충돌 감지를 하지 못함, 내 스스로 판단이 불가능하기 때문에 제대로 갔는지 아닌지 상대방이 알려줘야 한다. 

➡️ 따라서 <span style ="color: red">ACK</span>가 필요하다.
여기서 말하는 ACK는 Link layer의 ACK 이다.
- TCP에서의 ACK와는 완전 다른 개념!!!
- TCP : end-to-end feedback

cf) 유선 이더넷에서는 충돌이 나면 충돌이 안 날때까지 계속 재전송한다. 충돌 감지가 가능하므로 ACK가 필요하지 않았음

### 802.11 MAC protocol: CSMA/CA
CSMA/CA
- Carrier Sense Multiple Access with Collision Avoidance
- Wifi에서 사용하는 MAC 프로토콜의 이름

동작
- 보낼 데이터가 있으면 Carrier sense 해보고 누군가 이야기하고 있으면 보내지 않고 그 이야기를 끝낼 때까지 기다린다. 기다렸다가 조용해지면 random-backoff를 사용해서 랜덤한 시간 만큼 기다렸다가 보낸다. 
- DIFS(고정된 시간)만큼 carrier sense를 했는데 조용했다면 데이터를 보낸다.으로 정해져 있음. 
- receiver는 SIFS(정해진 시간)만큼 기다린 후 데이터를 제대로 받았으면 ACK를 보낸다.


유선 이더넷에서는 충돌을 감지하면 바로 멈춘다. 반면 무선에서는 중간에 멈추는 개념이 없다. 무선에서는 충돌에 대한 피해가 더 크기 때문에 충돌을 피하기 위해 노력해야 한다.

### Collision Avoidance : RTS, CTS

![](https://velog.velcdn.com/images/ryujm/post/32222ead-e964-434a-9734-7d013090af7a/image.png)

- RTS: Ready to Send
- CTS: Clear to send

carrier sense 해보고 조용하면 바로 데이터를 보내는 것이 아니라 작은 control frame인 RTS를 먼저 보내본다.

- 충돌은 피할 수 없는 현상인데 데이터에서 충돌이 나는 것보다는 작은 사이즈의 control frame인 RTS, CTS에서 충돌이 나는 것이 피해가 덜하다.

사람이 적으면 굉장히 효율적인데 사람이 많으면 계속 충돌이 발생할 수 있다.

### 802.11 frame: addressing
Wifi에서 사용하는 프레임

![](https://velog.velcdn.com/images/ryujm/post/cf22864a-de09-47e4-b579-d52521adbcd5/image.png)

Address space가 4개다!

- Address 1
    - 무선 WiFi 데이터프레임을 받는 인터페이스의 MAC address

- Address 2
    - 무선 프레임을 전송하는 인터페이스의 MAC address

- Address 3
    - 데이터 부분에 해당하는 것을 처리하게 될 라우터의 MAC address

- Address 4
    - 잘 안 쓰임
    
**AP**를 주목해야 함!
- 한쪽은 WIFI(무선), 한쪽은 이더넷(유선)
- 라우터 입장에서 H1이 있는 것은 알지만 AP는 보이지 않음. 

AP Mac Address
- AP들이 beacon 메시지들을 주기적으로 broadcast하여 보내줌

Router의 MAC Address
- 자신의 MAC Address는 아는데 IP 주소를 모른다
- DHCP 프로토콜을 통해서 자신의 IP 주소, Subnet mask, Gateway Router의 IP, Local 네임서버의 IP를 알아온다.
- 라우터의 MAC 주소를 알기 위해서 ARP 테이블을 참조한다.

### 802.11 : mobility within same subnet

TCP connection
- 자신 IP, Port, 상대방 IP, Port가 변하지 않는 이상 계속 유지됨
- 같은 Subnet 안에서 IP 주소가 그대로 유지될 수 있음
- AP의 사이에서만 이동이 있을 경우에는 TCP Connection이 유지된다.
- 트래픽이 새로운 방향으로 흘러가기 위해서는 스위치 안에 들어있는 스위치 테이블만 바꾸면 된다.  
    - self-learning 사용 
ex) 유투브에서 날라오는 IP 패킷
- source : Youtube
- dest: H1

switch table 에서 H1에 해당하는 entry를 어떻게 바꿀 것인가??
- self-learning


### 802.11: advanced capabilities

무선 채널의 퀄리티를 좌우하는 요인
- access point와 mobile host 사이의 거리
- 가까우면 가까울수록 무선 채널 성능이 좋다

SNR
- noise 대비 signal 비율
- 디지털 데이터를 아날로그에 실어서 보낼 때 규칙이 필요함. 
- access point과 mobile host가 가까이 있으면 SNR이 높다.(채널 퀄리티가 좋다)

BER
- 비트 당 에러가 발생할 확률

Rate Adaptation
- 채널 환경에 따라서 data rate를 조절한다.

power management
- Wifi 어댑터가 무선통신을 하는데 computation 할 때 사용되는 전력보다 무선 통신을 사용하여 패킷을 주고받을 때 사용되는 전력이 10배 이상 훨씬 크다. 되도록이면 transmission 하는 회로 부분을 꺼두는 것이 좋다.


### Cellular Internet access
- 전체 관할 지역을 Cell이라는 단위로 나누어서 Cell 하나에 기지국을 하나 심어놓고 Cell에 속하는 Host들을 담당한다.

#### Cellular 네트워크에서 사용하는 MAC 프로토콜

![](https://velog.velcdn.com/images/ryujm/post/9e31f1cb-ec66-4616-a00a-4cf75dae62fb/image.png)

- FDMA / TDMA
- CDMA
    - 3G로 넘어오면서 CDMA 사용
    - 수학적인 연산을 대입해 자신에게 해당하는 데이터를 증폭시켜 받아들임

![](https://velog.velcdn.com/images/ryujm/post/11d91e9c-69a8-46d1-922b-7cd0aaef11b6/image.png)

- Data rate로 세대를 나눔

## Mobility
- 네트워크 관점에서 이동이라면, AP를 바꾸는 차원의 이동이 되거나 네트워크를 변경해야 한다.
- connectivity가 있는 상황에서 네트워크를 넘나드는 이동이 있어야 한다.

ex1) 노트북의 경우 wireless는 맞지만 mobility는 아니다.

ex2) 스마트폰의 경우 mobility의 예이다.

### Mobility
no 모빌리티
- 앉은 자리에서 인터넷하고 끝!

중간 모빌리티
- 네트워크를 넘나드는 이동을 했지만 가서 새로운 네트워크를 사용

high 모빌리티
- TCP connection을 유지하는 상황에서 다른 네트워크로 이동하는 상황

> 문제점
>- 어떻게 연결을 할 것인가
>- 어떻게 연결을 계속 유지할 것인가

### Mobility : vocabulary
permanent address
- 모바일 호스트는 permanent address를 가짐

home network
- 모바일 호스트가 존재하는 네트워크

home agent
- home network에 존재하는 모든 호스트들을 관리



> 어떻게 연결을 할 것인가

### Mobility via indirect routing
- 외부 노드가 접근할 때는 permanent address 정보만을 사용하고,
permanent address를 보고 home agent가 알아서 포워딩 해준다.

❗️ 현실에는 없는 것.. 상상


- 장점
    - permanent address 정보만 알면 목적지에 갈 수 있음

- 단점
    - 멀리 돌아가서 오래 걸릴 수 있음

### Mobility via direct routing
- 외부 클라이언트가 모바일 호스트에 접근하기 위해서 permanent address를 사용해서 패킷을 보내는데 home agent가 바로 그 패킷을 포워딩 해주는 것이 아니고 답(새로운 주소)을 돌려준다.
- home agent가 알려준 새로운 주소로 직접 연결

> 어떻게 연결을 계속 유지할 것인가

- 새로운 네트워크로 이동하면 거기에 foreign agent가 있음. foreign agent를 통해서 home agent 한테 연락하면 새로운 연결이 생긴다.


---
## 멀티미디어네트워크

## Multimedia: audio
오디오(음성, 음악)
- 공기에서 wave를 타고 가는 아날로그 신호
- 아날로그 신호를 디지털 데이터로 바꾸는 과정이 필요 ➡️ **샘플링**

샘플링
- 항상 오차가 발생함. 
- 오차를 줄이는 방법
    - 아날로그 신호를 디지털 데이터로 바꿀 때 표현하는 비트 수를 늘린다.  
    - 샘플링 주기를 짧게 한다.
- example rates
    - CD : 1.411 Mbps
    - MP3 : 96, 128, 160 kbps
    - Internet telephony : 5.3 kbps and up

```
8,000 samples/sec, 256 quantized values: 
> 64,000 bps
```

## Multimedia : video
비디오 : 이미지의 연속  
각 이미지를 프레임이라고 표현

프레임을 디지털로 변환시킬 때
- 각 픽셀에 어떤 색깔값이 나타나는가 저장
- 이웃한 픽셀에는 비슷한 색깔이 저장되기 때문에 중복되는 것을 그대로 적지 않고 압축시킨다.
- coding rate가 높을수록 화질 좋음

## Multimedia networking: 3 application types
- streaming, stored audio, video
    - 멀티미디어 데이터는 이미 서버에 저장이 되어 있고 클라이언트에게 스트리밍 해주는 서비스
    - streaming 
    - stored (at server)
    - ex) Youtube, Netflix 

- conversational void/video over IP
    - ex) Skype

- streaming live audio, video
    - 서버에 저장된 것이 아니라 실제 일어나고 있는 영상을 실시간으로 받음
    - ex) 야구 중계

## Streaming stored video

클라이언트 측에서 다음 프레임을 재생해야 하는데 network delay가 일정하지 않아 제대로 안 들어와있을 수 있음

jitter
- network delay가 일정하지 않음

<img src=""/>
클라이언트에서 바로 재생하지 않고 일정시간의 시간이 지난 후에 play 한다. > 버퍼링

### Client-side buffering, playout


### Streaming multimedia : DASH
DASH : Dynamic, Adaptive Streaming over HTTP
- HTTP를 사용해서 TCP를 통해 스트리밍을 보낸다.
- 동적으로 네트워크 환경에 알맞게 무언가 해준다.

> server

엄청나게 많은 사용자가 같은 데이터를 요청할 때 해결할 수 있는 방법

1. 멀티캐스트 (Multicast)
   - 실제로 구현하기는 어렵다..

2. CDN (Content Distribution Network)
   - 한 곳에 집중되어 있던 콘텐츠의 복사본을 전세계 곳곳에 저장한다. 
   - 나로부터 가장 가까운 곳에 있는 스토리지에서 가져오는 방식

사용자들한테 가장 홉 수가 가까운 곳에 위치시키기 위해서 access network 근처에다가 CDN 업체들이 서버를 위치시킴

---
## Network Security
요구조건

- confidentiality
    - 비밀성, 기밀성
    - 주고 받는 메시지는 둘 만 알아볼 수 있고 다른 사람은 알아볼 수 없음  
    - 암호화 기법을 사용하면 된다

- authentication
    - 인증
    - 말하고 있는 사람이 진짜 그 사람인지 확인

- message integrity
    - 보낸 메시지가 변형되지 않고 받는 사람에게 전달되어야 한다.

- access and availability
    - 서비스를 제공하는 사람은 24시간 내내 사용자들에게 서비스를 제공할 수 있어야 한다.

### Friends and enemies: Alice, Bob, Trudy
wireshark라는 툴을 통해 인터넷 활동 모니터링 가능

TOR
- The Onion Router의 약자
- 익명성 애플리케이션 툴
- 이것을 사용하면 자신이 어떤 서버에 접근하는지 아무도 모르게 해준다.

패킷
1. TCP connection 맺어야 함
2. HTTP Request

그냥 드랍시켜버리면 네트워크 오류라고 생각. 사용자에게 주고자 하는 에러메시지를 전달할 수 없음

TCP connection은 맺게 한 다음, HTTP request할 때 host 필드를 보고 필더링 하고자 하는 후보에 있다면 response를 만든다. response에 warning.html을 담아서 보낸다.

### cryptography
![](https://velog.velcdn.com/images/ryujm/post/30be3fbb-4cf1-4d40-bf93-d52086fec9e4/image.png)


- plain text를 cyper text로 바꿔주는 과정을 암호화(encryption)라고 한다. 암호화하는 과정에 필요한 요소는 key 다! 
- 보내고자 할 때 plain text를 key로 한번 적용시켜주면 cyper text가 된다.
- cyper text를 Bob이 가지고 있는 key로 적용시켜주면 decryption이 되어서 plain text가 나온다.

### 암호화 하는 기법 두 가지
1. Symmetric key cryptography
2. Public Key cryptography

### Symmetric key cryptography
- 암호화하고 해독하는 key가 같다.
- 과정이 대칭적이다.
- 연산이 빠르고 효율적인 대신에 같은 키를 공유해야 한다는 문제점이 있음
- 만난 적이 없는데 키를 공유한다는 것은 어려운 문제다.

### Public key cryptography
- 모든 사람이 각자 두 가지 종류의 key를 가진다.
- 모두에게 공개하는 Public key, 자기자신만 알고있는 Private key
- 메시지를 보낼 때 상대방의 Public key로 암호화해서 보낸다.
- 암호화된 메시지는 상대방의 Private key를 통해서만 해독 가능하다.
> Diffie-Hellman76, RSA78

### RSA: another important property
- public key 알고리즘
- 어떤 키를 먼저 적용시키든 간에 순서에 상관없이 동일한 결과가 나온다.
- 부담스러운 연산으로 Symmetric key보다 100배, 1000배 시간이 오래걸림. 실제로 메시지 전체를 암호화할 때는 public key 방식의 암호화를 사용하지 않고 symmetric key 방식을 사용한다.

### Authentication
![](https://velog.velcdn.com/images/ryujm/post/787cd3d3-aed9-4f48-a9bb-9f0991a0bdf1/image.png)


- 상대방에게 랜덤 메시지를 전송하고 상대방은 그 메시지를 암호화하여 다시 전송한다. 암호화된 메시지를 해독하여 원래 메시지가 나오는지 확인한다. 
- 둘 사이의 key가 있어야 한다!

### Digital signatures
- 보내고자 하는 메시지를 private key를 사용하여 암호화한다. -> '사인' 
- 상대방은 메시지를 보낸 사람의 public key를 사용하여 해독한다.

인증서
- 사용자의 Public key가 저장되어 있다.

### SSL and TCP/IP
- Secure Socket Layer
- TLS(Transport Layer Security)이라고도 함!

![](https://velog.velcdn.com/images/ryujm/post/7bd6ac19-95f5-4e97-8d36-b42841d272c1/image.png)


HTTP 메시지를 SSL 라이브러리를 통해서 내려보내면 HTTP<span style="color:red">S</span>이다
- HTTPS = HTTP + SSL

### SSL : simple secure channel
- handshake
    ![](https://velog.velcdn.com/images/ryujm/post/7da3bb24-7fe7-4dcd-b110-004eb6f79921/image.png)


    - SSL은 TCP를 기반으로 하므로 TCP connection이 있어야 함
    - TCP connection 이후에 이루어지는 과정
    1. Client는 Server에게 https로 요청을 보냄
    2. Server는 공인 인증기관에서 발급한 private key로  암호화된 server의 인증서를 보냄. 인증서의 구성은 자신이 누구인지와 server의 public key가 담겨져 있다.
    
    3. Client는 공인 인증기관의 public key로 복호화하여 server의 public key를 얻음. Client는 4개의 키로 구성된 master secret key를 생성하고, server의 public key로 암호화하여 보낸다.

    4. Server는 자신의 private key로 메시지를 복호화하고, master secret으로부터 대칭키와 MAC키를 생성. 생성된 key들로 암호화 통신을 한다.

    - MS : master secret
    - EMS : encrypted master secret

Master secret으로부터 얻는 4개의 key
- Kc : client가 server에게 데이터를 보낼 때 암호화하는 대칭키

- Mc : client가 server에게 데이터를 보낼 때 MAC을 만들기 위해 필요한 키

- Ks : server가 client에게 데이터를 보낼 때 암호화하는 대칭키

- Ms : server가 client에게 데이터를 보낼 때 MAC을 만들기 위해 필요한 키


## Firewall
- 하나의 네트워크의 gateway 자리에 있으면서 외부로 나가고 들어오는 패킷을 관리함
- 모니터링 디바이스
- 네트워크 운영자가 패킷 관리 정책을 정함