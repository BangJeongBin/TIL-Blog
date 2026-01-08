---
title: 패킷의 구조
description: 패킷의 구조와 캡슐화에 대해서 알아보자
author: bin
date: 2026-01-05 09:00:00 +0800
categories: [TIL, Network]
tags: [Network, OSI7, Packet, IP, TCP, HTTP, Header. Payload]
pin: true
math: true
mermaid: true
image:
 path: https://bangjeongbin.github.io/TIL-Blog/assets/img/posts/common/til-logo.png
 alt: Today I Learnd
---

![encapsulation image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdna%2FX0Bld%2FbtsgFuElDKp%2FAAAAAAAAAAAAAAAAAAAAANpLJI9lDdDLSRJ5vtiiwITAvZSn_uMgx2p6KIejRziE%2Fimg.png%3Fcredential%3DyqXZFxpELC7KVnFOS48ylbz2pIh7yKj8%26expires%3D1769871599%26allow_ip%3D%26allow_referer%3D%26signature%3DZ8%252BHjeVMfFdcfru44iiER%252BHaY%252Fo%253D)

패킷의 구조[^1]

## 패킷의 구조
---
```
[ Ethernet Frame ]
 └─ Ethernet Header
     └─ IP Packet
         ├─ IP Header
         └─ IP Payload
             └─ TCP Segment
                 ├─ TCP Header
                 └─ TCP Payload
                     └─ HTTP Message
                         ├─ HTTP Header
                         └─ HTTP Body (Payload)
```

<br>

## 캡슐화 (Encapsulation)
---
데이터를 전송하기 위해 상위 계층에서 받은 데이터에 해당 계층의 <u>헤더를 추가하는 과정</u>

### 캡슐화 과정 (OSI 7계층 기준)
---
1. **응용/표현/세션 계층**: 데이터를 생성하고, 애플리케이션 정보(HTTP 등)를 붙여 세그먼트(Segment) 생성

2. **전송 계층**: 세그먼트에 TCP/UDP 헤더(포트 정보)를 붙여 세그먼트로 만듦

3. **네트워크 계층**: 세그먼트에 IP 헤더(IP 주소)를 붙여 패킷(Packet) 생성 (라우터 통과)

4. **데이터 링크 계층**: 패킷에 MAC 헤더(MAC 주소)와 트레일러를 붙여 프레임(Frame) 생성 (스위치, 허브 통과)

5. **물리 계층(NIC)**: 프레임을 비트(0, 1)로 변환하여 물리적 매체(선)로 전송

<br>

## 역캡슐화 (Decapsulation)
---
수신된 데이터를 각 계층의 <u>헤더를 제거하며</u> 원래의 데이터로 되돌리는 과정

### 역캡슐화 과정 (OSI 7계층 기준)
---
1. **물리 계층(NIC)**: 비트를 프레임으로 복원

2. **데이터 링크 계층**: MAC 헤더/트레일러 제거 -> 패킷 추출

3. **네트워크 계층**: IP 헤더 제거 -> 세그먼트 추출 (라우터는 IP 헤더만 보고 포워딩)

4. **전송 계층**: TCP/UDP 헤더 제거 -> 데이터 추출 (포트 확인)

5. **응용/표현/세션 계층**: 헤더 제거 후 원래의 애플리케이션 데이터(사용자 화면 등)로 변환. 

<br>

![OSI Model](https://assets.bytebytego.com/diagrams/0295-osi-model.jpeg)

캡술화, 역캡슐화 과정[^2]

<br>

## 네트워크에서의 데이터 이동 과정
---
1. Host PC에서 생성한 **Ethernet Frame을 목적지를 향해 전송**한다.

2. **스위치는 Ethernet Frame을 읽고, MAC Table을 참조하여 목적지와 부합하는 라우터로 전달**한다.

3. **라우터는 Ethernet Frame을 읽을 수 없으므로, 역캡슐화하여 IP Datagram을 읽고 목적지로 가기 위한 경로에 있는 다음 라우터로 전달**한다.

4. 이 때, **라우터와 라우터 사이에서는 Data Link 계층의 WAN 프로토콜인 HDLC Frame 형태로 데이터를 전송해야하므로 HDLC 헤더를 붙여 Encapsulation한 후에 목적지 경로 Router****에 데이터 전달**한다.

5. HDLC Frame을 전달받은 **라우터는 Data Link 계층의 헤더를 읽을 수 없으므로 Decapsulation하여 Packet의 IP 헤더를 읽고 Ethernet 헤더를 Encapsulation 하여 목적지 Host PC로 데이터 전송**

<br>

![Network Diagram](https://www.gliffy.com/sites/default/files/inline-images/network-diagram-example.png)

네트워크 다이어그램[^3]

<br>

<!-- ## Related Posts
---
- 

<br> -->

## Reference
---
- [[Network 이론] 캡슐화, 캡슐화 해제](https://easyitwanner.tistory.com/391)
- [[Network / 네트워크] Encapsulation 캡슐화 & Decapsulation 역캡슐화](https://b1jou39.tistory.com/12)

[^1]: 출처 : https://easyitwanner.tistory.com/391
[^2]: 출처 : https://bytebytego.com/guides/what-is-osi-model/
[^3]: 출처 : https://www.gliffy.com/blog/how-to-create-a-network-diagram-with-gliffy
