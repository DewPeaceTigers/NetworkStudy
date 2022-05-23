### ICMP 
- Internet Control Message Protocol
- 사용자 데이터가 아니라 네트워크 상에서 이런저런 증상을 알기 위한 컨트롤 메시지를 운반하기 위한 프로토콜
- 네트워크에서 일어나는 특정 이벤트에 대해서 소스한테 리포트해 줄 필요가 있음 

### IPv6
- IPv4에 비해 헤더 부분이 단순함
- address space가 128 bit 임

### IPv4 IPv6 과도기 때
- tunneling 과정 필요
- 두 가지 프로토콜을 동시에 이해해서 변환을 시켜줌
- 새로운 버전의 패킷을 과거의 형태 패킷에 맞춰줄 필요가 있음 

## 라우팅 알고리즘
forwarding table은 어떻게 만들까?

### Graph abstraction
라우터 사이의 네트워크를 그래프로 개념화 시킴 
- 노드 : 라우터
- 엣지 : 링크
- 링크에 존재하는 값: 라우터 상의 실제 거리, 트래픽 양

➡️ 목적 : 목적지까지 최소 cost의 경로를 찾는 것

### 최단 경로를 찾는 방법
1. 네트워크 상황을 다 아는 경우
- "link state" algorithm

2. 이웃과만 정보를 교환한 경우 (부분적인 정보만 있음)
- "distance vector" algorithm

### link state algorithm
📍 다익스트라 알고리즘 사용
- 각 노드들이 자신의 링크 정보들을 전체 네트워크에 브로드캐스트해서 알게 함.
- 현실적으로 불가능. 
- link state의 범위는 실제로 전체 네트워크가 아니라 하나의 도메인에 속한 네트워크


### Distance Vector algorithm
📍 벨만포드 알고리즘 사용
- 이웃과만 정보를 교환함 
- X에서 Y로 가는 최단 경로 : X의 이웃들 중 하나는 반드시 거쳐감 
- 소스 X에서 Y까지의 최단거리를 recursive하게 구함 
  - Dx(y) = min(C(x, v), Dv(y)) 

- v가 넘겨주는 것은 distance의 array(vector)
  - 바로 념겨주는 정보가 distance의 array

cf) link state algorithm
- 단순히 모든 각각 노드에서 자신이 연결된 링크 정보를 넘겨줌

#### Distance Vector Algorithm 동작과정 

- 자신의 distance vector를 연결된 이웃들한테 전달 
- 이웃들은 받으면 또 계산해보고 업데이트되면 전달. 과정 반복 

- 연결된 이웃들한테 자기 자신을 distance vector로 전달하는 조건
  - distance vector 하나라도 업데이트가 되면 전달
  - 자신과 직접적으로 연결된 링크의 host가 변경된 경우


링크 cost가 바뀌면?
- 링크와 이웃한 distance vector를 다시 계산해야 함

안좋게 바뀌는 경우
- count-to-infinity 현상 발생 
- 전체 큰 그림을 가지지 못한 채 이웃에서 넘어오는 부분적인 정보만 가지고 계산을 하다보니까 상대방이 보내는 distance 값 자체가 자기 자신에 의존하는 값인 경우도 생김

### link state & distance vector
- 하나의 네트워크에 국한되어서 그 내부에서 라우팅이 이루어질 때 사용하는 알고리즘

### link state
- 직관적 
- 전체 큰 그림을 가지고(그래프를 가지고) 있기 때문에 다익스트라를 수행하는 것과 동일 
- 각 라우터가 자기 자신과 이웃한 link state 정보들을 전체 네트워크에 broadcast해서 그래프를 가지고 시작

### distance vector
- 최소 경로에 대해 구하는 식 자체를 분산적으로 구현
 

> 최소 경로를 구하는 결과물 자체는 같지만 구하는 과정에서 차이가 남

### Distance vector: link cost changes
distance vector의 분산 처리 과정 때문에 생기는 특수한 현상

안정화 된 이후에
- link cost가 줄어드는 경우
  - 변화에 대해서 새로운 distance vector를 구한 뒤에 업데이트를 하고 과정 자체가 바로 다음 라운드에 끝남 
  - 빠른 속도로 다시 안정화 됨

- link cost가 높아지는 경우
  - 큰 값으로 수렴할 때까지 핑퐁하면서 쭉 진행됨 
  - count-to-infinity 현상 
  - 갔다가 다시 돌아오는 reverse path를 막아야 함
    ➡️ 가장 직관적인 방법
    poison reverse : distance 값을 넘겨줄 때 distance 값에 결정적인 역할을 하는 이웃에 대해서만 무한대로 바꿔서 넘겨줌

### routing in the Internet
- RIP : distance vector algorithm을 구현한 프로토콜
- OSPF : link state algorithm을 구현한 프로토콜 
- BGP : inter-AS 라우팅 프로토콜 

### Intra-AS 알고리즘
AS(Autonomous System) 내부에서 동작하는 라우팅  
- 목적 : 최소 cost (최단 경로)
ex) link state algorithm, distance vector algorithm

### Inter-AS 알고리즘
AS들 사이에 동작하는 라우팅 알고리즘
- 목적이 불분명함, 최단 경로가 목적이 아님

### AS Numbers
모든 AS는 각자 자신의 고유한 넘버를 가지게 됨
- 1번 : BBN

### AS들 간의 특수한 관계
- AS가 6만개 넘게 존재
- AS를 운영하려면 하드웨어 장비들, 인력들, 소프트웨어, 운영비 필요..

- Customers and Providers
    - 갑: 원하는 것이 없음
    - 을: 
- "Peering" Relationship : 둘이 비슷. 


### BGP 
- Border Gateway Protocol
- AS들의 경계에 있는 라우터들 사이에 어떻게 라우팅할까 
- Police Based : AS들 간의 정책에 좌우됨 
- 돈을 제일 많이 벌 수 있는 길을 선택, 제일 경제적인 경로 선택


### ASPATH Attribute
AS 6341이 자신의 prefix를 다른 AS들한테 광고하는 상황

- AS Path 필드에 자기 자신을 추가

