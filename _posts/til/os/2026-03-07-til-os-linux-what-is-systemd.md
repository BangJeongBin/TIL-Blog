---
title: "[Linux] systemd란?"
description: 리눅스의 init 프로세스인 systemd에 대하여
author: bin
date: 2026-03-07 09:00:00 +0800
categories: [TIL, OS, Linux]
tags: [OS, Linux, Process, init, systemd]
pin: false
math: true
mermaid: true
image:
 path: https://substackcdn.com/image/fetch/$s_!GsZ3!,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F5bb905ab-78a3-449c-a3e8-bc2552a0fd28_638x359.webp
 alt: Today I Learnd
---
_systemd Boot Process[^1]_
{: .text-center }

<br>

## 𝙸. systemd란?
---
systemd는 SysVinit의 여러 한계를 개선하기 위해 개발된 초기화 및 시스템 관리 시스템으로서 대표적으로 Ubuntu, Debian, RHEL 계열 등 <u>현재의 여러 리눅스 배포판에서 기본 초기화 시스템으로 systemd를 사용</u>한다.

systemd 역시 부팅 과정에서 PID 1로 실행되며, 시스템 서비스와 다양한 시스템 자원을 관리하지만 SysVinit과 다른 점은 <u>SysVinit은 Runlevel을 중심으로 동작하지만, systemd는 Unit과 Target을 중심으로 동작한다는 차이점</u>이 있다.

<br>
<br>

### 주요 기능
---
- **병렬 서비스 실행** 
	- SysVinit은 실행 순서에 따라 서비스를 순차적으로 시작하는 방식인데 반해 systemd는 서비스 간 의존성을 파악해 동시에 실행할 수 있는 **서비스를 병렬로 실행**
	- 예를 들어 네트워크 서비스와 다른 독립적인 서비스가 있다면 두 서비스를 동시에 시작할 수 있어 속도및 편의성이 크게 향상
	
- **서비스 의존성 관리**
	- 서비스 간 **실행 순서와 의존 관계를 관리**
	- 의존 관계를 효율적으로 처리하여 서비스가 올바른 순서로 시작되고, 서비스 장애 시 다른 서비스에 미치는 영향을 최소화
	
- **로그 통합 관리**
	- systemd는 `systemd-journald`를 통해 시스템 로그를 통합 관리. 이는 일관된 형식으로 로그를 제공하며, 로그를 쉽게 검색하고 분석 가능
	
- **서비스 상태 및 장애 관리**
	- systemd는 시스템 부팅 시 시작되는 서비스와 종료되는 서비스의 시작, 중지, 재시작 등을 관리. 각 서비스는 unit 파일로 정의되며, `systemctl` 명령어를 통해 제어
	- 설정에 따라 비정상 종료된 서비스를 재시작하도록 구성 가능

<br>
<br>
<br>
<br>
<br>

## 𝙸𝙸. Unit
---
systemd에서는 다양한 리소스를 **유닛(Unit)**으로 관리하는데 이는 **작업의 단위**를 말한다. 쉽게 말하면 systemd에서 관리하는 서비스(.service), 마운트(.mount), 소켓(.socket) 등의 객체라고 이해하면 된다. 

systemd는 다양한 unit 을 통해 리눅스 시스템의 서비스와 자원을 관리하는데 각 unit 은 시스템의 다른 부분을 관리하며, nuit의 종류는 파일 확장자로 구분한다.

<br>

#### 대표적인 Unit

- **`.service`**
	- 서비스나 애플리케이션 등 백그라운드 데몬을 관리하는 데 사용
	- 어떻게 서비스가 시작되고, 중지되고, 재시작되는지를 정의함
	- 예시: `cron.service`

<br>

- **`.socket`**
	- IPC 소켓, TCP 소켓 등 네트워크 소켓을 관리
	- 소켓(네트워크·IPC)을 대신 열어 두고, 요청이 오면 서비스를 기동
	- 예시: `cups.socket`

<br>

- **`.device`**
	- 커널이 인식한 하드웨어 장치인 시스템의 디바이스를 나타냄
	- udev 규칙에 의해 생성되며, 특정 디바이스에 대한 의존성을 정의할 때 사용
	- 예시: `dev-sda1.device`

<br>

- **`.mount`**
	- 파일시스템 마운트 지점을 관리
	- `/etc/fstab`에 있는 마운트 지점을 systemd unit으로 변환할 수 있음
	- 예시: `home.mount`

<br>

- **`.automount`**
	- 파일 시스템 마운트 지점을 접근하는 시점에 자동으로 마운트
	- 예시: `proc-sys-fs-binfmt_misc.automount`

<br>

- **`.target`**
	- 여러 유닛을 묶는 그룹화하여 관리하는 데 사용
	- 시스템의 특정 상태에 도달하기 위해 필요한 유닛들을 조합할 수 있음
	- 런레벨 역할을 대신함
	- 예시: `multi-user.target`

<br>

- **`.timer`**
	- 정해진 시각·주기에 작업 실행
	- cron의 대안
	- 예시: `apt-daily.timer`

<br>

- **`.swap`**
	- 스왑 영역 관리
	- swap 파일이나 swap 파티션을 정의하여 사용할 수 있음
	- 예시: `dev-sda2.swap`

<br>

- **`.path`**
	- 파일/디렉터리의 변화를 감지할 때 사용
	- 변경 사항이 있을 때 서비스를 활성화
	- 예시: `cups.path`

<br>

- **`.slice`**
	- 시스템 프로세스를 그룹화하여 리소스 관리를 수행
	- cgroup를 사용하여 CPU/메모리/IO 같은 리소스 제한 등 관리
	- 예시: `user.slice`

