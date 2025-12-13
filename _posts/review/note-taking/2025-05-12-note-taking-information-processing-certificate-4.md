---
title: "정보처리기사 Note-Taking [4]"
description: 정보처리기사 요약 노트 정리 4편
author: bin
date: 2025-05-12 09:00:00 +0800
categories: [Review, Note-Taking]
tags: [Network, CS]
pin: true
math: true
mermaid: true
image:
 path: https://bangjeongbin.github.io/TIL-Blog/assets/img/posts/common/note-taking-logo.png
 alt: Note Taking
---

> 해당 포스트는 학습 목적으로 작성되었으며 <<[2025 시나공 정보처리기사 실기 기본서](https://product.kyobobook.co.kr/detail/S000215623877)>>을 참고하여 작성하였음을 알려드립니다.

<br>

# 5장 - 인터페이스 구현
---

## 076 인터페이스 요구사항 검증
---
### 요구사항 검증 방법

|                        |                                                                             |
| :--------------------: | --------------------------------------------------------------------------- |
| 동료검토<br>(Peer Review)  | 요구사항 명세서를 작성자가 명세서 내용을 직접 설명하고 동료들이 이를 들으면서 결함을 발견하는 형태의 검토 방법              |
| 워크스루<br>(Work Through) | 검토 회의 전에 <u>요구사항 명세서를 미리 배포하여 사전 검토한 후에</u> 짧은 검토 회의를 통해 결함을 발견하는 형태의 검토 방법 |
|  인스펙션<br>(Inspection)  | 요구사항 명세서 작성자를 제외한 <u>다른 검토 전문가들이 요구사랑 명세서를 확인</u>하면서 결함을 발견하는 형태의 검토 방법     |

---

<br>

## 080 모듈 연계를 위한 인터페이스 기능 식별
---
### 모듈 연계

- 내부 모듈과 외부 모듈 또는 내부 모듈 간 데이터의 교환을 위해 관계를 설정하는 것

- 대표적인 모듈 연계 방법
	- EAI(Enterprise Application Integration)
	- ESB(Enterprise Service Bus)
	- 웹 서비스(Web Service)

---
### EAI(Enterprise Application Integration)

- EAI의 구축 유형

|                유형                | 기능                                                                                                                                                    |                                              모형                                              |
| :------------------------------: | ----------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------: |
| Point-to-Point<br>/ Peer-to-Peer | - 가장 기본적인 애플리케이션 통합 방식<br>- 애플리케이션을 1 : 1 로 연결함<br>- 변경 및 재사용이 어려움                                                                                    | ![point-to-point](https://lh3.googleusercontent.com/d/1V7i6e5cnwCEQL6OoPVpLHjarRcvuTex5)[^1] |
|           Hub & Spoke            | - 단일 접점인 허브 시스템을 통해 데이터를 전송하는 중앙 집중형 방식<br>- 확장 및 유지 보수가 용이함<br>- 허브 장애 발생 시 시스템 전체에 영향을 미침                                                           |  ![hub-n-spoke](https://lh3.googleusercontent.com/d/1ZBJ7Qr60h9aBcHxcYC-AfsMx_CvFphQS)[^1]   |
|     Message Bus<br>(ESB 방식)      | - 애플리케이션 사이에 미들웨어를 두어 처리하는 방식<br>- 확장성이 뛰어나며 대용량 처리가 가능함                                                                                              |  ![message-bus](https://lh3.googleusercontent.com/d/1e-w94WD508eM84T0D6vcDDaj8MbnfmdE)[^1]   |
|              Hybrid              | - Hub & Spoke와 Message Bus의 혼합 방식<br>- 그룹 내에서는 Hub & Spoke방식을, 그룹 간에는 Message Bus 방식을 사용함<br>- 필요한 경우 한 가지 방식으로 EAI 구현이 가능함<br>- 데이터 병목 현상을 최소화할 수 있음 |     ![hybrid](https://lh3.googleusercontent.com/d/1tWwCRJX1DrLhCylYOrLbh_t4HkGhaQ84)[^1]     |

---
### ESB(Enterprise Service Bus)

- 애플리케이션 간 표준 기반의 인터페이스를 제공하는 솔루션이다.
- 특정 서비스에 국한되지 않고 범용적으로 사용하기 위하여 애플리케이션의 결합도(Coupling)을 약하게 유지

---

<br>

## 084 인터페이스 보안
---
### 인터페이스 보안

- IPsec(IP Security)
	- 네트워크 계층에서 IP 패킷 단위의 데이터 변조 방지 및 은닉 기능을 제공하는 프로토콜
	- 암호화 수행 시 암호화와 복호화가 모두 가능한 양방향 암호화 방식을 사용

- SSL(Secure Sockets Layer)
	- TCP / IP 계층과 애플리케이션 계층 사이에서 인증, 암호화, 무결성을 보장하는 프로토콜

- S-HTTP(Secure Hypertext Transfer Protocol)
	- 클라이언트와 서버 간에 전송되는 모든 메세지를 암호화 하는 프로토콜

---

<br>

# 6장 - 화면 설계
---

## 086 사용자 인터페이스
---
### 사용자 인터페이스의 구분

|              구분               | 내용                                         |
| :---------------------------: | ------------------------------------------ |
|  CLI(Command Line Interface)  | 명령과 출력이 텍스트 형태로 이루어지는 인터페이스                |
| GUI(Graphical User Interface) | 아이콘이나 메뉴를 마우스로 선택하여 작업을 수행하는 그래픽 환경의 인터페이스 |
|  NUI(Natural User Interface)  | 사용자의 말이나 행동 등 자연스러운 움직임을 통해 기기를 조작하는 인터페이스 |

---
### 사용자 인터페이스의 기본 원칙

- <span style="color:red">중요</span>

| 원칙  | 내용                              |
| :-: | ------------------------------- |
| 직관성 | 누구나 쉽게 이해하고 사용할 수 있어야 함         |
| 유효성 | 사용자의 목적을 정확하고 완벽하게 달성해야 함       |
| 학습성 | 누구나 쉽게 배우고 익힐 수 있어야 함           |
| 유연성 | 사용자의 요구사항을 최대한 수용하고 실수를 최소화해야 함 |

---

<br>

# 7장 - 애플리케이션 테스트 관리
---

## 091 애플리케이션 테스트
---
### 애플리케이션 테스트

- 애플리케이션 테스트는 개발된 소프트웨어가 고객의 요구사항을 만족시키는지 **확인(Validation)** 하고 소프트웨어가 기능을 정확히 수행하는지 **검증(Verification)** 한다.

---
### 애플리케이션 테스트 기본 원리

- <span style="color:red">중요</span>

|                기본 원리                 | 설명                                                                                      |
| :----------------------------------: | --------------------------------------------------------------------------------------- |
|             완벽한 테스트 불가능              | 소프트웨어의 잠재적인 결함을 줄일 수 있지만 소프트웨어에 결함이 없다고 증명할 수는 없음                                       |
|      파레토 법칙(Pareto  Principle)       | 애플리케이션의 20%에 해당하는 코드에서 전체 결함의 80%가 발견된다는 법칙                                             |
|     살충제 패러독스(Pesticide Paradox)      | 동일한 테스트 케이스로 동일한 테스트를 반복하면 더 이상 결함이 발견되지 않는 현상                                          |
|         테스팅은 정황(Context) 의존          | 소프트웨어의 특징, 테스트 환경, 테스터의 역량 등 정황(Context)에 따라 테스트 결과가 달라질 수 있으므로, 정황에 따라 테스트를 다르게 수행해야 함 |
| 오류-부재의 궤변(Absence of Errors Fallacy) | 소프트웨어 결함을 모두 제거해도 사용자의 요구사항을 만족시키지 못하면 해당 소프트웨어는 품질이 높다고 말할 수 없는 것                      |
|             테스트와 위험은 반비례             | 테스트를 많이 하면 할 수록 미래에 발생할 위험을 줄일 수 있음                                                     |
|             테스트의 점진적 확대              | 테스트는 작은 부분에서 시작하여 점점 확대하며 진행해야 함                                                        |
|             테스트의 별도 팀 수행             | 테스트는 개발자와 관계없는 별도의 팀애서 수행해야 함                                                           |

---

<br>

## 092 애플리케이션 테스트의 분류
---
### 프로그램 실행 여부에 따른 테스트

| 테스트 종류 | 설명                                                                                              |
| :----: | ----------------------------------------------------------------------------------------------- |
| 정적 테스트 | - 종류 : **워크쓰루**, **인스펙션**, **코드 검사** 등<br>- 소스코드에 대한 코딩 표준, 코딩 스타일, 코드 복잡도, 남은 결함 등을 발견하기 위해 사용 |
| 동적 테스트 | - 종류 : **블랙박스 테스트**, **화이트박스 테스트**<br>- 소프트웨어 개발의 모든 단계에서 테스트를 수행함                              |

---
### 시각에 따른 테스트

|          테스트 종류          | 설명                                                                                      |
| :----------------------: | --------------------------------------------------------------------------------------- |
| 검증 테스트<br>(Verification) | - <u>개발자의 시각에서</u> 제품의 생산과정을 테스트하는 것<br>- 제품이 명세서대로 완성됐는지 테스트함                          |
|  확인 테스트<br>(Validation)  | - <u>사용자의 시각에서</u> 생산된 제품의 결과를 테스트하는 것<br>- 사용자가 요구한대로 제품이 완성됐는지, 제품이 정상적으로 동작하는지를 테스트함 |

---
### 목적에 따른 테스트

- <span style="color:red">중요</span>

|         테스트 종류          | 설명                                                                           |
| :---------------------: | ---------------------------------------------------------------------------- |
|  회복 테스트<br>(Recovery)   | 시스템에 여러 가지 결함을 주어 <u>실패하도록 한 후 올바르게 복구되는지를 확인</u> 하는 테스트                     |
|  안전 테스트<br>(Security)   | 시스템에 설치된 <u>시스템 보호 도구가 불법적인 침입으로부터 시스템을 보호할 수 있는지</u>를 확인하는 테스트              |
|   강도 테스트<br>(Stress)    | 시스템에 과도한 정보량이나 빈도 등을 부과하여 <u>과부하 시에도 소프트웨어가 정상적으로 실행되는지 확인</u> 하는 테스트        |
| 성능 테스트<br>(Performance) | 소프트웨어의 <u>실시간 성능이나 전체적인 효율성을 진단하는 테스트</u> 로, <u>소프트웨어의 응답 시간, 처리량</u> 등을 테스트 |
|  구조 테스트<br>(Structure)  | 소프트웨어 <u>내부의 논리적인 경로, 소스 코드의 복잡도 등을 평가</u> 하는 테스트                            |
| 회귀 테스트<br>(Regression)  | 소프트웨어의 <u>변경 또는 수정된 코드에 새로운 결함이 없음을 확인하는 테스트</u>                             |
|  병행 테스트<br>(Parallel)   | <u>변경된 소프트웨어와 기본 소프트웨어에</u> 동일한 데이터를 입력하여 결과를 비교하는 테스트                       |

---

<br>

## 093 테스트 기법에 따른 애플리케이션 테스트
---
### 화이트박스 테스트(White Box Test)

- 원시 코드의 논리적인 모든 경로를 테스트하여 테스트 케이스를 설계히는 방법

---
### 화이트박스 테스트의 종류

- <span style="color:red">중요</span>

|               테스트 종류                | 설명                                                                                       |
| :---------------------------------: | ---------------------------------------------------------------------------------------- |
|     기초 경로 검사(Base Path Testing)     | - 대표적인 화이트박스 테스트 기법                                                                      |
| 제어 구조 검사(Control Structure Testing) | 1. 조건 검사(Condition Testing)<br>2. 루프 검사(Loop Testing)<br>3. 데이터 흐름 검사(Data Flow Testing) |

---
### 화이트박스 테스트의 검증 기준

- <span style="color:red">중요</span>

|                       테스트 종류                        | 설명                                                                                   |
| :-------------------------------------------------: | ------------------------------------------------------------------------------------ |
|             문장 커버리지(Statement Coverage)             | 소스 코드의 <u>모든 구문이 한 번 이상 수행되도록</u> 테스트 케이스를 설계                                        |
|             결정 커버리지(Decision Coverage)              | 소스 코드의 <u>**모든 조건문**에 대해 조건식의 결과가 True인 경우와 False인 경우를 한 번 이상 수행되도록</u> 테스트 케이스를 설계  |
|             조건 커버리지(Condition Coverage)             | 소스 코드의 조건문에 포함된 <u>**개별 조건식**의 결과가 True인 경우와 False인 경우가 한 번 이상 수행되도록</u> 테스트 케이스를 설계 |
|       조건/결정 커버리지(Condition/Decision Coverage)       | <u>조건문이 True인 경우와 False인 경우에 따라 조건 커버리지의 입력 데이터를 구분</u>하는 테스트 케이스를 설계                |
| 변경 조건/결정 커버리지(Modified Condition/Decision Coverage) | <u>개별 조건식이 다른 개별 조건식의 영향을 받지 않고 전체 조건식의 결과에 독립적으로 영향</u>을 주도록 테스트 케이스를 설계            |
|       다중 조건 커버리지(Multiple Condition Coverage)       | 소스 코드의 조건문에 포함된 <u>모든 개별 조건식의 모든 조합을 고려</u>하도록 테스트 케이스를 설계                           |

---
### 블랙박스 테스트(Black Box Test)

- 각 기능이 완전히 작용되는 것을 입증하는 테스트, 기능 테스트라고도 한다.

---
### 블랙박스 테스트의 종류

- <span style="color:red">중요</span>

|                        테스트 종류                         | 설명                                                                                     |
| :---------------------------------------------------: | -------------------------------------------------------------------------------------- |
| 동치 분할 검사(Equivalence Partitioning Testring, 동등 분할 기법) | 입력 조건에 타당한 입력자료와 타당하지 않은 입력자료의 개수를 균등하게 하여 테스트 케이스를 정하고, 해당 입력자료에 맞는 결과가 출력되는지 확인하는 기법 |
|            경계값 분석(Boundary Value Analysis)            | 입력 조건의 중간값보다 경계값에서 오류가 발생될 확률이 높다는 점을 이용하여 입력 조건의 경계값을 테스트 케이스로 선정하여 검사하는 기법           |
|      원인-효과 그래프 검사(Cause-Effect Graphing Testing)      | 입력 데이터 간의 관계와 출력에 영향을 미치는 상황을 체계적으로 분석한 다음 효용성이 높은 테스트 케이스를 선정하여 검사하는 기법               |
|               오류 예측 검사(Error Guessing)                | 과거의 경험이나 확인자의 감각으로 테스트하는 기법                                                            |
|               비교 검사(Comparison Testing)               | 여러 버전의 프로그램에 동일한 테스트 자료를 제공하여 동일한 결과가 출력되는지 테스트하는 기법                                   |

---

<br>

## 094 개발 단계에 따른 애플리케이션 테스트
---
### 개발 단계에 따른 애플리케이션 테스트

- <span style="color:red">소프트웨어 생명 주기의 V-모델</span>

![application-test-v-model](https://lh3.googleusercontent.com/d/101BFMf06hnPDwGI454mL4na2spJ6xIDf)
[^2]

---
### 단위 테스트(Unit Test)

- 모듈이나 컴포넌트에 초점을 맞춰 테스트

---
### 통합 테스트(Integration Test)

- 단위 테스트가 완료된 모듈들을 결합하여 하나의 시스템으로 완성시키는 과정에서의 테스트

---
### 시스템 테스트(System Test)

- 개발된 소프트웨어가 완벽하게 수행되는가를 점검하는 테스트
- 기능적 요구사항과 비기능적 요구사항을 구분하여 각각을 만족하는지 테스트

---
### 인수 테스트(Acceptance Test)

- 사용자의 요구사항을 충족하는지 중점을 두고 테스트

| 테스트 종류 | 설명                                                                                 |
| :----: | ---------------------------------------------------------------------------------- |
| 알파 테스트 | - <u>개발자의 장소에서 사용자가 개발자 앞에서</u> 행해지는 테스트<br>- <u>통제된 환경에서 진행</u>, 개발자와 함께 확인하면서 기록 |
| 베타 테스트 | - 여러 명의 사용자 앞에서 행하는 테스트 기법<br>- 실업무를 가지고 <u>사용자가 직접 테스트</u>                        |

---

<br>

## 095 통합 테스트
---
### 통합 테스트

- 비점진적 통합 방식
	- 빅뱅 통합 테스트 방식

- 점진적 통합 방식
	- 하향식 통합 테스트
	- 상향식 통합 테스트
	- 혼합식 통합 테스트

---
### 하향식 통합 테스트(Top Down Integration Test)

- `상위 모듈` -> `하위 모듈` 방향으로 통합하면서 테스트 
- 깊이 우선 통합법, 넓이 우선 통합법 사용
- <span style="color:red">스텁(Stub)</span> 사용

---
### 상향식 통합 테스트(Bottom Up Integration Test)

- `하위 모듈` -> `상위 모듈` 방향으로 통합하면서 테스트
- 하위 모듈들을 클러스터(Cluster)로 결합
- <span style="color:red">드라이버(Driver)</span> 사용

---
### 회귀 테스팅(Refression Testing)

- **통합 테스트로 인하여** 변경된 모듈이나 컴포넌트에 새로운 오류가 있는지 확인하는 테스트

---

<br>

## 099 애플리케이션 성능 분석
---
### 애플리케이션 성능

- 최소한의 자원을 사용하여 최대한 많은 기능을 신속하게 처리하는 정도

- 애플리케이션 성능 측정 지표

|          측정 지표          | 설명                                                           |
| :---------------------: | ------------------------------------------------------------ |
|     처리량(Throughput)     | 일정 시간 내에 애플리케이션이 처리하는 일의 양                                   |
|  응답 시간(Response Time)   | 애플리케이션애 요청을 전달한 시간부터 응답이 도착할 때까지 걸린 시간                       |
| 경과 시간(Turn Around Time) | 애플리케이션에 작업을 의뢰한 시간부터 처리가 완료될 때까지 걸린 시간                       |
| 자원 사용률(Resource Usage)  | 애플리케이션이 의뢰한 작업을 처리하는 동안의 CPU 사용량, 메모리 사용량, 네트워크 사용량 등 자원 사용률 |

---

<br>

## 100 복잡도
---
### 빅오 표기법으로 표현한 최악의 알고리즘 시간 복잡도

|   최악 시간 복잡도   | 알고리즘                                                                               |
| :-----------: | ---------------------------------------------------------------------------------- |
|     O(1)      | 스택의 삽입(Push), 삭제(Pop)                                                              |
| $O(\log_2n)$  | 이진트리(BinaryTree), 이진 검색(Binary Search)                                             |
|     O(n)      | for 문                                                                              |
| $O(n\log_2n)$ | 힙 정렬(Heap Sort), 2-Way 합병 정렬(Merge Sort)                                           |
|   $O(n^2)$    | 삽입 정렬(Insertion Sort), 쉘 정렬(Shell Sort), 선택 정렬(Selection Sort), 버블 정렬(Bubble Sort) |
|   $O(2^n)$    | 피보나치 수열(Fibonacci Sequence)                                                        |

---

<br>

## 101 애플리케이션 성능 개선
---
### 소스 코드 품질 분석 도구

|           분석 도구            | 도구 종류                                                |
| :------------------------: | ---------------------------------------------------- |
| 정적 분석 도구(Static Analysis)  | pmd, cppcheck, SonarQube, checkstyle, com, cobertura |
| 동적 분석 도구(Dynamic Analysis) | Avalanche, Valgrind                                  |

---

<br>

# 8장 - SQL 응용
---

## 102 SQL - DDL
---
### DDL(Data Define Language, 데이터 정의어)

- <span style="color:red">CREATE, ALTER, DROP</span>

---
### CREATE SCHEMA

> CREATE SCHEMA `스키마명` AUTHORIZATION `사용자_id`;

---
### CREATE DOMAIN

> CREATEDOMAIN `도메인명` [AS] <br>
> 데이터_타입 [DEFAULT `기본값`] <br>
> [CONSTRAINT `제약조건명` CHECK(`범위값`)];
> 
> [] : 생략가능

---
### CREATE TABLE

> CREATE TABLE `테이블명` ( <br>
> 	`속성명` 데이터_타입 [DEFAULT `기본값`] [NOT NULL], <br>
> 	[PRIMARY KEY(`기본키_속성명`))] <br>
> 	[UNIQUE(`대체키_속성명`))] <br>
> 	[FOREIGN KEY(`외래키_속성명`))] <br>
> 		REFERENCES `참조테이블`(`기본키_속성명`) <br>
> 		[ON DELETE 옵션] <br>
> 		[ON UPDATE 옵션] <br>
> 	[CONSTRANINT `제약조건명`] [CHECK (`조건식`)]);
> 	
> [] : 생략가능

---
### CREATE VIEW

> CREATE VIEW `뷰명`[(`속성명`[, `속성명, ,,,`])]
> AS SELECT문;
> 
> [] : 생략가능

---
### CREATE INDEX

> CREATE [UNIQUE] INDEX `인덱스명` <br>
> ON `테이블명` <br>
> [CLUSTER];
> 
> [] : 생략가능

---
### ALTER TABLE

> ALTER TABLE `테이블명` ADD `속성명` 데이터_타입 [DEFAULT `'기본값'`]; <br>
> ALTER TABLE `테이블명` ALTER `속성명` 데이터_타입 [DEFAULT `'기본값'`]; <br>
> ALTER TABLE `테이블명` DROP COLUME `속성명` [CASCADE]; <br>
> 
> [] : 생략가능

---

<br>

## 103 SQL - DCL
---
### GRANT / REVOKE

> GRANT `권한_리스트` ON `테이블명` TO `사용자` [WITH GRANT OPTION]; <br>
> REVOKE [GRANT OPTION FOR] `권힌_리스트` TO `테이블명` FROM `사용자` [CASCADE]; <br>
 > 
> [] : 생략가능

---

<br>

## 106 DML - SELECT-2
---
### 집합 연산자를 이용한 통합 질의

|  집합 연산자   | 설명                                                     | 집합 종류 |
| :-------: | ------------------------------------------------------ | :---: |
|   UNION   | - 두 SELECT문의 조회 결과를 통합하여 모두 출력<br>- 중복제거               |  합집합  |
| UNION ALL | - 〃<br>- 중복제거 안함                                       |  합집합  |
| INTERSECT | - 두 SELECT문의 조회 결과 중 공통된 행만 출력                         |  교집합  |
|  EXCEPT   | - 첫 번째 SELECT문의 조회 결과에서 두 번째 SELECT문의 조회 결과를 제외한 행을 출력 |  차집합  |

![application-test-v-model](https://lh3.googleusercontent.com/d/1FmgBA0NAK_yP_uOta5Z6HyIf9OK7zYiy)
[^3]

---

<br>

## 107 DML - JOIN
---
### JOIN

![sql-join](https://lh3.googleusercontent.com/d/1_E5laxbJ6oYmZyNk9ZM6SIJFHuVd-nFx)
[^4]

---

<br>

# 11장 - 응용 SW 기초 기술 활용
---

## 140 OSI 참조 모델
---
### OSI(Open System Interconnection) 참조 모델

- 하위 계층
	1. 물리 계층(Physical Layer)
	2. 데이터링크 계층(Data Link Layer)
	3. 네트워크 계층(Network Layer, 망 계층)

- 상위 계층
	4. 전송 계층(Transport Layer)
	5. 세션 계층(Session Layer)
	6. 표현 계층(Presentation Layer)
	7. 응용 계층(Application Layer)

---
### 1. 물리 계층(Physical Layer)

- 두 장치 간의 <u>실제 접속과 절단 등 기계적, 전기적, 기능적, 절차적 특성</u>에 대한 규칙을 정의
- 관련 장비 : **리피터**, **허브**

---
### 2. 데이터링크 계층(Data Link Layer)

- 두 개의 인접한 개발 시스템들 간에 <u>신뢰성 있고 효율적인 정보 전송을 할 수 있도록 시스템 간 연결 설정과 유지 및 종료를 담당</u>
- 송, 수신 측 속도 차이 해결을 위해 <u>흐름 제어 기능</u>을 한다.
- 프레임의 시작과 끝을 구분하기 위한 <u>프레임의 동기화 기능</u>을 한다.
- 오류의 검출과 회복을 위한 <u>오류 제어 기능</u>을 한다.
- 프레임의 순서적 전송을 위한 <u>순서 제어 기능</u>을 한다.
- 관련 장비 : **랜카드**, **브리지**, **스위치**

---
### 3. 네트워크 계층(Network Layer, 망 계층)

- 개발 시스템들 간의 <u>네트워크 연결을 관리하는 기능과 데이터의 교환 및 중계</u> 기능
- <u>경로 설정(Routing)</u>, 데이터 교환 및 중계, 트래픽 제어. 패킷 정보 전송 등 수행
- <u>IP</u>
- 관련 장비 : **라우터**

---
### 4. 전송 계층(Transport Layer)

- 논리적인 안정과 균일한 데이터 전송 서비스를 제공함으로써 <u>종단 시스템(End-to-End) 간의 데이터 전송</u>
- <u>주소 설정, 다중화(분할 및 재조립)</u>
- <u>TCP, UDP</u>
- 관련 장비 : **게이트웨이**

---
### 5. 세션 계층(Session Layer)

- <u>송 / 수신 측 간의 관련성을 유지하고 대화 제어를 담당</u>
- <u>대화(회화) 구성 및 동기 제어, 토큰 사용</u>

---
### 6. 표현 계층(Presentation Layer)

- 서로 다른 데이터 표현 형태를 갖는 시스템 간의 상호 접속을 위해 필요한 계층
- <u>코드 변환, 데이터 암호화, 데이터 압축, 구문 검색, 정보 형식(포맷) 변환, 문맥관리</u>

---
### 7. 응용 계층(Application Layer)

- 응용 프로세스 간의 정보 교환, 전자 사서함, 파일 전송, 가상 터미널 등의 서비스 제공

---

<br>

## Related Posts
---
- [정보처리기사 Note-Taking [1]](https://bangjeongbin.github.io/TIL-Blog/posts/note-taking-information-processing-certificate-1)
- [정보처리기사 Note-Taking [2]](https://bangjeongbin.github.io/TIL-Blog/posts/note-taking-information-processing-certificate-2)
- [정보처리기사 Note-Taking [3]](https://bangjeongbin.github.io/TIL-Blog/posts/note-taking-information-processing-certificate-3)

<br>

## References
---
[^1]: 출처 : https://velog.io/@do_ng_iill/EAIEnterprise-Application-Integration-%EC%A0%95%EB%A6%AC
[^2]: 출처 : https://notedailyit.co.kr/2023-%EC%A0%95%EB%B3%B4%EC%B2%98%EB%A6%AC%EA%B8%B0%EC%82%AC-2%EA%B3%BC%EB%AA%A9-9-%EC%96%B4%ED%94%8C%EB%A6%AC%EC%BC%80%EC%9D%B4%EC%85%98-%ED%85%8C%EC%8A%A4%ED%8A%B8-v-%EB%AA%A8%EB%8D%B8/
[^3]: 출처 : https://cmelcmel.tistory.com/56
[^4]: 출처 : https://velog.io/@golmori/working-with-sets
