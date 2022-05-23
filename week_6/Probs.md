## 정민 문제
1. link state 알고리즘과 distance vector 알고리즘이 사용하는 최단경로 알고리즘
    - link state: 다익스트라
    - distance vector : 벨만포드 

2. RIP, OSPF, BGP 이란 무엇인가
    - RIP : Intra-AS, link state 알고리즘 구현한 프로토콜
    - OSPF : distance vector 알고리즘 구현한 프로토콜
    - BGP : Inter-AS 라우팅 알고리즘

3. count-to-infinity 현상 발생하는 경우는? + 해결 방법
    - link cost가 값이 커졌을 때 (안 좋은 방향) 발생
    - 해결방법: poisoned reverse 

4. Intra-AS 와 Inter-AS 의 목적 
    - Intra-AS : 최단 경로를 찾는 것
    - Inter-AS : 최단 경로는 중요 X, 정책을 지키는 방향, 

## 민지 문제
1. forwarding table은 어떻게 만드는가
    - 라우팅 알고리즘을 사용한다.

2.  link state 알고리즘과 distance vector 알고리즘이 사용하는 최단경로 알고리즘
    - link state: 다익스트라
    - distance vector : 벨만포드 

## 예리 문제
1. Distance Vector 알고리즘에서 최단 경로 탐색시 생기는 문제점과 해결 방법은?
    - 문제점: count-to-infinity  
            link cost가 값이 커졌을 때 (안 좋은 방향) 발생
    - 해결방법: poisoned reverse 

2. BGP는 Inter ASs의 경로를 무슨 기준으로 정하는가?
    - 경제적인 경로, 돈을 많이 벌 수 있는 경로