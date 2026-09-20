---
title: "[Windows] 윈도우의 UAC(User Account Control)란?"
description: UAC의 개념과 동작원리에 관하여
author: bin
date: 2026-02-29 09:00:00 +0800
categories: [TIL, OS, Windows]
tags: [OS, Windows, UAC]
pin: false
math: true
mermaid: true
image:
 path: https://learn.microsoft.com/en-us/windows/security/application-security/application-control/user-account-control/images/uac-consent-prompt-admin.png
 alt: Today I Learnd
---
_윈도우의 UAC 프롬프트[^1]_
{: .text-center }

<br>

## 𝙸. 윈도우의 UAC(User Account Control)란?
---
### UAC 등장 배경
---
`Windows XP` 때는 운영체제는 초기 설치 시 생성되는 첫 번째 사용자 계정을 자동으로 **관리자 그룹(Administrators)**에 포함시켰다. 그러면 세션에서 실행되는 모든 프로세스가 곧바로 관리자 권한을 상속받게 되었는데 이렇게 되면 대다수의 사용자가 항상 관리자 권한으로 시스템을 사용하게 된다.
   
이로 인해 일반적인 사용자가 관리자 권한으로 작업할 수밖에 없는 환경이 형성되었고, 악성코드(백도어, 원격 쉘 등)가 실행될 경우 곧바로 관리자 권한을 획득하여 시스템 전체에 영향을 미치는 심각한 보안 사고가 빈번하게 발생히였다. 그래서 `Windows Vista`부터 새로운 권한 관리 메커니즘인 **UAC**를 도입하게되었다.

<br>

