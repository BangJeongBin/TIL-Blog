---
title: "[YouTube] \"조현준 보안스쿨 - 기초강의\" Note-Taking [3]"
description: "[YouTube] \"조현준 보안스쿨 - 기초강의\" 공부기록 3편"
author: bin
date: 2026-02-09 09:00:00 +0800
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

## 8. 전송 계층 프로토콜
---
### 8.1 UDP (User Datagram Protocol)
---
#### 특징
- **비연결형** 프로토콜
- **비신뢰성** 전송 (전송 보장 X)
- 가상 연결 미형성
- 빠른 전송 속도
- 단순한 헤더 (8바이트 고정)
- Sequence Number 없음
- 오류 제어 최소화

#### 장단점
- **장점**: 빠른 속도, 낮은 오버헤드, 실시간성
- **단점**: 신뢰성 없음, 순서 보장 X, 흐름제어/혼잡제어 없음

#### 사용 사례
- DNS 질의/응답
- DHCP
- 스트리밍 (음성/영상)
- 온라인 게임
- SNMP
- TFTP

#### UDP 헤더 구조 (8바이트)

##### Source Port (출발지 포트): 16비트
- 송신 프로세스의 포트 번호
- 선택 사항 (0 가능)

##### Destination Port (목적지 포트): 16비트
- 수신 프로세스의 포트 번호
- 필수

##### Length (전체 길이): 16비트
- UDP 헤더 + 데이터 전체 길이
- 최소 8바이트

##### Checksum (체크섬): 16비트
- 오류 검출용
- IPv4에서는 선택, IPv6에서는 필수
- 출발지와 목적지에서 계산하여 비교
- 오류 발견 시 도착지에서 패킷 폐기 (재전송 요청 X)

<br>

### 8.2 TCP (Transmission Control Protocol)
---
#### 특징
- **연결지향형** 프로토콜
- **신뢰성** 있는 전송
- 가상 연결 형성 (3-way handshake)
- 느리지만 확실한 전송
- 가변 헤더 (20~60바이트)
- Sequence Number 사용 → 순서 보장
- 흐름제어, 오류제어, 혼잡제어 제공

#### 장단점
- **장점**: 신뢰성, 순서 보장, 흐름/혼잡 제어
- **단점**: 느린 속도, 높은 오버헤드

#### 사용 사례
- HTTP/HTTPS (웹)
- FTP (파일 전송)
- SMTP (이메일)
- SSH (원격 접속)
- Telnet

#### TCP 헤더 구조 (최소 20바이트)

##### Source Port (출발지 포트): 16비트

##### Destination Port (목적지 포트): 16비트

##### Sequence Number (순서 번호): 32비트
- 전송하는 데이터의 첫 바이트 번호
- 순서 보장 및 재조립에 사용

##### Acknowledgment Number (확인 응답 번호): 32비트
- 다음에 받기를 기대하는 바이트 번호
- ACK 플래그와 함께 사용

##### Header Length (헤더 길이): 4비트
- TCP 헤더 길이 (32비트 단위)
- 가변 길이 (옵션 필드 때문)

##### Reserved (예약): 6비트
- 미래 사용을 위해 예약
- 항상 0

##### Control Flags (제어 플래그): 6비트
★ 시험 빈출 **UAPRSF** (유압 씨프)

- **URG** (Urgent): 긴급 데이터, Urgent Pointer 필드 유효
- **ACK** (Acknowledgment): 확인 응답, Ack Number 필드 유효
- **PSH** (Push): 버퍼링 없이 즉시 응용 계층으로 전달
- **RST** (Reset): 연결 강제 종료, 비정상 종료
- **SYN** (Synchronize): 연결 설정, 초기 순서 번호 동기화
- **FIN** (Finish): 연결 종료 요청, 정상 종료

##### Window Size (윈도우 크기): 16비트
- 수신 가능한 데이터 양 (흐름 제어)
- 슬라이딩 윈도우 방식

##### Checksum (체크섬): 16비트
- 헤더 + 데이터 오류 검출
- 필수 (UDP와 달리)

##### Urgent Pointer (긴급 포인터): 16비트
- URG 플래그 설정 시 긴급 데이터의 마지막 바이트 위치

##### Options (옵션): 가변 길이
- MSS (Maximum Segment Size)
- Window Scale
- SACK (Selective ACK)
- Timestamp

#### TCP 연결 관리

##### 3-way Handshake (연결 설정)
1. 클라이언트 → 서버: SYN
2. 서버 → 클라이언트: SYN + ACK
3. 클라이언트 → 서버: ACK

##### 4-way Handshake (연결 종료)
1. 클라이언트 → 서버: FIN
2. 서버 → 클라이언트: ACK
3. 서버 → 클라이언트: FIN
4. 클라이언트 → 서버: ACK

<br>

## 9. 이메일 보안
---
### 9.1 PEM (Privacy Enhanced Mail)
---
#### 특징
- **중앙집중화된** 키 인증 체계
- **높은 보안성** (군사용, 금융계 적합)
- **이론 중심** 설계
- **사용률 낮음** (복잡성, 구현 어려움)
- X.509 인증서 기반
- 계층적 인증 구조