<br>

- **`.scope`**
	- systemd가 직접 띄우지 않은 외부 프로세스 묶음
	- 주로 시스템의 리소스 할당 및 관리를 위해 systmed에 의해 내부적으로 사용
	- 예시: `session-1.scope`

<br>

> **Runlevel과 Target 비교**    
> - Runlevel 0 $\approx$ `poweroff.target`
> - Runlevel 1 $\approx$ `rescue.target`
> - Runlevel 2 $\approx$ `multi-user.target`
> - Runlevel 3 $\approx$ `multi-user.target`
> - Runlevel 5 $\approx$ `graphical.target`
> - Runlevel 6 $\approx$ `reboot.target`
{: .prompt-tip }

<br>

#### Unit 파일 경로

systemd에게 인식되려면 unit은 하나의 파일로 직렬화되어야 하며 같은 이름이 여러 곳에 있으면 **위쪽이 우선**하는 특징이 있다.

1. **`/etc/systemd/system/`**
	- 관리자가 직접 만들거나 수정하는 곳 (최우선)
	- 사용자가 특정 서비스의 동작 방식을 변경하고자 할 때 사용됨. 예를 들어, 기본 서비스 유닛 파일에 사용자 정의 옵션을 추가하거나 수정하는 경우
	
2. **`/run/systemd/system/`**
	- 런타임에 생성되는 유닛
	- 이곳에 저장된 파일들은 시스템이 재부팅되면 사라지므로, 임시적인 변경을 위해 사용
	
3. **`/usr/lib/systemd/system/` (or `/lib/systemd/system/`)**
	- 패키지가 설치하는 기본 유닛
	- 즉, 시스템에 설치된 소프트웨어나 서비스가 자동으로 생성하는 유닛 파일들이 이곳에 위치

<br>
<br>
<br>
<br>
<br>

## 𝙸𝙸𝙸. 의존성 관리
---
<u>SysVinit과 달리 systemd는 유닛 사이의 의존 관계를 직접 관리</u>한다. 각 유닛 파일은 서비스의 동작 방식과 의존성을 정의한다. 의존성 관리는 크게 ‘순서’와 ‘요구사항’이라는 두 가지 측면에서 이루어진다.

- **순서 제어 (Ordering Dependencies)**
	- 특정 서비스가 다른 서비스보다 반드시 먼저 실행되어야 할 때 사용. 예를 들어, 데이터베이스 서비스가 실행되기 전에 네트워크 서비스가 먼저 올라와야 하는 경우
	
- **요구사항 제어 (Requirement Dependencies)**
	- 특정 서비스가 실행되기 위해 반드시 필요한 다른 서비스를 지정한다. 만약 필수 서비스가 시작되지 않으면, 이를 의존하는 서비스도 시작되지 않거나 실패 처리

<br>

| **종류**       | **의미**                                                |
| ------------ | ----------------------------------------------------- |
| `.After`     | 지정된 유닛이 시작된 후에 현재 유닛을 시작                              |
| `.Before`    | 지정된 유닛이 시작되기 전에 현재 유닛을 시작                             |
| `.Requires`  | **[강한 의존]** 지정된 유닛을 필수적으로 시작하며, 해당 유닛이 실패하면 현재 유닛도 중단 |
| `.Wants`     | **[약한 의존]** 지정된 유닛을 시작하려고 시도하지만, 실패해도 현재 유닛을 계속 실행    |
| `.Conflicts` | 지정된 유닛과 동시에 실행될 수 없음을 의미                              |

<br>

한 가지 주의할 점은, <u>의존성 (Wants/Requires)과 실행 순서 (After/Before)는 별개의 설정</u>이라는 것이다. 'A가 필요하다'와 'A 다음에 실행한다'는 따로 적어야 하며, 순서 지정이 없으면 systemd는 두 유닛을 병렬로 띄울 수 있다.

<br>
<br>

이처럼 현대의 Linux 에서는 init은 프로세스의 전통적인 구현 방식인 SysVinit 보다는 systemd 방식을 채택하는 것을 볼 수있다. 이는 위에 언급한 **병렬처리**와 **의존성 정리** 등의 특징이 효율적이기 때문임을 알 수 있다.

하지만 복잡성이 증가함에 따라 Unix의 철학인 <i>"한 가지 일을 잘하기"</i> 를 벗어나게 된다는 재미있는 논란이 있다는거 같기도 하다.ㅋㅋ

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## Related Posts
---
- [[Linux] SysVinit의 개념과 systemd와의 차이](https://bangjeongbin.github.io/TIL-Blog/posts/til-os-linux-the-concept-of-sysvinit-and-the-difference-from-systemd)

<br>
<br>
<br>

<!-- ## Footnote
---
> <a name="footnote_1">ⓐ</a> 

<br>
<br>
<br> -->

## Reference
---
- [Linux systemd 완전 정복하기](https://cumulus.tistory.com/158)
- [What is SystemD on Linux?](https://linuxtldr.com/systemd-linux/)
- [Systemd Vs Init for Linux Beginners (Final Verdict)](https://linuxtldr.com/init-vs-systemd/)
- [1. Working with systemd unit files](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html/using_systemd_unit_files_to_customize_and_optimize_your_system/assembly_working-with-systemd-unit-files_working-with-systemd)
- [[Linux] systemd 은 뭐하는 아이 일까?](https://coffeebaralog.tistory.com/79)
- [systemd의 의존성 관리와 서비스 시작 순서 분석](https://inpoblgdr.com/systemd/)

<br>

[^1]: 출처: https://machaddr.substack.com/p/systemd-sysvinit-runit-and-openrc
