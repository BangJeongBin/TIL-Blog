---
title: "[YouTube] \"조현준 보안스쿨 - 기초강의\" Note-Taking [2]"
description: "[YouTube] \"조현준 보안스쿨 - 기초강의\" 공부기록 2편"
author: bin
date: 2026-02-02 09:00:00 +0800
categories: [Review, Note-Taking]
tags: [Certificate]
pin: true
math: true
mermaid: true
image:
 path: https://bangjeongbin.github.io/TIL-Blog/assets/img/posts/common/note-taking-logo.png
 alt: Note Taking
---

> 해당 포스트는 학습 목적으로 작성되었으며 <<[조현준 보안스쿨 - 기초강의](https://www.youtube.com/playlist?list=PLaR0eJQDBqV-NeNVmyIuC9Snb9hotoAhu)>>을 참고하여 작성하였음을 알려드립니다.

<br>

## 5. 네트워크 프로토콜
---
### 5.1 HTTP 연결
---
#### HTTP/1.0
- **특징**: 비영속적 연결 (Non-Persistent Connection)
- 매 요청마다 TCP 연결 생성 및 종료
- 오버헤드 큼

#### HTTP/1.1
- **특징**: 영속적 연결 (Persistent Connection)
- 하나의 TCP 연결로 여러 요청/응답 처리
- Keep-Alive 헤더
- 파이프라이닝 지원

#### HTTP/2
- 멀티플렉싱, 헤더 압축
- 서버 푸시 기능

<br>

### 5.2 Slow HTTP DDoS 공격 (3가지)
---
#### 1. Slowloris (Slow HTTP Header DoS)
- **방식**: HTTP 헤더를 천천히 전송
- 완전한 요청을 보내지 않고 연결 유지
- 서버 연결 자원 고갈

#### 2. RUDY (Slow HTTP POST DoS, R-U-Dead-Yet)
- **방식**: POST 요청의 Body를 천천히 분할 전송
- Content-Length는 크게 설정하고 데이터는 천천히 전송
- 서버가 요청 완료를 대기하며 자원 소모

#### 3. Slow HTTP Read DoS
- **방식**: HTTP 응답을 천천히 읽음
- Window Size를 작게 설정하여 서버가 응답을 천천히 전송하도록 유도
- 서버 연결 자원 장시간 점유

**대응 방법**
- 연결 타임아웃 설정
- 최소 전송 속도 요구
- 동일 IP의 연결 수 제한
- Rate Limiting

<br>

## 6. OSI 7 계층 (OSI 7 Layer)
---

|계층|이름|특징|데이터 단위|주요 프로토콜|장비|
|:-:|:-:|:--|:-:|:-:|:-:|
|**7**|응용 계층<br>(Application)|- 각종 응용 서비스 제공<br>- 사용자 인터페이스<br>- 네트워크 관리|Message|`HTTP`, `HTTPS`, `FTP`, `TFTP`,<br>`SMTP`, `POP3`, `IMAP`,<br>`DNS`, `DHCP`, `SNMP`,<br>`Telnet`, `SSH`|Gateway,<br>Proxy|
|**6**|표현 계층<br>(Presentation)|- 데이터 형식 변환<br>- 암호화/복호화<br>- 압축/압축 해제<br>- 인코딩/디코딩|Message|`ASCII`, `EBCDIC`,<br>`JPEG`, `MPEG`, `GIF`,<br>`MIME`, `SSL/TLS`|Gateway|
|**5**|세션 계층<br>(Session)|- 세션 연결/관리/종료<br>- 동기화 (체크포인트)<br>- 대화 제어<br>- 소켓 연결 관리|Message|전송 모드 결정<br>(반이중, 전이중)<br>`NetBIOS`, `RPC`,<br>`SQL`, `NFS`|Gateway|
|**4**|전송 계층<br>(Transport)|- End-to-End 통신<br>- 신뢰성 있는 데이터 전송<br>- 흐름제어, 오류제어, 혼잡제어<br>- QoS 보장<br>- 포트 번호 사용|Segment|`TCP`, `UDP`,<br>`SCTP`|Gateway,<br>L4 Switch|
|**3**|네트워크 계층<br>(Network)|- 논리적 주소 지정 (IP)<br>- 라우팅 (경로 설정)<br>- 패킷 전달<br>- 단편화/재조립|Packet|`IP`, `ICMP`, `IGMP`,<br>`ARP`, `RARP`,<br>`NAT`, `IPSEC`,<br>`RIP`, `OSPF`, `BGP`|Router,<br>L3 Switch|
|**2**|데이터링크 계층<br>(Data Link)|- 물리적 주소 지정 (MAC)<br>- 프레임화<br>- 오류 검출 및 정정<br>- 흐름제어<br>- 매체 접근 제어|Frame|`Ethernet`, `Token Ring`,<br>`PPP`, `HDLC`, `SLIP`,<br>`802.11 (Wi-Fi)`,<br>`MAC`, `LLC`|Bridge,<br>Switch,<br>NIC|
|**1**|물리 계층<br>(Physical)|- 물리적 연결 설정/해제<br>- 비트 스트림 전송<br>- 전송 매체 정의<br>- 전기적/기계적 규격<br>- 신호 변환|Bit Stream|케이블, 커넥터,<br>리피터, 신호 규격<br>(RS-232, V.35)|Hub,<br>Repeater,<br>Cable|

<br>

### 6.1 계층별 제어 기능
---
#### L4 전송 계층: 오류제어 + 흐름제어 + 혼잡제어
- **논리적 제어** (End-to-End)
- 신뢰성 있는 데이터 전송 보장

#### L2 데이터링크 계층: 오류제어 + 흐름제어
- **물리적 제어** (Hop-by-Hop)
- 인접 노드 간 신뢰성 있는 전송

#### 오류제어 (Error Control)
- **목적**: 전송 오류 검출 및 정정
- **방법**:
    - ARQ (Automatic Repeat Request): 재전송 요구
        - Stop-and-Wait ARQ
        - Go-Back-N ARQ
        - Selective Repeat ARQ
    - FEC (Forward Error Correction): 오류 정정 코드

#### 흐름제어 (Flow Control)
- **목적**: 송신자와 수신자 간 전송 속도 조절
- **방법**:
    - Stop-and-Wait
    - Sliding Window: Window Size 조절
- **Window Size**: 확인 응답 없이 전송 가능한 데이터 양

#### 혼잡제어 (Congestion Control)
- **목적**: 네트워크 혼잡 방지 및 해소
- **방법**:
    - Slow Start
    - Congestion Avoidance
    - Fast Retransmit
    - Fast Recovery
- **트래픽 양 조절**: 네트워크 전체 부하 관리

<br>

## 7. IP 프로토콜
---
### 7.1 패킷 전송 방법
---
#### Unicast (유니캐스트)
- 1:1 통신
- 특정 단일 호스트에게 전송
- 가장 일반적인 전송 방식

#### Multicast (멀티캐스트)
- 1:N 통신
- 특정 그룹(다수)에게 전송
- 멀티캐스트 그룹 주소 사용
- 예시: IPTV, 화상회의

#### Broadcast (브로드캐스트)
- 1:All 통신
- 같은 네트워크의 모든 호스트에게 전송
- IPv4에서만 지원 (IPv6는 미지원)
- 예시: ARP 요청, DHCP Discover

#### Anycast (애니캐스트)
- 1:Nearest 통신
- 그룹 내 가장 가까운 하나의 호스트에게 전송
- 주로 IPv6에서 사용
- 예시: DNS 루트 서버, CDN

<br>

### 7.2 헤더 구조
---
#### 공통 규칙
- **IP 헤더**의 첫 번째 필드: **버전 (Version)**
- **TCP/UDP 헤더**의 첫 번째 필드: **소스 포트 주소 (Source Port)**

<br>

### 7.3 IPv4
---
#### 주요 특징
- **주소 길이**: 32비트 (4바이트)
- **헤더 길이**: 가변 (20~60바이트)
- **주소 표기**: 점-십진 표기법 (예: 192.168.0.1)
- **브로드캐스트**: 지원
- **헤더 체크섬**: 있음

#### 주요 헤더 필드

##### Version (버전): 4비트
- IP 프로토콜 버전 (IPv4 = 4)

##### Header Length (헤더 길이): 4비트
- 헤더 길이를 32비트 단위로 표시
- 최소값 5 (20바이트), 최대값 15 (60바이트)

##### Total Length (전체 길이): 16비트
- 헤더 + 데이터 전체 길이
- 최대 65,535바이트

##### Identification (식별자): 16비트
- 단편화된 패킷들을 식별하기 위한 고유 번호

##### Flags (플래그): 3비트
- **bit 0**: Reserved (예약, 항상 0)
- **bit 1**: DF (Don't Fragment)
    - 1: 단편화 금지
    - 0: 단편화 허용
- **bit 2**: MF (More Fragments)
    - 1: 뒤에 단편 있음
    - 0: 마지막 단편 (또는 단편화 안됨)

##### Fragment Offset (단편 오프셋): 13비트
- 원본 데이터에서의 위치
- 8바이트 단위

##### TTL (Time To Live): 8비트
- 패킷의 최대 생존 시간 (홉 수)
- 라우터 경유 시마다 1씩 감소
- 0이 되면 폐기 → 무한 루프 방지

##### Protocol (프로토콜): 8비트
- 상위 계층 프로토콜 식별 (다중화)
- 예시: TCP=6, UDP=17, ICMP=1
- **다중화 관련**:
    - L4: Port Number
    - L3: Protocol Number
    - L2: Type (Ethertype)

##### Header Checksum (헤더 체크섬): 16비트
- 헤더의 오류 검사
- 단편화 후 재계산 필요
- 데이터는 포함하지 않음

##### Source/Destination Address: 각 32비트
- 송신지/목적지 IP 주소

<br>

### 7.4 IPv6
---
#### 주요 특징
- **주소 길이**: 128비트 (16바이트)
- **헤더 길이**: 고정 40바이트
- **주소 표기**: 콜론-16진수 표기법
	- `E.g. 2001:0db8::1`
- **브로드캐스트**: 미지원 → 멀티캐스트 사용
- **헤더 체크섬**: 없음 (상위 계층에서 처리)
- **주소 공간**: 2^128개 (거의 무한대)

#### IPv4 대비 개선사항
- 주소 공간 대폭 확장
- 헤더 단순화 (처리 속도 향상)
- 보안 기능 내재화 (IPsec 필수)
- QoS 지원 강화
- 자동 구성 (Auto-configuration)

#### 삭제된 5개 헤더 필드
1. **Header Length** (헤더 길이): 고정 길이로 불필요
2. **Identification** (식별자): 확장 헤더로 이동
3. **Flags** (플래그): 확장 헤더로 이동
4. **Fragment Offset** (단편 오프셋): 확장 헤더로 이동
5. **Header Checksum** (헤더 체크섬): 상위/하위 계층에서 처리

#### 주요 헤더 필드

##### Version (버전): 4비트
- IPv6 = 6

##### Traffic Class (트래픽 클래스): 8비트
- QoS, 우선순위 지정
- IPv4의 ToS(Type of Service)에 해당

##### Flow Label (플로우 레이블): 20비트
- 특정 플로우(흐름)에 대한 특별한 처리 제공
- 실시간 트래픽 처리
- QoS 보장

##### Payload Length (페이로드 길이): 16비트
- 데이터 길이 (헤더 길이 제외)
- IPv4의 Total Length와 유사하지만 헤더 미포함
- 확장 헤더 포함

##### Next Header (다음 헤더): 8비트
- 다음에 오는 헤더 유형 지정
- 확장 헤더 또는 상위 계층 프로토콜
- **확장 헤더 예시**:
    - Hop-by-Hop Options
    - Routing
    - Fragment
    - **Authentication (AH)**: IPsec 인증
    - **ESP (Encapsulating Security Payload)**: IPsec 암호화
    - Destination Options

##### Hop Limit (홉 제한): 8비트
- IPv4의 TTL과 동일한 역할
- 무한 루프 방지

##### Source/Destination Address: 각 128비트
- 송신지/목적지 IPv6 주소

<br>

## Related Posts
---
- [[YouTube] "조현준 보안스쿨 - 기초강의" Review](https://bangjeongbin.github.io/TIL-Blog/posts/review-youtube-cho-hyun-joon-security-school-basic-course)
- [[YouTube] "조현준 보안스쿨 - 기초강의" Note-Taking [1]](https://bangjeongbin.github.io/TIL-Blog/posts/note-taking-youtube-cho-hyun-joon-security-school-basic-course-1)
- [[YouTube] "조현준 보안스쿨 - 기초강의" Note-Taking [3]](https://bangjeongbin.github.io/TIL-Blog/posts/note-taking-youtube-cho-hyun-joon-security-school-basic-course-3)
- [[YouTube] "조현준 보안스쿨 - 기초강의" Note-Taking [4]](https://bangjeongbin.github.io/TIL-Blog/posts/note-taking-youtube-cho-hyun-joon-security-school-basic-course-4)

<br>

## References
---
- [조현준 보안스쿨 - 기초강의](https://www.youtube.com/playlist?list=PLaR0eJQDBqV-NeNVmyIuC9Snb9hotoAhu)
