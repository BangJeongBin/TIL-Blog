---
title: "[YouTube] \"조현준 보안스쿨 - 기초강의\" Note-Taking [1]"
description: "[YouTube] \"조현준 보안스쿨 - 기초강의\" 공부기록 1편"
author: bin
date: 2026-01-29 09:00:00 +0800
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

## 1. 정보보안의 3대 목표 (CIA)
---
### C - 기밀성 (Confidentiality)
- **위협**: 훔쳐보기, 가로채기, 도청, 스니핑
- **공격 유형**: 소극적 공격 (Passive Attack)
- **대책**: 암호화, 접근통제, 인증
- **특징**: 공격 탐지가 어려움 (데이터만 읽고 변경하지 않음)

<br>

### I - 무결성 (Integrity)
- **위협**: 변경, 위조, 삭제, 삽입
- **공격 유형**: 적극적 공격 (Active Attack)
- **대책**: 해시함수, 메시지 인증 코드(MAC), 디지털 서명
- **특징**: 공격 탐지가 상대적으로 용이함

<br>

### A - 가용성 (Availability)
- **위협**: DDoS, 시스템 파괴, 서비스 중단
- **공격 유형**: 적극적 공격 (Active Attack)
- **대책**: 백업, 복구, 이중화, 장애 대응 체계
- **추가 대책**: 방화벽, IDS/IPS, 트래픽 분산

<br>

### 추가 보안 요소

#### 인증 (Authentication)
- 자격 검증 및 신원 확인
- 정당한 사용자인지 확인하는 프로세스

#### 책임추적성 (Accountability)
- 사용자 행위 추적 및 기록
- 예시: 로그(Log) 관리, 감사 추적(Audit Trail)
- 부인방지와 연계

#### 부인방지 (Non-Repudiation)
- 행위에 대한 부인을 방지
- 디지털 서명을 통한 송수신 사실 증명
- 법적 효력 확보

<br>

## 2. 암호학 (Cryptography)
---
### 2.1 암호화 시스템 분류
---
#### 양방향 암호화
암호화와 복호화가 모두 가능한 시스템

##### 대칭키 암호화 (Symmetric Key Cryptography)
- **특징**: 암호화 키 = 복호화 키
- **장점**: 빠른 처리속도, 작은 키 사이즈
- **단점**: 키 배송 문제 (Key Distribution Problem)
- **용도**: 대용량 데이터 암호화, 기밀성 유지

**스트림 암호 (Stream Cipher)**
- XOR 연산 기반
- 비트 단위 또는 바이트 단위 암호화
- 예시: RC4, A5/1
- 특징: 빠른 속도, 하드웨어 구현 용이

**블록 암호 (Block Cipher)**
- 고정된 블록 단위로 암호화
- 치환(Substitution)과 전치(Permutation) 사용
- 예시: DES, 3DES, AES, ARIA, SEED
- 운용 모드: ECB, CBC, CFB, OFB, CTR
- 특징: 높은 보안성, 다양한 응용 가능

##### 비대칭키 암호화 (Asymmetric Key Cryptography, 공개키 암호)
- **특징**: 암호화 키 ≠ 복호화 키 (공개키/개인키 쌍)
- **장점**: 키 배송 문제 해결, 디지털 서명 가능
- **단점**: 느린 처리속도, 큰 키 사이즈
- **용도**: 키 교환, 디지털 서명, 인증
- **송수신자**: 모두 한 쌍의 키(공개키/개인키) 보유 필요
- **대표 알고리즘**: RSA, ECC, ElGamal, DSA

**암호화 방식**
- 공개키로 암호화 → 개인키로 복호화 (기밀성)
- 개인키로 암호화 → 공개키로 복호화 (인증 및 부인방지)

<br>

#### 단방향 암호화
복호화가 불가능한 암호화

##### 해시 함수 (Hash Function)
- **특징**:
    - 암호화만 가능 (복호화 불가)
    - 고정된 길이의 출력 (해시값, 다이제스트)
    - 동일 입력 → 동일 출력 (결정론적)
    - 눈사태 효과 (Avalanche Effect): 입력의 작은 변화가 출력의 큰 변화 유발
- **요구사항**:
    - 역상 저항성 (Preimage Resistance)
    - 제2역상 저항성 (Second Preimage Resistance)
    - 충돌 저항성 (Collision Resistance)
