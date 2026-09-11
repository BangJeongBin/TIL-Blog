---
title: "[Windows] 윈도우의 핵심 프로세스"
description: Windows 핵심 프로세스들의 계층 구조와 기능별 분류
author: bin
date: 2026-02-25 09:00:00 +0800
categories: [TIL, OS, Windows]
tags: [OS, Windows, Process]
pin: false
math: true
mermaid: true
image:
 path: https://bangjeongbin.github.io/TIL-Blog/assets/img/posts/common/til-logo.png
 alt: Today I Learnd
---

![windows_components](https://learn.microsoft.com/ko-kr/windows-hardware/drivers/kernel/images/ntarch.png)
_Windows의 구성요소[^1]_

<br>

## 𝙸. 윈도우 프로세스 계층 구조
---
```
[SYSTEM] (PID 4, 커널 모드 컨테이너)
 └── [SMSS.EXE] (Master 세션 관리자)
      │
      ├── [SMSS.EXE (Session 0)] (서비스 세션) ── [종료됨]
      │    ├── CSRSS.EXE (Session 0 전용 서브시스템)
      │    └── WININIT.EXE (세션 0 백그라운드 서비스 시작)
      │         ├── SERVICES.EXE (서비스 제어 관리자 - SCM)
      │         │    └── SVCHOST.EXE (서비스 호스트)
      │         │         ├── TASKHOSTW.EXE (예약 작업 호스트)
      │         │         └── RUNTIMEBROKER.EXE (UWP 앱 권한 프록시)
      │         ├── LSASS.EXE (로컬 보안 인증 서브시스템)
      │         └── LSAISO.EXE (가상화 기반 자격 증명 보호 - Credential Guard)
      │
      └── [SMSS.EXE (Session 1)] (사용자 UI 세션) ── [종료됨]
           ├── WINLOGON.EXE (대화형 사용자 로그온 처리)
           │    ├── USERINIT.EXE (사용자 환경 초기화) ── [종료됨]
           │    │    └── EXPLORER.EXE (Windows 탐색기 / 셸)
           │    │         └── [주로 사용자 실행 프로세스들] (Chrome, KakaoTalk 등)
           │    └── CSRSS.EXE (Session 1 UI 사용자 서브시스템)
           └── CSRSS.EXE (Session 1 전용 서브시스템)
```

<br>

윈도우는 부팅 시 보통 100개 내외의 프로세스가 실행된다. 시스템이 부팅될 때 특정 순서에 따라 핵심 프로세스들이 부모-자식 관계를 형성하며 생성 및 초기화된다.

<br>

### 간략한 부팅의 순서
---
1. `SYSTEM` (PID 4<sup>[ⓐ](#footnote_1)</sup>): 윈도우 최상위 컨테이너 프로세스
	
2. `SMSS.EXE` (Master): Session Manager Subsystem의 약자로, 시스템 세션을 생성하고 초기화
    - Session 0 (서비스 관리 영역): 백그라운드 서비스 전용 세션 (`WININIT.EXE` 호출)
    - Session 1 (사용자 환경 영역): 실제 대화형 사용자 화면 세션 (`WINLOGON.EXE` 호출)
        
3. 초기화 세션 SMSS의 종료: Session 0과 Session 1을 생성한 세션별 `SMSS.EXE` 및 로그인 후의 `USERINIT.EXE`는 역할을 마치면 자연스럽게 종료(Terminated)된다.

<br>

## 𝙸𝙸. 기능별 프로세스 분류
---
### 시스템 초기화 · 커널 관련
---
- `System`:	커널 모드 스레드가 실행되는 윈도우 커널 자체의 프로세스 (PID 4, 실행 파일 없음)
	
- `System Idle Process`:	CPU가 놀고 있는 시간을 나타내는 가상의 프로세스
	
- `smss.exe`:	세션 매니저. 세션 생성과 초기화를 담당하고 임무가 끝나면 종료
	
- `csrss.exe`:	Win32 서브시스템의 사용자 모드 파트너. 콘솔 창, 프로세스/스레드 생성 통지 등을 처리
	
- `wininit.exe`:	세션 0에서 서비스 제어 관리자·LSASS 등 핵심 백그라운드 프로세스를 기동
	
- `winlogon.exe`:	대화형 로그온 처리. 자격 증명 공급자를 불러오고 로그온/로그오프를 관리

<br>

### 보안 · 인증
---
- `lsass.exe`:	로그온 검증, 액세스 토큰 발급, 보안 정책 적용, 보안 이벤트 로깅을 담당하는 인증의 핵심
	
- `lsaiso.exe`:	Credential Guard 활성화 시 VBS(가상화 기반 보안)로 자격 증명을 격리된 영역에 보관

<br>

### 서비스 관리
---
- `services.exe`:	서비스 제어 관리자(SCM). 등록된 윈도우 서비스의 시작·중지·복구를 관리
	
- `svchost.exe`:	여러 서비스 DLL을 하나의 프로세스로 묶어 실행하는 범용 호스트
	
- `spoolsv.exe`:	인쇄 작업 큐 관리 및 프린터 드라이버 인터페이스 제공
	
- `taskhostw.exe`:	작업 스케줄러가 실행하는 DLL 기반 작업을 담는 호스트

<br>

### 사용자 인터페이스
---
- `explorer.exe`:	바탕화면·작업 표시줄·시작 메뉴·파일 탐색기를 제공하는 윈도우 셸
	
- `dwm.exe`:	창 합성(compositing)과 시각 효과 렌더링
	
- `ShellExperienceHost.exe`:	액션 센터, 시작 메뉴 타일 등 모던 UI 요소 렌더링
	
- `SearchUI.exe`:	검색 UI (최신 버전은 SearchApp.exe·SearchHost.exe로 이름이 바뀜)

<br>

### 런타임 · 지원
---
- `RuntimeBroker.exe`:	UWP 앱이 요청하는 카메라·위치 등 권한을 중개·검증
	
- `fontdrvhost.exe`:	사용자 모드에서 글꼴 렌더링 처리
	
- `ctfmon.exe`:	IME, 필기 인식, 음성 입력 등 대체 텍스트 입력 서비스 관리

<br>

### 백그라운드 · 모니터링
---
- `WmiPrvSE.exe`:	WMI 공급자를 호스팅해 관리 스크립트·쿼리 실행을 지원
	
- `SearchIndexer.exe`:	파일 콘텐츠를 인덱싱해 빠른 검색을 지원
	
- `MsMpEng.exe`:	Windows Defender의 실시간 검사 엔진
	
- `SecurityHealthService.exe`:	Windows 보안 센터 상태 점검 및 알림 관리

<br>

## 𝙸𝙸𝙸. 마무리
---
Windows에서는 많은 프로세스가 복잡하게 동작하고 있기에 정상적인 프로세스를 알면 악성프로세스를 트리아지 할 수 있는 능력이 생긴다.

공격자는 탐지를 회피하기 위해 `svchost.exe`, `explorer.exe` 같은 정상 프로세스의 이름을 그대로 사용하는 경우가 많다. 이런 경우에서 악성 프로세스를 트리아지하기 위해선 **1. 파일 경로 확인**, **2. 부모 프로세스 확인**, **3. 디지털 서명** 등의 방법으로 정밀 분석하여 악성 프로세스를 식별할 수 있어야 한다.

<br>
<br>
<br>
<br>
<br>
<br>

## Related Posts
---
- [[Windows] 윈도우의 레지스트리란?](https://bangjeongbin.github.io/TIL-Blog/posts/til-os-core-what-is-windows-registry/)
- [[Windows] 윈도우 레지스트리 심화](https://bangjeongbin.github.io/TIL-Blog/posts/til-os-windows-registry-deep-dive)

<br>

## Footnote
---
> <a name="footnote_1">ⓐ</a> PID 4: 윈도우 System 프로세스에 항상 고정으로 할당되는 PID 번호. 윈도우 운영체제가 컴퓨터를 구동하고 유지하는 데 필수적인 프로세스이므로, 임의로 종료하거나 없앨 수 없는 특징이 있다.

<br>

## Reference
---
- [Overview of Windows components](https://learn.microsoft.com/en-us/windows-hardware/drivers/kernel/overview-of-windows-components)
- [윈도우 부팅과 시스템 프로세스](https://information-security.tistory.com/445)
- [[Windows] Windows 주요 프로세스 분석](https://darksoulstory.tistory.com/487)

<br>


[^1]: 출처: https://learn.microsoft.com/en-us/windows-hardware/drivers/kernel/overview-of-windows-components
