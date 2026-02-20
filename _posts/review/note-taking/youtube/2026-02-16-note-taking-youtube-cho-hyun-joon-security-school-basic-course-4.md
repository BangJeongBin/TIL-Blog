---
title: "[YouTube] \"조현준 보안스쿨 - 기초강의\" Note-Taking [4]"
description: "[YouTube] \"조현준 보안스쿨 - 기초강의\" 공부기록 4편"
author: bin
date: 2026-02-16 09:00:00 +0800
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

## 11. 웹 애플리케이션 공격
---
### 11.1 XSS (Cross-Site Scripting)
---
#### 개념
- 웹 페이지에 악성 스크립트 삽입
- 사용자 브라우저에서 실행
- 클라이언트 측 공격

#### 유형

##### 1. 저장형 XSS (Stored XSS, Persistent XSS)
- 악성 스크립트가 서버에 저장
- 게시판, 댓글 등에 삽입
- 피해 지속적, 광범위

##### 2. 반사형 XSS (Reflected XSS, Non-Persistent XSS)
- 악성 스크립트가 요청에 포함
- URL, 검색어 등에 삽입
- 일회성 공격, 특정 사용자 대상

##### 3. DOM 기반 XSS (DOM-Based XSS)
- 클라이언트 측 스크립트에서 발생
- 서버 개입 없이 DOM 조작
- 탐지 어려움

#### 공격 시나리오
1. 공격자가 취약한 웹사이트에 악성 스크립트 삽입
2. 피해자가 해당 페이지 방문
3. 악성 스크립트가 피해자 브라우저에서 실행
4. 쿠키, 세션 정보 등을 공격자에게 전송

#### 피해
- 쿠키 탈취 → 세션 하이재킹
- 피싱 페이지 생성
- 키로깅
- 악성코드 유포

#### 대응 방안
- **입력값 검증 및 필터링**
- **출력값 인코딩** (HTML Entity Encoding)
- **CSP** (Content Security Policy) 적용
- **HttpOnly 쿠키** 플래그 설정
- **X-XSS-Protection** 헤더 사용

<br>

### 11.2 CSRF (Cross-Site Request Forgery)
---
#### 개념
- 사용자가 의도하지 않은 요청을 강제로 전송
- 인증된 사용자의 권한 도용
- 서버 측 공격

#### 공격 시나리오
1. 공격자가 악성 스크립트를 포함한 페이지 생성
2. 피해자가 정상 사이트에 로그인한 상태로 악성 페이지 방문
3. 악성 스크립트가 피해자 모르게 정상 사이트에 요청 전송
4. 정상 사이트는 인증된 요청으로 인식하여 처리
    - 개인정보 수정
    - 송금
    - 게시글 작성 등

#### 피해
- 권한 도용
- 의도하지 않은 행위 수행
- 개인정보 변경
- 금전적 피해

#### 대응 방안
- **CSRF 토큰** 사용
    - 예측 불가능한 토큰 생성
    - 요청마다 검증
- **Referer 검증**
- **SameSite 쿠키** 속성 설정
- **재인증** 요구 (중요한 작업)
- **CAPTCHA** 사용

<br>

### 11.3 XSS vs CSRF 비교
---

|  구분   | XSS           | CSRF          |
| :---: | :------------ | :------------ |
| 공격 대상 | 사용자 (클라이언트)   | 서버            |
| 공격 목적 | 정보 탈취         | 권한 도용         |
| 실행 위치 | 피해자 브라우저      | 서버            |
|  핵심   | 악성 스크립트 실행    | 위조된 요청 전송     |
|  공통점  | **입력값 검증 부실** | **입력값 검증 부실** |


<br>

### 11.4 SQL Injection
---
#### 개념
- SQL 쿼리에 악의적인 SQL 구문 삽입
- 데이터베이스 조작 및 정보 탈취
- 가장 위험한 웹 취약점 중 하나

#### 공격 기법
- **인증 우회**: `' OR '1'='1`
- **데이터 조회**: UNION SELECT
- **데이터 변조**: UPDATE, DELETE
- **시스템 명령 실행**: xp_cmdshell (MS-SQL)
- **Blind SQL Injection**: 참/거짓 반응 관찰

#### 공격 예시
```sql
-- 정상 쿼리
SELECT * FROM users WHERE id='user1' AND pw='pass123';

-- 공격 쿼리 (인증 우회)
SELECT * FROM users WHERE id='admin' --' AND pw='anything';
-- 결과: admin 계정으로 로그인 성공
```