### UAC의 정의 및 주요 목적
---
**UAC**의 핵심은 <mark>최소 권한 원칙(Principle of Least Privilege)</mark><sup>[ⓐ](#footnote_1)</sup>에 기반하여 작동한다. 이 말은 즉 필요한 순간에, 필요한 만큼만 권한을 부여한다는 개념이다. 실제로 <u>관리자 그룹(Administrators)에 속한 계정이라도, 모든 프로세스는 기본적으로 일반 사용자 수준의 권한으로 실행한다.</u>

<br>

다음은 **UAC의 주요 도입 목적** 4가지 이다.

|    **도입 목적**    | **설명**                                                                 |
| :-------------: | ---------------------------------------------------------------------- |
| **권한 상승 공격 완화** | 사용자의 동의 없이는 관리자 수준으로 프로그램을 실행할 수 없도록 제한한다.                             |
| **최소 권한 원칙 구현** | 사용자가 의도적으로 권한을 상승시키지 않는 한, 일상적인 작업은 제한된 권한으로 수행된다.                     |
|  **보안 인식 제고**   | 권한 상승이 요청될 때 사용자에게 시각적으로 알려주어, "지금 이 프로그램이 높은 권한을 요구하고 있다"는 사실을 인지시킨다. |
|   **호환성 유지**    | 관리자 권한을 필요로 하는 기존 소프트웨어도 계정 전환 없이 그대로 사용할 수 있게 해준다.                    |

<br>

### UAC 프롬프트의 종류
---
UAC 프롬프트의 색상은 3가지로 나뉜다.

![uac prompt color](https://upload.wikimedia.org/wikipedia/en/7/72/User_Account_Control.png?utm_source=en.wikipedia.org&utm_campaign=parser&utm_content=thumbnail_unscaled)
_UAC 프롬프트의 종류 (Windows 11)[^2]_
{: .text-center }

#### 빨간색 배경 (경고)
- <span style="color:red">차단된 앱</span>
- 신뢰할 수 없는 프로그램이나 차단된 프로그램이 관리자 권한을 요청할 때 나타난다. 해당 프로그램의 게시자가 시스템 정책이나 Windows Defender, Smart Screen 등으로 차단되어 있을 경우 상단이 빨간색으로 된 창이 뜨면서 실행 자체가 불가능하게 된다.

#### 노란색 배경 (주의)
- <span style="color:yellow">게시자를 알 수 없는 앱</span>
- 디지털 서명이 없거나 유효하지 않은 게시자의 프로그램이 관리자 권한을 요청할 때 나타난다. 공식 기관에서 발급된 인증서가 아니거나 파일이 변조되었을 때 주로 발생한다.

#### 파란색/회색 배경 (시스템 작업)
- <span style="color:blue">게시자가 알려지거나 신뢰할 수 있는 앱</span>
- Windows 자체의 설정이나 시스템 작업이 관리자 권한을 요청할 때 나타난다. 일반적으로 위험 위협이 크게 없다.

<br>

> **참고 자료**    
> [UAC 프롬프트를 노출시키는 주요 작업들 - WIKIPEDIA](https://en.wikipedia.org/wiki/User_Account_Control)
{: .prompt-tip }

<br>

## 𝙸𝙸. UAC 동작 원리
---
 기본적으로 윈도우 운영체제는 일반 사용자뿐만 아니라 관리자 계정이라 할지라도 보안 컨텍스트(Security Context)를 일반 사용자 수준으로 제한하여 프로세스를 실행한다.

 사용자가 로그인하면 시스템에서 **해당 사용자에 대한 액세스 토큰**을 만든다. 액세스 토큰에는 특정 SID(보안 식별자) 및 Windows 권한을 포함하여 사용자에게 부여되는 액세스 수준에 대한 정보가 포함된다.

 또한 관리자 그룹(Administrators)에 속하는 사용자가 로그인온하면 **표준 사용자 액세스 토큰**과 **관리자 액세스 토큰**이라는 <u>두 개의 별도 액세스 토큰이 만들어진다.</u>

![diff login admin and user](https://learn.microsoft.com/ko-kr/windows/security/application-security/application-control/user-account-control/images/uac-windows-logon-process.gif)
{: .align-center }
_관리자와 표준 사용자의 로그인 프로세스 차이[^1]_
{: .text-center }

<br>

### 엑세스 토큰 구조
---
#### 표준 사용자 액세스 토큰 (Standard User Access Token)
- **권한 필터링**: 상승된 토큰과 동일한 사용자 식별 정보를 가지고 있지만, 관리자 전용 윈도우 권한과 관리자 SID가 제거된 상태의 토큰
    
- **기본 프로세스 실행**: 관리자 작업이 필요 없는 일반적인 애플리케이션을 실행하는 데 사용
    
- **데스크톱 및 권한 상속**: 로그인 시 바탕화면을 띄우는 `explorer.exe` 프로세스를 이 제한된 토큰으로 실행한다. 이후 사용자가 시작하는 모든 애플리케이션은 `explorer.exe`의 하위 프로세스로서 이 '제한된 토큰'을 상속받아 기본적으로 일반 사용자 권한으로 동작

<br>

#### 관리자 액세스 토큰 (Administrator Access Token)
- 계정에 할당은 되나 기본적으로 사용할 수 없고 <u>UAC 프롬프트를 통해 활성화되는 토큰</u>
	
- **권한 범위**: 시스템 주요 설정 변경, 파일 설치 등 전체 관리자 권한을 행사할 수 있는 토큰
    
- **전환 메커니즘**: 관리자 계정으로 웹 서핑이나 이메일 확인 등의 일상 작업을 할 때는 제한된 토큰이 사용되다가, 관리자 권한이 필요한 작업이 발생하면 윈도우가 사용자에게 승인을 요청하는 UAC 프롬프트를 출력. UAC 프롬프트를 거쳐 상승된 토큰을 사용하는 프로세스는 종료되기 전까지 권한 상승 상태를 지속적으로 유지한다.
    
- **실행 조건**: 사용자가 동의(Consent)하거나 자격 증명을 입력하여 승인할 때에만 해당 프로그램에 전체 관리자 권한을 가진 '상승된 토큰'이 할당되어 실행
 
<br>

## 𝙸𝙸𝙸. UAC 설정 4단계
---
![uac settings](https://learn.microsoft.com/ko-kr/windows/win32/uxguide/images/winenv-uac-image3.png)
{: .align-center }
_UAC 설정 4단계 (Windows 7)[^3]_
{: .text-center }

<br>

|   **UAC 설정 수준**    | **동작 방식 및 특징**                                                                                                        |
| :----------------: | --------------------------------------------------------------------------------------------------------------------- |
|     **항상 알림**      | 모든 권한 상승 요청 시 UAC 프롬프트가 활성화된다.                                                                                        |
|  **기본 알림 (기본설정)**  | 마이크로소프트가 서명한 프로그램(윈도우 업데이트, 제어판 설정 등)은 프롬프트 없이 자동 권한 상승되며, 외부 프로그램 요청 시 알림을 띄운다.                                      |
| **바탕화면이 어두워지지 않게** | 기본 알림과 동일하나 보안 데스크톱(어두워지는 화면)에서 실행되지 않고 별도의 알림 창으로 활성화된다.<br>공격자나 악성코드가 UAC 프롬프트와 상호작용(강제 허용 응답 등)할 가능성이 높아질 가능성이 있다. |
|     **알리지 않음**     | UAC 비활성화 모드이다.<br>**보안상 전혀 권장하지 않음.**                                                                                 |

<br>

## 𝙸𝚅. UAC Auto-Elevation
---
 윈도우 운영체제의 자동 권한 상승(Auto-Elevation)은 UAC 기본 설정 환경에서 사용자가 제어판 설정 변경이나 시스템 도구를 사용할 때, 보안성을 유지하면서도 불필요한 알림 팝업으로 인한 불편함을 줄이기 위해 도입된 메커니즘이다.

 프로세스가 실행될 때 윈도우의 응용 프로그램 정보 서비스(AIS, Application Information Service / AppInfo)는 해당 프로세스가 UAC 프롬프트(경고창) 없이 관리자 권한(`Administrator Access Token`)을 자동으로 획득할 수 있는지 검증한다.

 자동 권한 상승이 이루어지기 위해서는 다음 **4가지 조건이 예외 없이 모두 동시에 충족**되어야 한다.

<br>

### UAC 자동 권한 상승(Auto-Elevation) 필수 조건
---
#### 1. 사용자 계정 자격 조건 (Administrators Group)

- 실행 주체 계정이 관리자 그룹(Administrators)에 속해 있어야 한다.
    
- 일반 사용자(Standard User) 계정에서 실행할 경우에는 자동 권한 상승이 불가능하며, 항상 관리자 자격 증명을 요구하는 프롬프트가 출력

#### 2. 디지털 서명 조건 (Microsoft Digital Signature)

- 실행 파일(`.exe`)이 **마이크로소프트(Microsoft)의 유효한 디지털 서명**으로 서명되어 있어야 한다.
    
- 서명이 없거나, 타사(Third-party) 서명, 혹은 서명이 훼손된 파일은 자동 권한 상승 대상에서 제외

#### 3. 매니페스트(Manifest) 설정 조건

- 실행 파일의 리소스 섹션 내에 포함된 XML 구조의 **매니페스트 파일**에 자동 권한 상승 명시가 존재해야 한다.
    
- `<autoElevate>true</autoElevate>` (또는 `autoElevate="true"`) 속성이 설정되어 있고, executionLevel이 `requireAdministrator` 또는 `highestAvailable`로 지정되어 있어야 운영체제가 자동 권한 상승 절차를 발동

#### 4. 신뢰할 수 있는 경로 조건 (Trusted Directory)

- 실행 파일이 보안상 보호받는 **신뢰할 수 있는 시스템 디렉터리** 내에 위치해야 한다. 임의의 사용자 폴더(`C:\Users\...`)나 다운로드 경로에서 실행되는 파일은 다른 모든 조건을 만족하더라도 자동 권한 상승이 거부된다.
    
- 대표적인 경로: `C:\Windows\System32\` 또는 `C:\Program Files\` 등 관리자 권한 없이는 파일 수정 및 조작이 불가능한 보안 경로

<br>
<br>
<br>
<br>
<br>
<br>

## Related Posts
---
- [[Windows] 윈도우의 Privilege와 Integrity Level](https://bangjeongbin.github.io/TIL-Blog/posts/til-os-windows-privilege-and-integrity-level)

<br>

## Footnote
---
> <a name="footnote_1">ⓐ</a> 최소 권한 원칙(PoLP): "최소 권한 액세스"라고도 하는 최소 권한 원칙은 사용자가 자신의 책임을 수행하기 위해 절대적으로 필요한 항목에만 액세스할 수 있어야 한다는 개념입니다.

<br>

## Reference
---
- [사용자 계정 컨트롤 작동 방법](https://learn.microsoft.com/ko-kr/windows/security/application-security/application-control/user-account-control/how-it-works)
- [User Account Control](https://en.wikipedia.org/wiki/User_Account_Control)
- [사용자 계정 컨트롤(UAC)의 역할 및 설정 끄기](https://m.blog.naver.com/kangyh5/223826000461)
- [사용자 계정 컨트롤 (UAC)](https://wikidocs.net/307277)
- [사용자 계정 컨트롤](https://namu.wiki/w/%EC%82%AC%EC%9A%A9%EC%9E%90%20%EA%B3%84%EC%A0%95%20%EC%BB%A8%ED%8A%B8%EB%A1%A4)

<br>

[^1]: 출처: https://learn.microsoft.com/ko-kr/windows/security/application-security/application-control/user-account-control/how-it-works
[^2]: 출처: https://en.wikipedia.org/wiki/User_Account_Control
[^3]: 출처: https://learn.microsoft.com/ko-kr/windows/win32/uxguide/winenv-uac
