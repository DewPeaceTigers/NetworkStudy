### 민지 문제

1. Go-Back-N 방식과 Selective repeat 방식의 차이

   - GBN : 유실되면 Window size 전체 다 재전송
   - SR : 유실되면 유실된 것만 재전송

2. TCP 방식의 ACK는 어떤 의미인가

   - N-1번째까지 잘 받았다는 뜻. N번째를 기다린다

3. fast retransmit 이란

   - 같은 ACK가 timer 내에 여러번 오면 유실됐다고 먼저 판단하고 재전송하는 것. (timer 이전에)

4. flow control을 진행할 때 receiver 측에서 receive buffer의 공간이 없다고 보냈을 때 sender측은 어떻게 하는가
   - 데이터 없이 pkt을 보내 Sender가 피드백할 수 있도록 지속적으로 확인

### 예리 문제

1. 각 TCP/IP layer의 전송 단위가 무엇일까요?

   - Application : message
   - Transport : Segment
   - Network : Packet
   - Link : Frame
   - Physical : bit

2. TCP의 ACK #은 어떻게 결정되나요?

   - 성공적으로 받은 paket의 마지막 number+1

3. TCP의 Reliable Data Transfer의 과정을 설명하세요

   - cumulative ACKs
   - single retransmission
   - pipelined segments

4. TCP 연결을 종료할 때의 절차는 무엇인가요? (이름 적기)

   - 4-way handshake

### 정민 문제

1. TCP connection을 closing 할때 time wait이 있는 이유

   - 상대방의 ACK loss되면 무한히 기다리게 된다.
   - 보낸 데이터가 다 도착하지 않았을 수도 있다.

2. Go-Back-N, Selective repeat에서 ACK(n)이 의미하는 것

   - GBN : n번까지 잘 받았습니다.
   - SR : n번을 잘 받았습니다.

3. TCP에서 패킷 유실을 탐지하는 조건 두가지

   - time out
   - 3 duplicate ACKs

4. TCP Series 2 Reno의 Multiplicative decrease 특징

   - 네트워크상 패킷 유실은 다른 관점이라 각각 맞춰서 대응함.
