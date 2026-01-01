---
title: "[Inflearn] \"외워서 끝내는 네트워크 핵심이론 - 기초\" Note-Taking"
description: "[Inflearn] 외워서 끝내는 네트워크 핵심이론 - 기초 공부기록"
author: bin
date: 2025-12-24 09:00:00 +0800
categories: [Review, Note-Taking]
tags: [Network, IP, TCP, OSI7, Protocol]
pin: true
math: true
mermaid: true
image:
 path: https://bangjeongbin.github.io/TIL-Blog/assets/img/posts/common/note-taking-logo.png
 alt: Note Taking
---

> 해당 포스트는 학습 목적으로 작성되었으며 <<[외워서 끝내는 네트워크 핵심이론 - 기초](https://www.inflearn.com/course/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%ED%95%B5%EC%8B%AC%EC%9D%B4%EB%A1%A0-%EA%B8%B0%EC%B4%88)>>을 참고하여 작성하였음을 알려드립니다.

<br>

## 섹션 2. Internet 기반 네트워크 입문
---
![hw-sw-archtecture](https://lh3.googleusercontent.com/d/1TsayCAMRhvHYqz8-i_DxCYDDasiK_Bl-)


### OSI 7계층 프로토콜 구조

| 계층  | 프로토콜           | 식별자     | 데이터 단위  |
| --- | -------------- | ------- | ------- |
| L2  | Ethernet (LAN) | MAC 주소  | Frame   |
| L3  | IP (WAN)       | IP 주소   | Packet  |
| L4  | TCP, UDP       | Port 번호 | Segment |
| L5  | SSL/TLS        | -       | -       |
| L7  | HTTP           | -       | Stream  |

### 식별자 정리
- **L2 - MAC 주소**: NIC(랜카드)마다 부여되는 하드웨어 물리 주소
- **L3 - IP 주소**: Host를 식별하는 논리 주소
- **L4 - Port 번호**: 
  - L2: 인터페이스 식별자
  - L3-L4: 서비스 식별자
  - L7: 프로세스 식별자

### Host의 개념
**Computer + Network = Host**

**Host의 분류:**

1. **Switch (네트워크 인프라)**
   - 네트워크 그 자체를 구성하는 Host
   - 대표: Router

2. **End-point (단말기)**
   - Switch를 이용하는 주체
   - 대표: Client, Server, Peer

### Switch의 종류
**Switching = Interface 선택 작업**

| Switch 종류 | 판단 기준 | 역할 |
|------------|----------|------|
| L2 Switch | MAC 주소 | End-point 직접 연결 (Access Switch) |
| L3 Switch | IP 주소 | 네트워크 간 라우팅 (Router) |
| L4 Switch | Port 번호 | 부하 분산 |
| L7 Switch | HTTP 프로토콜 | 애플리케이션 레벨 분산 |

<br>

## 섹션 3. L2 수준에서 외울 것들
---
### NIC (Network Interface Card)
- **별칭**: LAN 카드
- **특징**: 하드웨어 장치이며 MAC 주소(L2 식별자)를 가짐
- **L2 Access Switch**: End-point에 직접 연결되는 스위치

### 핵심 개념 정리
- **MAC 주소**: NIC 제조 시 하드웨어에 고정되는 물리 주소
- **IP 주소**: 소프트웨어적으로 할당되는 논리 주소
- **Port 번호**: 특정 서비스를 식별하는 번호
- **서브넷 마스크**: 네트워크를 구분하는 데 사용

### Broadcast
- **특징**: L2 네트워크 내 모든 호스트에게 전송
- **필수 요소**: 브로드캐스트 범위 조절
- **방법**: 서브넷 마스크를 사용하여 네트워크 분할

<br>

## 섹션 4. L3 수준에서 외울 것들
---
### IP 주소 구조
```
192.168.1.10 = 11000000.10101000.00000001.00001010
```

**주소 분할:**
- `192.168.1` → **Network ID** (네트워크 식별)
- `10` → **Host ID** (호스트 식별)

### IP Packet의 이해
- **정의**: L3 계층의 데이터 단위
- **최대 크기**: MTU (Maximum Transmission Unit) - 일반적으로 1,500 byte
- **구성**: Header + Payload
- **Encapsulation**: 
  - L2 Frame의 Payload 안에 L3 IP Packet이 포함
  - L3 Packet의 Payload 안에 L4 TCP/UDP 포함

### 계층별 데이터 단위
- **L1-L2**: Frame
- **L3 (IP)**: Packet
- **L4 (TCP)**: Segment
- **Socket**: Stream

### 네트워크 장애 유형

| 장애 유형 | 증상 | 주요 원인 | 비고 |
|---------|------|----------|------|
| **Loss Segment** | 패킷 유실 | 주로 Network 문제 | 혼잡, 장비 오류 |
| **Re-Transmission + ACK-Duplicate** | 재전송 후 중복 ACK | Network 또는 End-point | 지연, 버퍼 부족 |
| **Out Of Order** | 패킷 순서 뒤바뀜 | 거의 Network 문제 | TCP 스택에서 자동 보정 |
| **Zero Window** | 버퍼 공간 없음 | End-point 애플리케이션 | 처리 속도 불균형 |

### IPv4 Header
- **일반적인 크기**: 20 byte (옵션 없을 시)
- **주요 필드**: Version, TTL, Protocol, Source IP, Destination IP 등

### Subnet Mask
- **목적**: Network ID와 Host ID 구분
- **방법**: IP 주소와 AND 연산 수행

**CIDR 표기법 (Classless Inter-Domain Routing):**
```
192.168.0.10/24
             ↑
        서브넷 마스크 비트 수 (255.255.255.0)
```

### Loopback Address
- **주소**: `127.0.0.1`
- **용도**: 자기 자신과 통신 (IPC - Inter Process Communication)
- **장점**: IP 주소가 변경되어도 항상 동일

### TTL과 단편화

**TTL (Time To Live):**
- 패킷이 라우터를 거칠 때마다 1씩 감소
- 0이 되면 패킷 폐기 (무한 루프 방지)
- 단위: hop (라우터를 거치는 횟수)

**단편화 (Fragmentation):**
- **발생 원인**: 경로 상 MTU 크기 차이
- **조립 위치**: 주로 수신측에서 수행
- **권장**: 단편화가 발생하지 않는 것이 최선
- **VPN 주의**: IPsec 적용 시 MTU 감소 가능

### 인터넷 사용을 위한 필수 설정
1. **IP 주소**: 내 컴퓨터의 주소
2. **Subnet Mask**: 네트워크 범위 설정
3. **Gateway IP 주소**: 외부 네트워크 연결 경로
4. **DNS 주소**: 도메인 이름 해석 서버

### DHCP (Dynamic Host Configuration Protocol)
- **구성**: DHCP 서버 + DHCP 클라이언트
- **기능**: 복잡한 인터넷 설정을 자동으로 수행
- **핵심**: 사용할 IP 주소를 서버가 자동 할당
- **장점**: 수동 설정 오류 방지, 관리 편의성

### ARP (Address Resolution Protocol)
- **목적**: IP 주소로 MAC 주소를 알아냄
- **필요 상황**: Gateway의 MAC 주소를 찾아야 인터넷 연결 가능
- **동작**: 브로드캐스트로 "이 IP 가진 사람 MAC 주소 알려줘" 요청

**RARP (Reverse ARP):**
- MAC 주소로 IP 주소를 알아내는 역방향 프로토콜

### Ping과 RTT
- **Ping**: 유틸리티 프로그램 (프로토콜 자체는 아님)
- **목적**: RTT (Round Trip Time) 측정
- **RTT**: 패킷이 목적지까지 갔다가 돌아오는 시간
- **사용 프로토콜**: ICMP (Internet Control Message Protocol)

<br>

## 섹션 5. L4 수준 대표주자 TCP와 UDP
---
### TCP와 UDP 비교

| 특징 | TCP | UDP |
|------|-----|-----|
| **연결** | 연결 지향 (Connection) | 비연결 |
| **신뢰성** | 높음 (재전송, 순서 보장) | 낮음 |
| **속도** | 상대적으로 느림 | 빠름 |
| **혼잡 제어** | O | X |
| **순서 보장** | O | X |
| **사용 예** | 웹, 이메일, 파일 전송 | 게임, 스트리밍, DNS |

**핵심 차이점:**
- TCP에만 **연결(Connection, Session)** 개념이 존재
- 연결은 **상태(전이)** 개념을 동반

![tcp-3-way-handshack](https://lh3.googleusercontent.com/d/1P6tOeC8VJGvdZGZNGe3wrlI6gL46dBhD)

### TCP 연결 과정 (3-Way Handshake)
- **의미**: 정책 교환 단계
- **주도권**: 일반적으로 Client가 더 능동적 (연결 수립/해제 선택)
- **MSS (Maximum Segment Size) 교환**:
  - 클라이언트와 서버가 MSS를 공유
  - 작은 쪽 MSS에 맞춰 Segment 크기 조정

### TCP 연결 종료 과정 (4-Way Handshake)
- **Socket 특성**: 유한한 자원 → Closed와 동시에 회수
- **⚠️ 중요 원칙**: 
  - 연결 종료는 반드시 **Client 측에서** 수행
  - 이유: Server 측에서 먼저 종료 시 **Time Wait** 발생
  - Time Wait 상태가 쌓이면 서버 리소스 고갈

![tcp-4-way-handshack](https://lh3.googleusercontent.com/d/1WrENgu3DEtSvNBP_MpUE7jjDTs_DlD00)

### TCP Header 형식
- **포트 번호 범위**: 0 ~ 65535 (실제로는 1 ~ 65534 사용)
  - 총 2¹⁶ = 65,536개
  - 0번, 65535번은 예약됨
- **Checksum**: 전송 중 데이터 손상 여부 확인

### UDP Header 형식
- **특징**:
  - 혼잡 제어 없음
  - 수신측 상태 무시 (일방적 전송)
  - 헤더가 단순하여 오버헤드 적음

**게임 서버가 UDP를 사용하는 이유:**
- TCP 사용 시: 네트워크 상태가 안 좋은 유저에 맞춰 전체가 하향 평준화
- UDP 사용 시: 각 클라이언트를 독립적으로 처리 가능

<br>

## 섹션 6. 웹을 이루는 핵심 기술
---
### DNS (Domain Name System)
- **구조**: 분산형 계층적 데이터베이스
- **목적**: 도메인 이름을 IP 주소로 변환

**도메인 구조:**
```
www.naver.com
│   └─────┬───┘
│      Domain Name
└─ Host Name
```

**DNS 조회 최적화:**
1. **DNS Cache**: Host가 한 번 조회한 결과를 캐시에 저장 (Expired 시까지)
2. **hosts 파일**: 로컬 파일에 기록 시 DNS 조회 생략
3. **DNS Forwarding**: 공유기가 제공하는 DNS 중계 기능

### URL과 URI
- **URL (Uniform Resource Locator)**: 리소스의 위치
- **URI (Uniform Resource Identifier)**: 리소스의 식별자
- **관계**: URL은 URI에 포함되는 개념
- **Resource**: File과 동일하게 생각하면 편함

**URL 구조:**
```
Protocol://Address:Port/Path?Parameter=value
   ↓        ↓       ↓    ↓         ↓
  http   domain    80  /page   ?id=123
```

**예시:**
```
http://www.test.co.kr/index.html
                      └─ 생략 가능 (기본값)
```

### HTTP (HyperText Transfer Protocol)
- **정의**: HTML 문서를 전송하기 위해 만들어진 L7 통신 프로토콜
- **특징**: 
  - L5 이상은 Socket 통신
  - Stream 데이터 사용 (시작은 있지만 끝이 정해지지 않음)
  - 끝은 HTTP 프로토콜로 해석

**HTTP Header 분류:**
1. **일반 헤더**: 요청/응답 모두 사용
2. **요청 헤더**: 클라이언트 정보
3. **응답 헤더**: 서버 정보
4. **엔티티 헤더**: 본문(body) 정보

### 주요 HTTP 응답 코드

**2xx - 성공:**
- `200 OK`: 요청 정상 처리
- `201 Created`: 새로운 자원 생성 성공

**3xx - 리다이렉션:**
- `301 Moved Permanently`: 영구 이동
- `302 Found`: 임시 이동

**4xx - 클라이언트 오류:**
- `400 Bad Request`: HTTP 규약 위반 요청
- `403 Forbidden`: 권한 없음, 잘못된 접근
- `404 Not Found`: 리소스 없음

**5xx - 서버 오류:**
- `500 Internal Server Error`: 서버 내부 오류로 요청 처리 불가

### HTTP Method
- **GET**: 리소스 조회
- **POST**: 리소스 생성, 데이터 전송
- **HEAD**: 헤더 정보만 조회
- **TRACE**: 요청 경로 확인
- **PUT**: 리소스 전체 수정
- **DELETE**: 리소스 삭제
- **OPTIONS**: 서버가 지원하는 메소드 확인
- **CONNECT**: 프록시를 통한 터널링

### Web 서비스 구조

**Web 브라우저 구성 요소:**
1. **구문 분석**: HTML, CSS 파싱
2. **렌더링**: 화면에 표시
3. **JS 엔진**: JavaScript 실행

**개발 설계 원칙:**
- **UI, Data, 제어 분리**
  - CSS: UI (스타일)
  - HTML: Data (구조)
  - JavaScript: 제어 (동작)
- **⚠️ 보안 원칙**: 원격지 사용자 입력은 반드시 검증 대상

### APM (Application Performance Monitoring)
- **위치**: WAS와 DB 사이
- **목적**: 성능 및 속도 모니터링

**주요 모니터링 지표:**
- **TPS (Transaction Per Second)**: 초당 처리 트랜잭션 수
- **응답 시간**: 요청부터 응답까지 소요 시간
- **병목 지점**: 성능 저하 구간 파악

<br>

## Related Posts
---
- [[Inflearn] "외워서 끝내는 네트워크 핵심이론 - 기초" Review](https://bangjeongbin.github.io/TIL-Blog/posts/review-inflearn-network-core-theory-of-memorabilization)

<br>

## References
---
- [외워서 끝내는 네트워크 핵심이론 - 기초](https://www.inflearn.com/course/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%ED%95%B5%EC%8B%AC%EC%9D%B4%EB%A1%A0-%EA%B8%B0%EC%B4%88)