- **용도**: 무결성 검증, 패스워드 저장, 디지털 서명
- **예시**: MD5, SHA-1, SHA-2 (SHA-256, SHA-512), SHA-3

|구분|대칭키|비대칭키|
|:-:|:-:|:-:|
|장점|빠른 처리속도|키 배송 문제 해결|
|단점|키 배송 문제|느린 처리속도|
|키 개수|n(n-1)/2 (많음)|2n (적음)|
|키 길이|짧음 (128bit)|길음 (2048bit 이상)|

<br>

### 2.2 하이브리드 암호 시스템
---
- **개념**: 대칭키와 비대칭키의 장점을 결합
- **동작 방식**:
    1. 대칭키로 실제 데이터 암호화 (빠른 속도)
    2. 비대칭키로 대칭키 암호화하여 전송 (안전한 키 교환)
- **예시**: SSL/TLS, PGP, S/MIME
- **세션키**: 통신마다 생성되는 일회용 대칭키

<br>

### 2.3 주요 암호 알고리즘
---
#### XOR 연산 (Exclusive OR)
- 두 값이 동일하면 0 (False)
- 두 값이 다르면 1 (True)
- 특징: 자기 자신과 XOR하면 0, 같은 값 두 번 XOR하면 원래 값
- 스트림 암호의 기본 연산

#### 모듈러 연산 (Modular Arithmetic)
- **용도**:
    - Diffie-Hellman 키 교환
    - RSA 알고리즘 키 생성 및 암복호화
    - ElGamal 암호
- **개념**: 나머지 연산을 이용한 수학적 계산
- **보안 근거**: 이산대수 문제, 소인수분해 문제의 어려움

<br>

## 3. 접근통제 (Access Control)
---
### 3.1 접근통제 3요소
---
#### 식별 (Identification)
- 본인이 누구인지 시스템에 밝히는 것
- 책임 추적성의 기반
- 수단: ID (공개 정보)
- 특징: 고유성 보장 필요

#### 인증 (Authentication) ★
시스템이 사용자의 신원을 검증하고 인정하는 과정

##### 인증의 3요소 (Three Factors of Authentication)

|     구분     |             Type              |      특징       |                 예시                  | 비용  |            공격 방식             |
| :--------: | :---------------------------: | :-----------: | :---------------------------------: | :-: | :--------------------------: |
| **Type 1** | 지식 기반<br>(Something You Know) | 사용자가 알고 있는 정보 |   패스워드, PIN,<br>패스프레이즈,<br>보안 질문    | 낮음  | 추측, 사전 공격,<br>무차별 대입,<br>키로깅 |
| **Type 2** | 소유 기반<br>(Something You Have) |  사용자가 소유한 물건  | OTP 토큰,<br>스마트카드,<br>인증서,<br>모바일 기기 | 중간  |        강탈, 도난,<br>복제         |
| **Type 3** | 존재 기반<br>(Something You Are)  |  사용자의 생체 특징   |    지문, 홍채,<br>얼굴, 정맥,<br>음성, 망막     | 높음  |   위조 어려움,<br>바이오메트릭<br>스푸핑   |

**다중 인증 (Multi-Factor Authentication, MFA)**
- 2개 이상의 서로 다른 Type 조합
- 2FA (Two-Factor Authentication): 2개 Type 사용
- 보안성 크게 향상

##### 인증 유형
- **사용자 인증**: 사람의 신원 확인
- **메시지 인증**: 메시지의 출처 및 무결성 확인 (MAC, HMAC)
- **기기 인증**: 디바이스의 정당성 확인

#### 인가 (Authorization)
- **개념**: 인증된 사용자에게 권한을 부여하는 과정
- **원칙**:
    - 최소 권한의 원칙 (Principle of Least Privilege)
    - 업무 분리의 원칙 (Separation of Duties)
    - 차등 권한 부여
- **구현**: ACL (Access Control List), 권한 매트릭스

<br>

### 3.2 접근통제 모델
---
#### MAC (Mandatory Access Control, 강제적 접근통제)
- **특징**:
    - 중앙집중적 관리
    - 엄격한 보안 정책
    - 관리자가 모든 권한 통제
    - 보안 레이블(Security Label) 기반
- **장점**: 높은 보안성
- **단점**: 유연성 부족, 관리 복잡
- **적용**: 군사, 정부 기관
- **예시**: Bell-LaPadula 모델, Biba 모델