#### 피해
- 데이터베이스 정보 유출
- 데이터 변조/삭제
- 인증 우회
- 시스템 장악

#### 대응 방안
- **Prepared Statement** (파라미터화된 쿼리) 사용
- **입력값 검증 및 필터링**
- **최소 권한 원칙** (DB 계정 권한 제한)
- **에러 메시지 숨김** (정보 노출 방지)
- **웹 방화벽(WAF)** 사용
- **ORM** (Object-Relational Mapping) 사용

<br>

## 12. 위험 관리 (Risk Management)
---
### 12.1 위험 대응 전략 (4가지)
---
#### 1. 위험 수용 (Risk Acceptance)
- **개념**: 현재의 위험을 받아들이고 잠재적 손실 비용 감수
- **적용 시기**:
    - 위험의 영향이 미미할 때
    - 대응 비용이 손실보다 클 때
    - 다른 대응 방법이 없을 때
- **예시**:
    - 소규모 시스템의 경미한 취약점
    - 발생 확률이 매우 낮은 위험

#### 2. 위험 감소 (Risk Reduction, Mitigation)
- **개념**: 위험을 감소시킬 수 있는 대책을 채택하여 구현
- **방법**:
    - 보안 통제 구현
    - 보안 솔루션 도입
    - 보안 정책 수립
- **예시**:
    - 방화벽 설치
    - 백신 프로그램 도입
    - 패치 관리
    - 교육 및 훈련

#### 3. 위험 회피 (Risk Avoidance)
- **개념**: 위험이 존재하는 프로세스나 사업을 수행하지 않고 포기
- **방법**:
    - 자산 매각
    - 사업 중단
    - 설계 변경
    - 대체 방안 선택
- **예시**:
    - 위험한 서비스 폐지
    - 취약한 시스템 교체
    - 아웃소싱 중단

#### 4. 위험 전가 (Risk Transfer, Transition)
- **개념**: 잠재적 비용을 제3자에게 이전하거나 할당
- **방법**:
    - 보험 가입
    - 아웃소싱
    - 클라우드 서비스 이용
- **예시**:
    - 사이버 보험
    - 보안 관제 외주
    - 데이터센터 임대

<br>

### 12.2 위험 분석 방법
---
#### 정량적 분석 (Quantitative Analysis)
- **특징**:
    - 객관적, 수치화
    - 금액으로 표현
    - 계산 가능
- **지표**:
    - ALE (Annual Loss Expectancy): 연간 예상 손실액
    - SLE (Single Loss Expectancy): 단일 사고 예상 손실액
    - ARO (Annual Rate of Occurrence): 연간 발생 빈도
    - 공식: ALE = SLE × ARO
- **장점**: 객관적, 비교 용이, 비용 대비 효과 분석 가능
- **단점**: 측정 어려움, 시간/비용 소요

#### 정성적 분석 (Qualitative Analysis)
- **특징**:
    - 주관적, 서술적
    - 등급/순위로 표현
    - 경험 기반
- **방법**:
    - 위험 매트릭스
    - 델파이 기법
    - 전문가 판단
- **등급**: 상/중/하, 높음/중간/낮음
- **장점**: 신속, 비용 절감, 이해 용이
- **단점**: 주관적, 일관성 부족

<br>

## 13. 재해복구 (Disaster Recovery)
---
### 13.1 백업 사이트 유형
---
#### 1. Mirror Site (미러 사이트)
- **구성**: Active-Active
- **특징**:
    - 실시간 동기화
    - 완전 이중화
    - 즉시 전환 가능
- **복구 시간**: 거의 0 (RTO ≈ 0)
- **구축 비용**: 가장 높음
- **적용**: 금융, 국방 등 중요 시스템

#### 2. Hot Site (핫 사이트)
- **구성**: Active-Standby
- **특징**:
    - 완전한 장비 구축
    - 주기적 백업
    - 신속한 전환 가능 (수 시간 이내)
- **복구 시간**: 수 시간
- **구축 비용**: 높음
- **적용**: 핵심 업무 시스템

#### 3. Warm Site (웜 사이트)
- **구성**: 부분적 장비 구축
- **특징**:
    - 기본 인프라만 구축
    - 일부 데이터 백업
    - 추가 장비 설치 필요
- **복구 시간**: 수일
- **구축 비용**: 중간
- **적용**: 일반 업무 시스템

