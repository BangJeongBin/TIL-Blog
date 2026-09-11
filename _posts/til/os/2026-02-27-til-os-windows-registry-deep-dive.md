---
title: "[Windows] 윈도우 레지스트리 심화"
description: 레지스트리의 5가지 루트키와 주요 하이브 설명
author: bin
date: 2026-02-27 09:00:00 +0800
categories: [TIL, OS, Windows]
tags: [OS, Windows, Registry]
pin: false
math: true
mermaid: true
image:
 path: https://bangjeongbin.github.io/TIL-Blog/assets/img/posts/common/til-logo.png
 alt: Today I Learnd
---

![windows-hive-structure](https://i.pinimg.com/736x/db/e7/ab/dbe7abb64b7720dd3d03608e41e570c5.jpg)
_레지스트리의 하이브 구조[^1]_

<br>

## 𝙸. 루트 키 (Root Key)
---
레지스트리는 최상위 경로에 위치한 5개의 루트 키를 중심으로 구조를 형성한다.

<br>

### HKLM (HKEY_LOCAL_MACHINE)
---
- <mark>Master Key</mark>
	
- <u>루트키 중 파일로 존재하며 디스크의 하이브 파일에서 직접 로드되는 원본 데이터이다.</u>
	
- 시스템 전역 설정. 설치된 드라이버, 서비스, 하드웨어 정보 등
	
- 자체 하이브를 갖고 있으며, HKLM 하이브 중 일부는 관리자 계정으로도 접근하지 못하는 하이브가 있어 시스템 계정으로 접근 가능

<br>

### HKU (HKEY_USERS)
---
- <mark>Master Key</mark>
	
- <u>루트키 중 파일로 존재하며 디스크의 하이브 파일에서 직접 로드되는 원본 데이터이다.</u>
	
- 시스템에 등록된 모든 사용자 계정의 설정. 계정 프로파일은 각 키들의 (기본값)에 링크되어 있다.
	
- HKCU는 사실 이 중 현재 사용자 항목을 가리키는 링크이다.

<br>

### HKCU (HKEY_CURRENT_USER)
---
- <mark>Derived Key</mark>
	
- 현재 로그인한 사용자의 개인 설정으로 현재 로그온한 사용자의 정보를 서브키로 가진다.
	
- 이 서브키들은 HKU 루트키에서 가져온 것으로 아래 그림과 같이 HKU 서브키들 중 현재 로그인한 사용자의 SID (S1002) 계정의 서브키들이 HKCU의 서브키와 동일한 것을 볼 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdna%2FbT41je%2FbtqDZYJSbr5%2FAAAAAAAAAAAAAAAAAAAAAF26KHiHcwjK-aok6MOGkYtMMZfdhTrMYfnobZjQTDtx%2Fimg.png%3Fcredential%3DyqXZFxpELC7KVnFOS48ylbz2pIh7yKj8%26expires%3D1790780399%26allow_ip%3D%26allow_referer%3D%26signature%3D7xyqFNtEjKeyaCGydl3eHoPdMn0%253D)
_HKEY_CURRENT_USER[^2]_

<br>

### HKCR (HKEY_CLASSES_ROOT)
---
- <mark>Derived Key</mark>
	
- 파일 확장자 연결, COM 객체 등록 정보 등
	
- 해당 루트키는 하위 서브키로 HKLM\SOFTWARE\Classes와 HKU\<SID>\Classes의 심볼릭 링크 정보를 가짐 (.btapp)

<br>

### HKCC (HKEY_CURRENT_CONFIG)
---
- <mark>Derived Key</mark>
	
- 현재 하드웨어 프로파일 정보로 이 키에 저장된 정보들은 디스크에 영구적으로 저장되지는 않고 시스템이 시작할 때 사용되는 하드웨어 프로파일을 저장
	
- 별도의 하이브를 갖고 있지 않으며 프로그램이 현재 활성화된 하드웨어를 알아보기 위해 이 루트키 참조한다.

<br>

