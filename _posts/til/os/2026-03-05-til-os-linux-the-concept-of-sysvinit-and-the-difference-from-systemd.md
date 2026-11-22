---
title: "[Linux] SysVinit의 개념과 systemd와의 차이"
description: 리눅스의 init 프로세스인 SysVinit의 개념 및 전통의 SysVinit과 systemd의 차이점
author: bin
date: 2026-03-05 09:00:00 +0800
categories: [TIL, OS, Linux]
tags: [OS, Linux, Process, init, SysVinit, systemd]
pin: false
math: true
mermaid: true
image:
 path: https://petermartin.nl/media/yootheme/cache/46/sysv-init-46b31076.webp?src=images/focus-on/linux/sysv-init.jpg&type=webp,85&hash=022bcf9d
 alt: Today I Learnd
---
_리눅스  SysVinit 이미지[^1]_
{: .text-center }

<br>

## 𝙸. Linux Boot Process
---

![linux init process](https://linuxtldr.com/wp-content/uploads/2022/12/init-process-1024x710.webp)
_리눅스의 부팅 순서[^2]_
{: .text-center }

<br>

리눅스에 부팅 후 `ps`나 `systemctl`을 입력하면 이미 수십 개의 서비스가 떠 있는 것을 볼 수 있다. (물론 윈도우에 비하면 확연히 적음)

<br>

**Linux Boot Process**

1. **BIOS / UEFI**
	- 컴퓨터의 전원을 켜고 하드웨어를 초기화한 후 부트로더를 실행

2. **Bootloader (GRUB 등)**
	- 리눅스 커널을 메모리에 적재하고 실행

3. **Kernel**
	- 하드웨어와 메모리 등을 초기화하고 필요한 드라이버를 로드

4. **init 프로세스 (PID 1)**
	- 최초의 사용자 공간 프로세스로, 시스템 초기화와 서비스 실행을 담당함

5. **시스템 서비스 실행**
	- 네트워크, SSH, 로깅, 웹 서버 등 필요한 서비스를 실행

6. **로그인 환경 제공**
	- 콘솔 로그인이나 그래픽 로그인 환경을 제공

<br>
<br>
<br>
<br>
<br>

## 𝙸𝙸. 첫 프로세스 init (PID 1)
---

 또한 `ps aux` 명령어를 입력하면 제일 상단에 PID 1번으로 `/sbin/init`이 수행된 것을 볼 수 있는데 이게 바로 init process이다.

![linux ps command](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F23376B4F5718D0272B)
_ps aux 명령어[^3]_
{: .text-center }

<br>

처음 커널은 하드웨어를 초기화하고 루트 파일시스템을 마운트한 뒤, 마지막으로 <u>사용자 영역의 프로그램 하나를 실행하는데 이것이 init이며 당연하게도 프로세스 번호(PID)는 항상 1번을 할당받는다.</u> 이후 시스템에 존재하는 모든 프로세스는 직간접적으로 이 프로세스의 자식이 된다.

init 프로세스의 주요 역할은 다음과 같다.

- **시스템 부팅 과정에서 필요한 초기화 작업 수행**

- **시스템 서비스 및 데몬 실행**
    
- **시스템 종료 및 재부팅 관리**
    
- **고아 프로세스의 재부모 지정 및 자식 프로세스 회수(reaping)**

<br>

init의 구현은 시대에 따라 바뀌어 왔는데 오랫동안 표준이었던 것이 **SysVinit**이고, 지금의 Ubuntu나 RHEL 계열 같은 주요 배포판은 **systemd**를 사용한다. 현대 시스템에서 `/sbin/init`은 systemd를 가리키는 심볼릭 링크인 경우가 많아서, <u>사실상 init이 곧 systemd라고 보면 된다.</u>

<br>

> **개념 정리**    
> 리눅스에서 init은 커널 부팅 후 가장 먼저 실행되는 PID 1 사용자 공간 프로세스(초기화 시스템 개념)를 뜻하고, SysVinit와 systemd는 그중 전통적인 구현체 중 하나를 말한다.
> 즉, init은 상위 개념(역할/프로세스)이고 SysVinit와 systemd는 구체적인 구현 방식을 말한다.
{: .prompt-tip }

<br>
<br>
<br>
<br>
<br>

## 𝙸𝙸𝙸. SysVinit (System V init)
---
SysVinit(System V init)은 전통적인 유닉스 System V 방식에서 유래한 초기화 시스템으로, CentOS 기준으로는 6버전 이하에서 주로 사용됐으며 현재 대부분의 리눅스 배포판에서는 `systemd`가 채택되었다.

SysVinit는 리눅스 부팅 시 init 프로세스가 실행되면 설정 파일을 확인하고, 지정된 순서에 따라 시스템 서비스를 실행하는 구조로 되어있다. 또한 SysVinit는 시스템의 동작 상태를 **런레벨(runlevel)** 이라고 하는 번호로 구분하는 특성을 가지고 있다. 또한 각 상태로 진입하거나 종료하기 위해 실행하는 **셸 스크립트** 디렉터리를 사용한다.

대표적인 파일과 디렉터리는 다음과 같다.

|            **경로**            | **설명**                                              |
| :--------------------------: | --------------------------------------------------- |
|        `/etc/inittab`        | - 초기화 설정 및 기본 Runlevel 지정<br>- 각 Runlevel 에서의 행동 지정 |
|        `/etc/init.d/`        | - 서비스 실행 및 종료 스크립트<br>- 서비스당 하나의 스크립트가 존재           |
| `/etc/rcN.d/`<br>(N는 런레벨 번호) | - Runlevel별 서비스 실행 설정                               |
|         `/etc/rc.d/`         | - 일부 배포판에서 사용하는 초기화 스크립트 경로                         |

<br>
<br>

### Runlevel
---
`Runlevel`은 시스템이 어떤 운영 상태로 동작할지 구분하는 실행 단계로 다음과 같다.

| **런레벨** |          **의미**           |   **systemd 대응**    |
| :-----: | ----------------------- | :-----------------: |
|    **0**    |          시스템 종료           |  `poweroff.target`  |
|    **1**    |    단일 사용자 모드(복구·안전 모드)    |   `rescue.target`   |
|    **2**    |    다중 사용자, 네트워크 서비스 제외    |      배포판마다 상이       |
|    **3**    | 다중 사용자 + 네트워크 (CLI 서버 환경) | `multi-user.target` |
|    **4**    |       미사용(사용자 정의용)        |          -          |
|    **5**    |       다중 사용자 + GUI        | `graphical.target`  |
|    **6**    |            재부팅            |   `reboot.target`   |

<br>

> **Tip**    
> Runlevel 2, 3, 4, 5번의 의미는 배포판에 따라 세부 정의가 조금씩 다르게 구성될 수 있다.
{: .prompt-tip }

<br>
<br>

### /etc/rcX.d/ 와 S/K 스크립트
---
SysVinit는 각 서비스의 실행 및 종료를 쉘 스크립트로 관리하는데 각 서비스 스크립트는 일반적으로 다음과 같은 인자를 지원한다.

```bash
/etc/init.d/sshd start
/etc/init.d/sshd stop
/etc/init.d/sshd restart
```

<br>

또한 각 런레벨에서 실행할 서비스는 `/etc/rcN.d/` 디렉터리에 모여 있는데 이 디렉터리 안의 파일은 실제 스크립트가 아니라 `/etc/init.d/`에 있는 스크립트를 가리키는 **심볼릭 링크**로 존재할 수 있다.

```bash
# ls -l /etc/rc5.d/
S01cron -> ../init.d/cron
K01speech-dispatcher -> ../init.d/speech-dispatcher
```

<br>

여기서 보면 파일명의 앞 글자가 `S`, `K`의 알파벳으로 이루어져 있고 그 바로 뒤에 `숫자`가 오는 형태로 이루어진 것을 확인할 수 있는데 여기에는 규칙이 존재한다.

- `S`: Start, 해당 런레벨에 진입할 때 서비스를 시작한다.
    
- `K`: Kill, 서비스를 종료한다.
    
- `숫자`: 스크립트 실행 순서이며, 숫자가 같으면 이름순으로 처리된다.

<br>

이러한 SysVinit는 <u>쉘 스크립트 기반으로서 구조가 단순하고 이해하기 쉽다는 장점</u>이 있지만, 서비스를 <u>하나씩 차례로 실행하기 때문에 부팅이 느리고, 서비스 사이의 의존 관계를 init이 알지 못해서 순서를 사람이 파일 이름의 숫자로 맞춰 줘야 한다는 제한적</u>이라는 큰 단점이 존재한다.

<br>
<br>
<br>
<br>
<br>

## 𝙸𝚅. SysVinit, systemd 차이점
---
SysVinit은 Runlevel과 `/etc/rcN.d/`의 `S` / `K` 스크립트를 순차 실행하는 단순한 구조인데 반해 systemd는 유닛 파일과 의존성 선언으로 병렬 부팅, 서비스 감시, 중앙 로그까지 강력한 기능들을 제공한다.

이렇듯 systemd의 기능이 SysVinit 구현 방식보다 더 좋은 상황이 많아 현대의 Linux 배포판들은 systemd 방식을 채택하는 경우가 많다.

|  **항목**   | **SysVinit**       | **systemd**                     |
| :-------: | ------------------ | ------------------------------- |
| 서비스 기동 방식 | 스크립트를 순차 실행        | 의존성을 계산해 병렬 실행                  |
|   부팅 속도   | 상대적으로 느림           | 상대적으로 빠름                        |
|  의존성 관리   | 없음 (번호로 수동 조절)     | Wants / Requires / After 등으로 선언 |
|   설정 방식   | bash 스크립트          | 선언형 유닛 파일                       |
|    로그     | 서비스별 로그 파일에 제각각 기록 | journald가 모아서 `journalctl`로 조회  |
|  서비스 감시   | 직접 구현해야 함          | `Restart=` 옵션으로 자동 재시작          |
|   자원 제어   | 별도 도구 필요           | cgroup 기반으로 유닛에서 제한 가능          |

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
- [[Linux] systemd란?](https://bangjeongbin.github.io/TIL-Blog/posts/til-os-linux-what-is-systemd)

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
- [Linux concept: SysV init](https://petermartin.nl/en/focus-on/linux/sysv-init)
- [What is ‘init’ Process and Command on Linux?](https://linuxtldr.com/init-linux/)
- [What is SystemD on Linux?](https://linuxtldr.com/systemd-linux/)
- [1. Working with systemd unit files](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html/using_systemd_unit_files_to_customize_and_optimize_your_system/assembly_working-with-systemd-unit-files_working-with-systemd)

<br>

[^1]: 출처: https://petermartin.nl/en/focus-on/linux/sysv-init
[^2]: 출처: https://linuxtldr.com/init-linux/
[^3]: 출처: https://talkingaboutme.tistory.com/entry/Linux-init-process
