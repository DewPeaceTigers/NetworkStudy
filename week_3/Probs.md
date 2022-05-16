## 민지 문제
1. 라우터에서 하는 일은 무엇인가

    forwarding, routing

2. NAT란
    
    IPv4가 너무 부족해서 내부에서만 유일한 IP를 사용하고 외부로 나갈때는 전체적으로 유일한 IP랑 포트로 변경해준다.

3. NAT 사용 문제

    라우터는 패킷의 헤더만 보지 않고 다른 레이어의 헤더를 건드린다. 그리고 포트 번호도 같이 변환되어 프로세스를 찾을 방법이 없다.

4. DHCP 동작 과정

    1. DHCP discover
    2. DHCP offer
    3. DHCP request
    4. DHCP ACK


## 정민 문제
1. 라우터가 하는 일 2가지

    forwarding, routing

2. DHCP 개념과 DHCP 서버가 제공해주는 정보

    동적으로 IP, mask, DNS, router 할당

3. IP 주소를 재사용하여 주소 공간 부족 문제를 해결하는 방법은?

    NAT

4. Subnet이란 무엇인가?

    1. 같은 네트워크 상에 있는 디바이스의 집합
    2. 라우터를 거치지 않고 접근할 수 있는 호스트의 집합

## 예리
1. CIDR은 무엇이고 사용하는 이유는?

    prefix가 가변적인 할당방법

    prefix가 고정적이면 낭비되는 경우가 발생하기 때문이다.

2. Longest Prefix Matching의 의미는?

    여러 주소 범위 중 prefix가 가장 구체적인 링크를 매핑하는 것이다

3. IP fragmentation이 일어나는 이유는?

    링크마다 MTU가 다르기 때문이다.

4. IP fragmentation에 의해 사용되는 Packet의 Header fields는? (설명 포함)

    16-bit identifier, flags, offset