## 𝙸𝙸. 마스터 키 (Master key), 파생 키 (Derived key)
---
![master_key_and_derived_key](https://www.forensic-artifacts.com/forensicArtifact/img/registry-forensics/sub01/003.png)
_Master Key와 Derived Key[^3]_

- **Master Key**
	- Derived key의 원본을 말하며, Windows의 Configuration Manager가 각 하이브 파일을 읽어 구성하는 값들로 레지스트리 하이브로부터 직접 값을 읽어 구성된다.
	- **HKEY_LOCAL_MACHINE**, **HKEY_USERS**가 여기에 해당

<br>

- **Derived key**
	- Master key의 심볼릭 링크 값들을 말하며, 해당 값들은 파일로 존재하지 않으며 메모리에만 존재한다.
	- **HKET_CLASSES_ROOT**, **HKEY_CURRNET_USER**, **HKEY_CURRNET_CONFIG**가 여기에 해당

<br>

> E.g. HKEY_CURRENT_USER는 메모리상에서 사용자 SID에 해당하는 마스터 키 영역으로부터 파생되어 구성됩니다.
{: .prompt-tip }

<br>

## 𝙸𝙸𝙸. 주요 하이브 목록
---
- **HKLM\HARDWARE**
	- 해당 하이브는 휘발성 정보로 메모리에 존재한다.
	- 모니터 포트 등 부팅 시 관련된 하드웨어 장치와 드라이버 맵핑 정보들을 저장

<br>

- **HKLM\SAM**
	- 경로: %SystemRoot% \System32\Config\SAM
	- 해당 하이브는 사용자의 로컬 계정 정보(로컬 계정의 식별자(RID), 암호화된 패스워드 해시, 사용자 프로필 등)와 그룹 정보를 갖고 있음 (리눅스 /etc/passwd와 비슷)
	- 만약 조사하고자 하는 시스템이 도메인 컨트롤러라면 AD(Active Directory)에 도메인 계정과 그룹 정보를 가진다.
	- 이 하이브는 일반 관리자 계정으로도 접근이 불가능하며, 시스템 계정으로만 접근 가능하다.

<br>

- **HKLM\SECURITY**
	- 경로: %SystemRoot% \System32\Config\SECURITY
	- 시스템 범위의 보안 정책과 사용자 권한 할당 정보, 현재 시스템의 패스워드 또는 마지막 로그온 사용자의 패스워드 등의 정보를 가진다.
	- 이 하이브 또한 시스템 계정으로만 접근이 가능하다.

<br>

- **HKLM\SYSTEM**
	- 경로: %SystemRoot% \System32\Config\SYSTEM
	- 해당 하이브는 시스템이 부팅될 때의 환경 설정 정보를 가진다.
	- 이런 정보들은 시스템이 정상적 부팅되었을 때 복사되며, 시스템이 비정상적으로 종료되었을 때 복사해 둔 정보를 바탕으로 부팅할 수 있는 옵션을 사용자에게 제공한다.
	- 해당 하이브에서 중요한 것은 바로 **CurrentControlSet** 키

<br>

## 𝙸𝚅. 포렌식 관점에서의 하이브
---
정상적으로 윈도우가 동작하는 중에는 운영체제가 레지스트리 하이브 파일의 삭제, 수정, 복사를 엄격히 보호하기 때문에 일반적인 파일 복사나 응용 프로그램 API로는 SYSTEM, SAM 같은 하이브를 그대로 가져올 수 없다.

활성화 시스템에서의 하이브 파일을 획득하려면, 저장매체의 섹터에 직접 접근하여 데이터 콘텐츠를 읽어오는 전문 포렌식 도구(예: FTK Imager, X-Ways Forensics 등)를 사용해야한다.

<br>
<br>
<br>
<br>
<br>
<br>

## Related Posts
---
- [[Windows] 윈도우의 핵심 프로세스](https://bangjeongbin.github.io/TIL-Blog/posts/til-os-core-windows-processes/)
- [[Windows] 윈도우의 레지스트리란?](https://bangjeongbin.github.io/TIL-Blog/posts/til-os-core-what-is-windows-registry/)

<br>

## Reference
---
- [Windows Registry Hives in Digital Forensics](https://ccnaguru.com/windows-registry-hives-in-digital-forensics/)
- [[Digital Forensic] Registry 분석](https://yum-history.tistory.com/265)
- [02. 레지스트리 구성](https://www.forensic-artifacts.com/registry-forensics/sub01)

<br>

[^1]: 출처: https://ccnaguru.com/windows-registry-hives-in-digital-forensics/
[^2]: 출처: https://yum-history.tistory.com/265
[^3]: 출처: https://www.forensic-artifacts.com/registry-forensics/sub01
