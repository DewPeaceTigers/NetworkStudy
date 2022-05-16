# 네트워크 계층
packet을 어떻게 보낼 것인지 고려한다. 라우터를 통해 배송되기 때문에 라우터에도 network 곛ㅇ이 있다.

## 라우터
packet이 들어오면 라우터는 헤더에 적힌 목적지를 확인 후 forwarding table에 적힌 링크를 확인 후 전송을 한다. 이때, 목적지와 link가 1:1로 매핑이 되어있으면 테이블의 크기가 너무 크기 때문에 목적지 주소의 범위로 link를 구분한다. 
- forwarding : 들어온 packet의 목적지 주소와 forwarding 엔트리를 매칭시켜서 해당 엔트리의 링크로 전송을 시킨다. 
> Longest Prefix Match Forwarding
forwarding 과정에서 여러개가 매칭이 되면 prefix가 더 긴 것과 매칭시켜 보내준다.

- routing : forwarding table을 사람이 만들기엔 방대한 양이기 때문에 라우팅 알고리즘으로 테이블을 만든다

## IP datagram format
- version : IP 프로토콜의 버전
- header length : 헤더의 길이
- type of service : 데이터의 타입
- length : 전체 datagram의 길이
- 16-bit identifer, flgs, fragment offset
- time to live(TTL) : 라우터를 거칠 때마다 -1을 해주며 0이 되는 순간 패킷은 버려진다. 네트워크 상에서 라우팅 테이블이나 forwarding이 잘못되었을 때 패킷이 무한 루프 도는 것을 막기 위해서 필요하다
- upper layer : transport 계층이 TCP인지 UDP인지 적혀있다
- header checksum : 에러 파악을 위한 필드
- 32 bit source IP address : 전송한 사람의 IP 주소
- 32 bit destination IP address : 목적지의 IP 주소
> TCP와 IP 헤더가 각각 20 byte 이므로 헤더만 40byte를 차지한다. 기본적인 애플리케이션 message+40byte가 전송된다.

## IP Address(IPv4)
- 32 bit 주소 체계이며 2^32 개의 IP 주소가 존재한다.
- host에 들어있는 network 인터페이스 자체를 지칭한다. 
> 컴퓨터에 NIC 카드가 여러개 있다면 여러개의 IP 주소를 갖는다. (ex. 라우터)

### IP 주소 배정 방법
IP 주소를 막무가내로 배정을 하면 라우터 안에 forwarding table이 너무 커진다. 이를 막기 위해 **같은 네트워크 호스트는 같은 네트워크 ID**를 배정한다. 이렇게 되면 forwarding table을 범위로 묶어서 link를 연결할 수 있다. 32bit 중 일부를 network ID(prefix, subnet ID)로 사용하고 나머지 부분을 host ID로 사용한다. 
> 12.34.158.0/24
앞에서부터 24bit는 네트워크 ID를 의미한다.

### IP 주소와 서브넷 마스크
어디까지가 prefix(networt ID)인지를 컴퓨터에게 쉽게 알려주기 위해 비트맵으로 구분한다.

### Classful Addressing vs CIDR(Classless Inter-Domain Routing)
- classful addressing
  prefix를 통해 class를 구분한다.
  - class A : network ID로는 8bit를 사용하고 나머지 24bit는 host ID로 사용한다. 2^24개의 호스트가 존재할 수 있으며 128개기관만 class A에 속할 수 있다. 이 경우 2^24개의 IP를 다 사용하지 않기 때문에 낭비가 발생한다.
  - class B : network ID로 16bit를 사용한다. 2^24개의 호스트들이 존재할 수 있다.
  - class C : network ID로 24bit를 사용하기 때문에 다양한 기관에서 사용할 수 있다. 하지만 2^8개의 호스트만 존재할 수 있다.
- CIDR
클래스가 없기 때문에 네트워크 크기에 맞게 prefix를 조절할 수 있다.

### subnet
같은 prefix를 가진 장치들의 집합이며 라우터들을 거치지 않고 갈 수 있는 호스트들의 집합이다. 

## NAT
요즘에는 한사람이 스마트폰, 태블릿, 노트북 등 여러개의 디바이스를 사용하기 때문에 IP주소가 부족하다. 이를 해결하기 위해 내부에서는 유일하지만 외부에서는 같은 IP를 사용할 수 있도록 하는 방법이다.
패킷이 전송될 때 외부로 나가려면 세계에서 유일한 IP주소를 사용해야하기 때문에 패킷의 source IP가 라우터의 IP 주소로 변경한다. 반대로 패킷이 들어올 경우 목적지의 IP주소를 라이터의 IP주소에서 호스트의 IP주소로 변경한다. 
>문제
>
>라우터에서는 IP packet의 헤더만 봐야하는데 source Port가 들어있는 data 부분을 변경한다. 이 과정에서 레이어 디자인이 무너진다.
>
>port 번호는 호스트 내부에서 프로세스를 찾아갈 때 사용하는데 이 포트 번호가 변경된다.

## DHCP(Dynamic Host Configuration Protocol)
동적으로 알아서 IP, mask, router, DNS를 configure한다. IP 주소 필요 요청이 들어오면 IP 주소를 대여해준 후 사용시간이 지나면 회수를 한다.

**#️⃣  Scenario**

1. C → DHCP Server : DHCP discover
    1. src : 0.0.0.0./ 68 : 아직 할당된 게 없다고
    2. broadcast를 하는 방법 ⇒ **dest : 255.255.255.255/67**
        
        이러면 67번을 열어둔 DHCP 서버만 응답한다.
        
    3. transaction ID : 654
2. S → C : DHCP offer
    1. **src : 할당 해줌**
    2. **dest : 255.255.255.255/68**
        
        broadcast하여 68만 열려있는 Client만 의미있게 받아드린다.
        
    3. transaction ID : 654
3. C → S : DHCP Request
    1. offer을 수락한다는 의미
    2. src: 0.0.0.0/68 ⇒ 아직 확정 아님
    3. dest :255.255.255.255/67
    4. **transaction ID : 이전 꺼 + 1** 즉, 655를 보낸다. OK의 의미
4. S → C : DHCP ACK
    1. req에 대한 확인차, 이 이후로 필요한 4가지 정보들이 들어온다.
    2. src : 223.1.2.5/67
    3. dest : 255.255.255.255/68
    4. transaction ID : 655

⇒ 왜 여러 단계?

offer는 여러 DHCP로 부터 올 수 있다. 하나를 골라서 req을 하게 도는 것이다.

⇒ DHCP Server는 Router에 있다.

### IP Fragmentation

Header에는 16-bit identifier | flags | fragment offset 필드가 있다.

이는 Packet이 Fragment될 때 사용하게 되는데 link마다 mtu가 달라 발생한다.

- length : 잘라진 길이 (1500이라면 실 데이터는 1480, 20은 헤더 사이즈)
- ID : Packet ID (같은 Packet은 동일하다.)
- fragFlag : 1 (내 뒤에 파편이 있음을 의미) / 0 (더이상 없음)
- offset : 기존 data에서 시작할 부분을 기록해둔다. (두번째 파편은 185) ⇒ 순서임

→ 이를 보고 목적지에서 reassmble한다.