#### DAC (Discretionary Access Control, 임의적 접근통제)
- **특징**:
    - 소유자가 접근 권한 결정
    - 신분(Identity) 기반
    - 유연한 권한 관리
- **장점**: 구현 용이, 유연성
- **단점**: 보안 취약성, 권한 남용 가능
- **적용**: 일반 운영체제 (Windows, Linux)
- **예시**: ACL, 파일 시스템 권한

#### RBAC (Role-Based Access Control, 역할기반 접근통제)
- **특징**:
    - 역할(Role) 기반 권한 부여
    - 사용자-역할-권한의 간접 매핑
    - 완충 작용 (사용자와 객체 사이)
- **장점**:
    - 관리 효율성
    - 인사이동에 유연 대응
    - Authorization Creep 방지
- **적용**: 인사이동이 잦은 조직, 대규모 기업
- **구성요소**:
    - 사용자(User)
    - 역할(Role)
    - 권한(Permission)
    - 세션(Session)

**Authorization Creep**
- 사용자가 부서 이동 시 이전 권한이 누적되는 현상
- RBAC으로 해결 가능

<br>

## 4. 악성 소프트웨어 (Malware)
---
### 4.1 종속형 악성코드
---
호스트 프로그램에 의존하여 실행

#### Trapdoor ≈ Backdoor (백도어)
- 정상적인 인증 절차를 우회하는 비밀 통로
- 개발자가 의도적으로 남기거나 공격자가 생성
- 원격 접근 및 제어 가능

#### Logic Bomb (논리 폭탄)
- 특정 조건 충족 시 악성 행위 수행
- 시한폭탄 (Time Bomb): 특정 시각에 동작
- 예시: 퇴사 직원이 심어둔 삭제 코드

#### Virus (바이러스)
- **특징**:
    - 자기 복제 가능
    - 호스트 파일에 기생
    - 사용자 실행 필요
- **유형**:
    - 부트 바이러스: MBR 감염
    - 파일 바이러스: 실행 파일 감염
    - 매크로 바이러스: 문서 파일 감염
    - 스크립트 바이러스: 스크립트 파일 이용
- **대응**: 백신 프로그램, 정기 스캔

<br>

### 4.2 독립형 악성코드
독립적으로 실행 가능

#### Worm (웜)
- **특징**:
    - 자기 복제 가능
    - 독립적 실행 (호스트 불필요)
    - 네트워크를 통해 자동 전파
    - 시스템 자원 소모
- **피해**: 네트워크 마비, 시스템 과부하
- **예시**: Morris Worm, Code Red, SQL Slammer

#### Zombie (좀비)
- **특징**:
    - 공격자의 원격 제어를 받는 시스템
    - 봇(Bot)으로도 불림
    - DDoS 공격에 이용
- **Botnet**: 좀비들의 네트워크
- **C&C Server**: 좀비를 제어하는 명령 서버

#### 기타 악성코드
- **Ransomware (랜섬웨어)**: 데이터 암호화 후 금전 요구
- **Spyware (스파이웨어)**: 정보 수집 및 전송
- **Adware (애드웨어)**: 광고 강제 표시
- **Rootkit (루트킷)**: 시스템 깊숙이 숨어 탐지 회피
- **Trojan Horse (트로이 목마)**: 정상 프로그램으로 위장

<br>

## Related Posts
---
- [[YouTube] "조현준 보안스쿨 - 기초강의" Review](https://bangjeongbin.github.io/TIL-Blog/posts/review-youtube-cho-hyun-joon-security-school-basic-course)
- [[YouTube] "조현준 보안스쿨 - 기초강의" Note-Taking [2]](https://bangjeongbin.github.io/TIL-Blog/posts/note-taking-youtube-cho-hyun-joon-security-school-basic-course-2)
- [[YouTube] "조현준 보안스쿨 - 기초강의" Note-Taking [3]](https://bangjeongbin.github.io/TIL-Blog/posts/note-taking-youtube-cho-hyun-joon-security-school-basic-course-3)
- [[YouTube] "조현준 보안스쿨 - 기초강의" Note-Taking [4]](https://bangjeongbin.github.io/TIL-Blog/posts/note-taking-youtube-cho-hyun-joon-security-school-basic-course-4)

<br>

## References
---
- [조현준 보안스쿨 - 기초강의](https://www.youtube.com/playlist?list=PLaR0eJQDBqV-NeNVmyIuC9Snb9hotoAhu)