#### 4. Cold Site (콜드 사이트)
- **구성**: 최소 시설만 확보
- **특징**:
    - 공간과 기본 설비만
    - 장비 미구축
    - 복구에 상당한 시간 필요
- **복구 시간**: 수 주 이상
- **구축 비용**: 가장 낮음
- **적용**: 비핵심 시스템

<br>

### 13.2 백업 사이트 비교
---

|   순서   | 구축 난이도 | 재해복구 시간 | 구축 비용  |
| :----: | :----: | :-----: | :----: |
| 1 (최고) | Mirror | Mirror  | Mirror |
|   2    |  Hot   |   Hot   |  Hot   |
|   3    |  Warm  |  Warm   |  Warm  |
| 4 (최저) |  Cold  |  Cold   |  Cold  |

<br>

## 14. 정보보안 인증제도
---
### 14.1 물리적 측면 (제품 인증)
---
#### 보안 제품 인증
- VPN, 방화벽, IDS/IPS 등

#### 평가 기준

##### TCSEC (Trusted Computer System Evaluation Criteria)
- **국가**: 미국
- **별칭**: Orange Book
- **등급**: D → C1 → C2 → B1 → B2 → B3 → A1
- **특징**: 기밀성 중심

##### ITSEC (Information Technology Security Evaluation Criteria)
- **국가**: 유럽 (영국, 독일, 프랑스, 네덜란드)
- **등급**: E0 → E1 → ... → E6
- **특징**: 기밀성 + 무결성 + 가용성

##### CC (Common Criteria)
- **적용**: 전 세계 (국제 표준)
- **등급**: EAL1 → EAL2 → ... → EAL7
- **특징**:
    - TCSEC, ITSEC 통합
    - ISO/IEC 15408
    - 상호 인정 협정 (CCRA)
- **구성 요소**:
    - TOE (Target of Evaluation): 평가 대상
    - PP (Protection Profile): 보안 요구사항
    - ST (Security Target): 보안 목표 명세서

<br>

### 14.2 관리적 측면 (조직 인증)
---
#### BS 7799
- **국가**: 영국
- **구성**:
    - **Part 1**: 실행 지침 → ISO/IEC 17799 → **ISO/IEC 27002**
    - **Part 2**: 보안 요구사항 → **ISO/IEC 27001**

#### ISO 27000 시리즈
- **ISO 27000**: 개요 및 용어
- **ISO 27001**: 정보보호 관리체계 요구사항 (인증 가능)
- **ISO 27002**: 정보보호 통제 실행 지침 (가이드)
- **ISO 27003**: 구현 지침
- **ISO 27004**: 측정 및 평가
- **ISO 27005**: 위험 관리
- **ISO 27701**: 개인정보 관리
- **ISO 24014**: IT 거버넌스

#### ISMS-P (정보보호 및 개인정보보호 관리체계)
- **국가**: 대한민국
- **인증 기관**: KISA (한국인터넷진흥원)
- **법적 근거**: 정보통신망법, 개인정보보호법
- **구성**:
    - ISMS: 정보보호 관리체계
    - PIMS: 개인정보보호 관리체계
    - ISMS-P: ISMS + PIMS 통합
- **인증 대상**:
    - 정보통신서비스 제공자
    - 연간 매출 1,500억 이상
    - 일평균 이용자 100만명 이상
    - 정보통신망 보유/운영자

<br>

## 15. 추가 핵심 개념
---
### 15.1 포트 번호 (Well-Known Ports)
---

|      서비스      |   포트    |  프로토콜   | 설명             |
| :-----------: | :-----: | :-----: | :------------- |
|  FTP (Data)   |   20    |   TCP   | 파일 전송 데이터      |
| FTP (Control) |   21    |   TCP   | 파일 전송 제어       |
|      SSH      |   22    |   TCP   | 보안 원격 접속       |
|    Telnet     |   23    |   TCP   | 원격 접속          |
|     SMTP      |   25    |   TCP   | 메일 전송          |
|      DNS      |   53    | TCP/UDP | 도메인 네임 서비스     |
| DHCP (Server) |   67    |   UDP   | 동적 IP 할당 서버    |
| DHCP (Client) |   68    |   UDP   | 동적 IP 할당 클라이언트 |
|     TFTP      |   69    |   UDP   | 간단한 파일 전송      |
|     HTTP      |   80    |   TCP   | 웹 서비스          |
|     POP3      |   110   |   TCP   | 메일 수신          |
|     IMAP      |   143   |   TCP   | 메일 수신 (서버 저장)  |
|     SNMP      |   161   |   UDP   | 네트워크 관리        |
|     HTTPS     |   443   |   TCP   | 보안 웹 서비스       |
|     SMTPS     | 465/587 |   TCP   | 보안 메일 전송       |
|      RDP      |  3389   |   TCP   | 원격 데스크톱        |

