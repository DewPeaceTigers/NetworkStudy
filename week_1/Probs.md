# 예리 문제
1. 네트워크 코어가 데이터를 전달하는 방식 두가지
    - circuit switching
    - packet switching

2. HTTP가 하는 역할 두가지
    - 
    - 

3. Transport 층에서 하는 일 두가지
    - Multiplexing / Demultiplexing
    - Error checking

4. Reliable Data Transfer 시 packet errors를 체킹하는 것 4가지
    - Error Detection, Feedback, Retransmission, Sequence Number

---
# 민지 문제
1. TCP와 UDP의 차이
  TCP는 sender와 receiver를 연결하고 reliable data transfer을 제공한다. 또, receiver의 속도에 맞춰서 전송하도록 flow control과 sender와 receiver 사이 네트워크에 맞춰서 전송하도록 congestion control을 제공하지만 UDP는 이 4가지를 모두 제공하지 않는다. 

2. packet 지연의 4가지 요소
  - nodal processiong : 패킷 검사, 목적지 확인 하는 동안 발생하는 지연
  - queueing : 대기하는 동안 발생하는 지연
  - Transmission delay : 첫번째 비트가 나간 시간부터 마지막 비트가 나갈 때까지 걸리는 시간
  - Propagation delay : 마지막 비트가 link에 올라온 후부터 다음 라우터까지 도착하는데 걸리는 시간

3. 서버의 특징 두가지(IP와 동작 시간)
  서버는 항상 동작해야하면 IP가 고정되어 있다.

4. Transport 계층에서 하는 일 두가지
  - mutiplexing/demutliplexing
  - 에러 체크

5. UDP, TCP에서 에러를 확인하는 방법
  - 세그먼트의 헤더 필드 중 checksum을 이용해 에러가 발생했는지 확인한다

6. Reliable Data Transfer 시 패킷 에러가 발생한다 했을 때 이를 해결하는 방법
  - Error detection, Feedback, Retransmission, Sequence number

7. Reliable Data Transfer 시 패킷 에러와 유실이 모두 발생한다 했을 때 이를 해결하는 방법
  - 패킷 에러 발생한 경우 필요한 4가지 + Timer

---
# 정민 문제

1. 네트워크를 통해 데이터를 전달하는 방식 2가지
    1. circuit switching
        
        • 출발지에서 목적지까지 가는 길을 미리 예약해놓고 특정 사용자만이 사용하게 만들어놓음
        
    2. packet switching
        
        • 유저가 보내는 패킷을 패킷 단위로 받아서 그때 그때 올바른 방향으로 포워딩 해줌
        
        • 인터넷에서는 이 방식 사용
        
2. 각 네트워크 계층의 대표적인 프로토콜은?
    
    (1) APP : HTTP
    
    (2) Transport : TCP, UDP
    
    (3) Network : IP
    
    (4) Link : WIFI / LTE
    
3. **소켓의 주소**를 알기 위해서 필요한 정보
    - IP Address : 어떤 컴퓨터인지
    - Port number : 어떤 프로세스인지

4. HTTP의 특징 2가지
    1. TCP 사용
        
        • 클라이언트가 웹에 접속하면 TCP 연결을 생성함
        
    2. stateless (상태가 없다)
        
        • 서버는 클라이언트 상태에 대한 정보를 기억하지 않음

5. Multiplexing이란?
    
    여러 어플리케이션의 socket들로부터 들어오는 데이터를 수집하여, 패킷으로 만들어 하위 레이어로 전송하는 것
    
6. 패킷 에러, 패킷 유실을 극복하기 위한 매커니즘
    - 패킷 에러 : Error Detection, Feedback, Retransmission, Sequence #
    - 패킷 유실 : Timout

7. Reliable data transfer에서 “Reliable”의 의미는?
    - 데이터가 하나도 유실되지 않고 그대로 전송됨

8. Demultiplexing 할 때 UDP, TCP 각각 필요한 정보
    - UDP (2가지) : dest IP & dest Port
    - TCP (4가지) : src IP & src Port & dest IP & dest Port