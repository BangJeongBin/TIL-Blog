---
title: "[Windows] 윈도우의 Privilege와 Integrity Level"
description: Privilege와 Integrity Level에 대하여
author: bin
date: 2026-02-28 09:00:00 +0800
categories: [TIL, OS, Windows]
tags: [OS, Windows, Privilege, Integrity Level]
pin: false
math: true
mermaid: true
image:
 path: https://www.thewindowsclub.com/wp-content/uploads/2022/05/Mandatory-Integrity-Control-in-Windows.png
 alt: Today I Learnd
---
_윈도우의 Integrity Level 피라미드[^1]_
{: .text-center }

<br>

## 𝙸. 프로세스 권한 (Privilege)
---
- Windows Privileges는 <u>프로세스가 시스템을 대상으로 수행할 수 있는 행위의 목록</u>이다.
	
- 일반적인 파일 권한(DACL)과 달리, 이 권한은 프로세스, 서비스, 토큰, 시스템 구성 요소에 직접 영향을 주며, 사용자 로그온 시 생성되는 **액세스 토큰** 안에 포함되어 검사된다.
	
- 권한의 이름은 보통 `Se`로 시작한다. 또한 현재(윈도우 10 이상) 버전에서는 약 **40~45**개의 권한이 정의되어 있으며, 보유하는 권한의 범위는 계정 종류와 그룹 정책, 로컬 보안 정책에 따라 달라진다.

<br>

