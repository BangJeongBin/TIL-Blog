---
title: "[Windows] 윈도우의 레지스트리란?
description: 윈도우 레지스트리(Registry) 구조 및 핵심 개념 정리
author: bin
date: 2026-02-26 09:00:00 +0800
categories: [TIL, OS, Windows]
tags: [OS, Windows, Registry]
pin: false
math: true
mermaid: true
image:
 path: https://bangjeongbin.github.io/TIL-Blog/assets/img/posts/common/til-logo.png
 alt: Today I Learnd
---

![windows-regedit](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdna%2Fp3sK4%2Fbtsv8y0brFM%2FAAAAAAAAAAAAAAAAAAAAAFnlbZ0xW0tp00Wa65iv6E0TI56dKOqaO6WqAMU8nk9F%2Fimg.png%3Fcredential%3DyqXZFxpELC7KVnFOS48ylbz2pIh7yKj8%26expires%3D1790780399%26allow_ip%3D%26allow_referer%3D%26signature%3D%252Fiaisjn%252Bz%252FM9XpDmrite4AgG4nQ%253D)
_Windows의 레지스트리 편집기 (regedit.exe)[^1]_


## 𝙸. 레지스트리(Registry)란?
---
 "레지스트리(Registry)"는 운영체제, 설치된 프로그램, 사용자 계정마다의 설정 값을 담아두는 중앙 저장소이다.(리눅스는 파일 시스템의 형태로 구현되어 있다.) 예전 윈도우(3.1 이전)에서는 각 프로그램이 개별 INI 파일로 설정을 관리했는데, 이를 하나의 통합된 <mark>중앙 집중형 데이터베이스</mark>로 관리하기 위해 등장한 것이 레지스트리이다.

디스크에 저장된 레지스트리 데이터를 "레지스트리 하이브(Hive)" 파일이라고 부르는데, 대표적으로 <u>`C:\Windows\System32\Config` 경로에 시스템 관련 하이브</u>가, <u>각 사용자 폴더 안에 `NTUSER.DAT`라는 이름으로 사용자별 하이브가</u> 저장됩니다. 부팅 시 윈도우의 설정 관리자(CM, Configuration Manager)가 이 파일들을 읽어 메모리 상에 트리 형태의 자료구조로 로그/구성한다.

<br>

## 𝙸𝙸. 레지스트리의 구조
---
레지스트리 구조는 일반적인 폴더 트리와 거의 흡사한 형태로 데이터를 저장한다.

파일 시스템으로 비유하여 설명하자면 이렇게 비유 할 수 있다. 

| 레지스트리 용어          | 파일 시스템 비유 | 설명                    |
| ----------------- | --------- | --------------------- |
| 키(Key)            | 폴더        | 다른 키나 값을 담는 컨테이너      |
| 값(Value)          | 파일        | 실제 데이터를 갖는 항목 (이름 존재) |
| 값 타입(Value Type)  | 파일 확장자    | 값 데이터가 저장된 형식 (타입)   |
| 값 데이터(Value Data) | 파일 내용     | 값이 실제로 담고 있는 데이터      |

또한 레지스트리의 특징으로는 값 변경 시 즉시 운영체제와 응용 프로그램에 반영되어 별도 재부팅을 필요로 하지 않는 경우가 많으며, 일부 핵심 시스템 설정을 제외하곤 즉시 적용된다. 그렇기 때문에 더더욱 레지스트리 수정에는 신중을 가해야한다.

<br>

### 값 타입(Value Type)의 종류
---

![](https://lh3.googleusercontent.com/d/1YLRsWOJW2BVyqkf8rD_BQELCNVNa3Y-a)
_값 타입(Value Type)의 종류[^2]_

<br>

## 𝙸𝙸𝙸. 보안관점에서의 레지스트리
---
레지스트리는 단순한 설정 정보 저장소를 넘어, 악성코드의 동작 방식이나 사용자 행위를 입증하는 결정적인 아티팩트(Artifact) 역할을 한다.

- **지속성(Persistence) 메커니즘 분석**
	- 악성코드가 재부팅 후에도 자동 실행되도록 등록하는 Run 키, 서비스(Services) 등록 정보, 스케줄러 설정 등을 확인할 수 있다.
    
- **은닉 요소 탐지**
	- 레지스트리 내부 값 데이터 영역에 악성 바이너리나 스크립트를 은닉하는 파일리스(Fileless) 공격 기법을 탐지할 수 있다.
    
- **사용자 행위 추적**
	  최근 실행한 프로그램 목록, 네트워크 연결 이력, USB 등 외부 저장매체 연결 기록 등 사용자 활동 흔적이 보존되어 있다.
    
- **시스템 변조 유무 검증**
	  보안 정책 해제, 방화벽 비활성화 등 시스템 환경 설정이 무단으로 변경되었는지 추적할 수 있다.

이렇듯 윈도우 시스템에서의 레지스트리는 침해사고 대응이나 포렌식 분석 등 보안 분석에서 중요한 요소이므로 해당 구조에 대해 학습해야만 한다. 다음 글에서는 레지스트리의 다양한 키(Key)에 대해서 알아보도록 하자.

<br>
<br>
<br>
<br>
<br>
<br>

## Related Posts
---
- [[Windows] 윈도우의 핵심 프로세스](https://bangjeongbin.github.io/TIL-Blog/posts/til-os-core-windows-processes/)

<br>

## Reference
---
- [레지스트리(Registry) 에 대해 알아보겠습니다.](https://feccle.tistory.com/31)
- [Windows registry information for advanced users](https://learn.microsoft.com/en-us/troubleshoot/windows-server/performance/windows-registry-advanced-users)
- [[OS] 윈도우 레지스트리 개념과 구조, 주요 특징](https://star7sss.tistory.com/1085)

<br>

[^1]: 출처: https://star7sss.tistory.com/985
[^2]: 출처: https://learn.microsoft.com/en-us/troubleshoot/windows-server/performance/windows-registry-advanced-users