<br>

### 15.2 AAA (Authentication, Authorization, Accounting)
---
#### Authentication (인증)
- 사용자 신원 확인
- Who are you?

#### Authorization (인가)
- 권한 부여
- What can you do?

#### Accounting (과금/회계)
- 사용 내역 기록
- What did you do?
- 로그, 감사 추적

<br>

### 15.3 방화벽 유형
---
#### 패킷 필터링 방화벽
- L3, L4 정보 기반
- 빠르지만 기능 제한적

#### 상태 기반 (Stateful) 방화벽
- 연결 상태 추적
- 동적 규칙 적용

#### 애플리케이션 게이트웨이 (프록시 방화벽)
- L7 검사
- 철저하지만 느림

#### 차세대 방화벽 (NGFW)
- 통합 보안 기능
- IPS, 안티바이러스, 애플리케이션 제어

<br>

### 15.4 IDS vs IPS
---

| 구분  | IDS                        | IPS                         |
| :-: | :------------------------- | :-------------------------- |
| 이름  | Intrusion Detection System | Intrusion Prevention System |
| 역할  | 탐지 및 경보                    | 탐지 및 차단                     |
| 위치  | Out-of-band (복사 트래픽)       | In-line (실제 트래픽)            |
| 대응  | 수동적                        | 능동적                         |
| 장점  | 오탐 영향 적음                   | 즉각 대응                       |
| 단점  | 실시간 차단 불가                  | 오탐 시 서비스 영향                 |

<br>

### 15.5 DES vs AES
---

|  구분   | DES                      | AES                          |
| :---: | :----------------------- | :--------------------------- |
|  이름   | Data Encryption Standard | Advanced Encryption Standard |
| 블록 크기 | 64비트                     | 128비트                        |
| 키 길이  | 56비트                     | 128/192/256비트                |
| 라운드 수 | 16                       | 10/12/14 (키 길이에 따라)          |
|  보안성  | 취약 (무차별 대입 가능)           | 안전                           |
|  사용   | 레거시 시스템                  | 현재 표준                        |

<br>

### 15.6 디지털 서명 과정
---
#### 서명 생성 (송신자)
1. 메시지를 해시 함수로 해시값 생성
2. 해시값을 송신자의 개인키로 암호화 → 디지털 서명
3. 원본 메시지 + 디지털 서명 전송

#### 서명 검증 (수신자)
1. 디지털 서명을 송신자의 공개키로 복호화 → 해시값1
2. 원본 메시지를 해시 함수로 해시값 생성 → 해시값2
3. 해시값1 == 해시값2 비교 → 무결성 및 인증 확인

<br>

### 15.7 대칭키 배송 문제 해결 방법
---
1. **키 분배 센터 (KDC)**: 신뢰할 수 있는 제3자가 키 분배
2. **Diffie-Hellman**: 공개된 채널에서 키 교환
3. **공개키 암호화**: 대칭키를 공개키로 암호화하여 전송
4. **물리적 전달**: 오프라인으로 키 전달

<br>

## Related Posts
---
- [[YouTube] "조현준 보안스쿨 - 기초강의" Review](https://bangjeongbin.github.io/TIL-Blog/posts/review-youtube-cho-hyun-joon-security-school-basic-course)
- [[YouTube] "조현준 보안스쿨 - 기초강의" Note-Taking [1]](https://bangjeongbin.github.io/TIL-Blog/posts/note-taking-youtube-cho-hyun-joon-security-school-basic-course-1)
- [[YouTube] "조현준 보안스쿨 - 기초강의" Note-Taking [2]](https://bangjeongbin.github.io/TIL-Blog/posts/note-taking-youtube-cho-hyun-joon-security-school-basic-course-2)
- [[YouTube] "조현준 보안스쿨 - 기초강의" Note-Taking [3]](https://bangjeongbin.github.io/TIL-Blog/posts/note-taking-youtube-cho-hyun-joon-security-school-basic-course-3)

<br>

## References
---
- [조현준 보안스쿨 - 기초강의](https://www.youtube.com/playlist?list=PLaR0eJQDBqV-NeNVmyIuC9Snb9hotoAhu)