현재 프로세스가 어떤 권한을 갖고 있고 어떤 상태(**Enabled**/**Disabled**)인지는 `whoami /priv` 명령어로 확인 가능
```
C:\Windows\ServiceProfiles>whoami /priv

PRIVILEGES INFORMATION
----------------------

Privilege Name               Description                          State
============================= ==================================== ========
SeShutdownPrivilege           Shut down the system                 Disabled
SeChangeNotifyPrivilege        Bypass traverse checking             Enabled
SeUndockPrivilege              Remove computer from docking station Disabled
SeIncreaseWorkingSetPrivilege  Increase a process working set       Disabled
SeTimeZonePrivilege            Change the time zone                 Disabled
```

<br>

## 𝙸𝙸. 무결성 수준 (Integrity Level, IL)
---

![Process Explorer](https://blog.kakaocdn.net/dna/eKcXvS/btrZlrcNuMC/AAAAAAAAAAAAAAAAAAAAAMcUZkQUfgoMJ2V6a3ve4A--X8HPa-eCrRMM5cuzDX1Y/img.png?credential=yqXZFxpELC7KVnFOS48ylbz2pIh7yKj8&expires=1790780399&allow_ip=&allow_referer=&signature=G4quN2X1yzChE7UngZT%2BmzCPt40%3D)
_Process Explorer를 사용한 Integrity Level 확인[^2]_

- Integrity Level은 프로세스가 가진 **신뢰도 등급**을 의미하며 UAC와 함께 처음 도입된 보안 메커니즘으로, 엄밀히 말하면 무결성 수준은 UAC 메커니즘의 일부라고 봐도 무방하다.
	
- 기존의 NTFS 파일 권한이 소유자가 임의로 권한을 부여하는 **DAC** 방식이라면, 무결성 수준은 **MAC**를 기반으로 한 통제 정책이다. 시스템이 정한 신뢰 등급에 따라 접근 가능 여부가 강제로 결정

<br>

> E.g. 프로세스가 다른 프로세스 안에서 쓰기를 원한다면 최소한 동일한 무결성 수준을 가져야 한다. 이는 낮은 무결성 수준을 가진 프로세스가 중간 무결성 수준을 가진 프로세스에 대해 완전한 접근 권한을 가진 핸들을 열 수 없다는 것을 의미함.
{: .prompt-tip }

<br>

### Integrity Level 5단계
---

|    **IL**     |     **SID**      | **설명**                                                                                                                                                    |
| :-----------: | :----------: | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
|  **SYSTEM**   | S-1-16-16384 | 윈도우 커널 및 핵심 서비스가 사용하는 최상위 수준                                                                                                                          |
|   **HIGH**    | S-1-16-12288 | 일반적으로 관리자 권한 프로세스가 사용하며, UAC 프롬프트 승인을 거쳐야 도달 가능. <br>시스템 레지스트리 수정, 프로그램 설치, 시스템 파일 변경 등이 가능                                                           |
|  **MEDIUM**   | S-1-16-8192  | 일반 사용자 프로세스의 기본 수준. <br>관리자 계정으로 로그인한 상태이더라도, UAC를 거치지 않고 실행된 프로그램은 기본적으로 Medium 수준으로 동작한다.                                                           |
|    **LOW**    | S-1-16-4096  | 웹 브라우저(Chrome, Edge 등)의 탭 프로세스나 PDF 뷰어 등 인터넷 자원을 처리하는 애플리케이션에 적용.<br>악성 파일이 다운로드되거나 웹을 통해 실행되더라도, 시스템 파일이나 다른 프로그램의 메모리를 오염시키지 못하도록 격리(Sandbox)하는 역할. |
| **UNTRUSTED** |   S-1-16-0   | 가장 낮은 수준. 신뢰할 수 없는 외부 콘텐츠를 처리하는 프로세스가 주로 사용.<br>시스템의 거의 모든 영역에 쓰기 권한이 차단.                                                                             |

<br>

## 𝙸𝙸𝙸. Privilege와 IL의 동작 방식
---
### 시나리오로 보는 동작 방식
---
#### 1. 악성코드가 관리자 권한 프로세스에 코드를 주입하려 할 때 (DLL Injection)

- **상황**: 웹 브라우저(Low IL)를 통해 감염된 악성코드가 `System32`에서 실행 중인 보안 프로그램이나 탐색기 프로세스의 메모리를 변경하려 함.
    
- **Integrity Level의 작용**: 악성코드 프로세스(Low IL)가 target 프로세스(Medium 또는 High IL)에 `OpenProcess` 및 `WriteProcessMemory` API를 호출하는 순간, **IL 등급 차이로 인해 커널 수준에서 차단**됩니다. Privilege를 확인할 단계조차 가지 못한다.

<br>

#### 2. 시계(시간)를 변경하는 경우

- **상황**: 일반 프로그램이 Windows API를 사용해 시스템 시간을 변경하려 함.
    
- **Integrity Level의 작용**: 시스템 시간 개체는 고유한 IL을 가지고 있어 일반 Medium IL 프로세스의 접근을 제한. UAC 승인을 통해 **High IL**로 승격되어야 1차 관문을 통과한다.
    
- **Privilege의 작용**: UAS 승인을 통한 High IL 상태가 되더라도, 해당 프로세스 액세스 토큰 안에 `SeTimeZonePrivilege` 또는 `SeSystemtimePrivilege`라는 특정 권한이 부여되어 있고 **활성화 상태**여야만 최종적으로 시계가 변경된다.

<br>

### 차이점 정리
---

|   **구분**   | **Integrity Level (IL)**              | **Privilege (권한)**                         |
| :--------: | ------------------------------------- | ------------------------------------------ |
| **주요 차이점** | "너의 신뢰 등급으로 **이 대상(객체)**을 건드릴 수 있는가?" | "너의 토큰에 **이 시스템 명령**을 내릴 자격이 명시되어 있는가?"    |
| **제어 대상**  | 객체간 수평/수직 접근 (파일, 프로세스 메모리, 레지스트리 등)  | OS 차원의 특정 기능 실행 (셧다운, 드라이버 로드, 시계 변경 등)    |
| **주요 원칙**  | No Write Up (하위 등급은 상위 등급 수정 불가)      | 명시적 권한 매핑 (각 기능마다 `Se...Privilege` 1대1 매칭) |

<br>
<br>
<br>
<br>
<br>
<br>

## Related Posts
---
- [[Windows] 윈도우의 UAC(User Account Control)란?](https://bangjeongbin.github.io/TIL-Blog/posts/til-os-windows-what-is-uac)

<br>

## Reference
---
- [Windows Privileges란 무엇인가요?](https://lastcard.tistory.com/614)
- [Privileged 속성](https://learn.microsoft.com/ko-kr/windows/win32/msi/privileged)
- [Integrity Levels](https://angelica.gitbook.io/hacktricks/windows-hardening/windows-local-privilege-escalation/integrity-levels)

<br>

[^1]: 출처: https://www.thewindowsclub.com/mandatory-integrity-control
[^2]: 출처: https://goldsony.tistory.com/254