#### 장단점
- **장점**: 강력한 보안, 표준화된 구조
- **단점**: 구현 복잡, 중앙 관리 부담, 확장성 제한

<br>

### 9.2 PGP (Pretty Good Privacy)
---
★ 현재 가장 많이 사용

#### 특징
- **Phil Zimmermann**이 개발 (1991년)
- **분산화된** 키 인증 (Web of Trust)
- **구현의 용이성** 중시
- **실세계 사용 중심**
- **현재 가장 많이 사용**되는 이메일 암호화 솔루션
- OpenPGP 표준

#### Web of Trust (신뢰의 그물망)
- 사용자 간 상호 인증
- 중앙 인증 기관 불필요
- 신뢰도 레벨 설정

#### 기능
- 암호화: RSA, AES
- 디지털 서명
- 압축: ZIP
- Base64 인코딩

#### 장단점
- **장점**: 분산 구조, 구현 용이, 유연성
- **단점**: 신뢰 관리 복잡, 키 배포 문제

<br>

### 9.3 S/MIME (Secure/Multipurpose Internet Mail Extensions)
---
#### 특징
- **MIME 기반** + 보안 기능 추가
- **전자서명** 및 **암호화** 기술 제공
- **다양한 상용 툴킷** 지원
- **X.509 인증서** 기반 (PKI)
- 엔터프라이즈 환경에서 많이 사용

#### 주요 기능
- 메시지 암호화 (기밀성)
- 디지털 서명 (인증, 무결성, 부인방지)
- 인증서 관리

#### 장단점
- **장점**: 상용 지원 우수, PKI 통합, 표준화
- **단점**: 인증서 관리 필요, 비용

<br>

### 9.4 이메일 보안 비교
---

|   구분   |  PEM  |        PGP        |   S/MIME    |
| :----: | :---: | :---------------: | :---------: |
|  키 관리  | 중앙집중  | 분산 (Web of Trust) | PKI (X.509) |
| 사용 목적  | 군사/금융 |       개인/일반       |    기업/상용    |
| 구현 복잡도 |  높음   |        중간         |     중간      |
| 현재 사용률 |  낮음   |        높음         |     높음      |
|  인증서   | X.509 |      PGP 인증서      |    X.509    |

<br>

## 10. OSI 계층별 웹 보안 기술
---
### 10.1 네트워크 계층 (L3)
---
#### IPsec (IP Security)
- IP 패킷 암호화 및 인증
- VPN 구축
- **AH** (Authentication Header): 인증 및 무결성
- **ESP** (Encapsulating Security Payload): 암호화 및 인증
- 전송 모드 / 터널 모드

<br>

### 10.2 전송 계층 (L4)
---
#### SSL (Secure Sockets Layer)
- Netscape 개발
- 현재는 deprecated
- **TLS (Transport Layer Security)**
- SSL의 후속 표준
- HTTPS (HTTP over TLS)
- 웹 통신 암호화의 표준
- 버전: TLS 1.0, 1.1, 1.2, 1.3 (최신)

**TLS 동작 과정**
1. Handshake: 암호화 협상, 인증
2. Key Exchange: 세션키 교환
3. Data Transfer: 암호화 통신

<br>

### 10.3 응용 계층 (L7)
---
- **S/MIME**: 이메일 보안
- **PGP**: 이메일/파일 암호화
- **Kerberos**
    - **대칭키 기반** 인증 프로토콜
    - **티켓(Ticket)** 방식
    - MIT 개발
    - 단일 인증(SSO) 지원

#### Kerberos 구성 요소
- KDC (Key Distribution Center)
    - AS (Authentication Server): 인증
    - TGS (Ticket Granting Server): 티켓 발급
- 클라이언트
- 서비스 서버

#### Kerberos 동작 과정
1. AS에 인증 요청 → TGT 발급
2. TGS에 TGT 제시 → 서비스 티켓 발급
3. 서비스 서버에 서비스 티켓 제시 → 접근

<br>

## Related Posts
---
- [[YouTube] "조현준 보안스쿨 - 기초강의" Review](https://bangjeongbin.github.io/TIL-Blog/posts/review-youtube-cho-hyun-joon-security-school-basic-course)
- [[YouTube] "조현준 보안스쿨 - 기초강의" Note-Taking [1]](https://bangjeongbin.github.io/TIL-Blog/posts/note-taking-youtube-cho-hyun-joon-security-school-basic-course-1)
- [[YouTube] "조현준 보안스쿨 - 기초강의" Note-Taking [2]](https://bangjeongbin.github.io/TIL-Blog/posts/note-taking-youtube-cho-hyun-joon-security-school-basic-course-2)
- [[YouTube] "조현준 보안스쿨 - 기초강의" Note-Taking [4]](https://bangjeongbin.github.io/TIL-Blog/posts/note-taking-youtube-cho-hyun-joon-security-school-basic-course-4)

<br>

## References
---
- [조현준 보안스쿨 - 기초강의](https://www.youtube.com/playlist?list=PLaR0eJQDBqV-NeNVmyIuC9Snb9hotoAhu)
