---
title: "[Online Academy] \"리눅스 기초 강의\" Note-Taking"
description: "[Online Academy] 리눅스 기초 강의 공부기록"
author: bin
date: 2025-12-19 09:00:00 +0800
categories: [Review, Note-Taking]
tags: [Linux]
pin: true
math: true
mermaid: true
image:
 path: https://bangjeongbin.github.io/TIL-Blog/assets/img/posts/common/note-taking-logo.png
 alt: Note Taking
---

> 해당 포스트는 학습 목적으로 작성되었으며 <<[리눅스 기초 강의](https://academy.segfaulthub.com)>>을 참고하여 작성하였음을 알려드립니다.

<br>

## 1. 기본 개념
---
### 프로세스 식별자

- **PID**: Process ID (프로세스 ID)
- **PPID**: Parent Process ID (부모 프로세스 ID)

### 명령어 구조

```
[명령어] [전달인자] [옵션]
```

**예시:**

```bash
ping 8.8.8.8 -c 3
```

- `ping`: 명령어 (필수, 항상 맨 앞)
- `8.8.8.8`: 전달인자
- `-c 3`: 옵션 (위치 변경 가능, 생략 가능)

**옵션 확인:** `명령어 -h`

<br>

## 2. 경로 표현
---
### 특수 경로 기호

- `/`: 최상위 경로(루트)
- `~`: 홈 디렉토리
- `.`: 현재 디렉토리
- `..`: 상위 디렉토리

### 경로 유형

**절대경로**

- 최상위 디렉토리부터 전체 경로 표현
- `/etc/passwd`, `/root`

**상대경로**

- 현재 위치 기준 경로 표현
- `./경로`, `../경로`

<br>

## 3. 파일 시스템 구조
---

|디렉토리|설명|
|---|---|
|`/bin`|기본 명령어 바이너리 파일|
|`/dev`|하드웨어 장치 파일|
|`/etc`|시스템 설정 파일|
|`/home`|사용자 홈 디렉토리|
|`/lib`|공유 라이브러리 파일|
|`/root`|root 계정 홈 디렉토리|
|`/sbin`|시스템 관리 명령어|
|`/tmp`|임시 파일 (재부팅 시 삭제)|
|`/var`|가변 데이터 파일|

<br>

## 4. 파일 확인 명령어
---
```bash
cat [파일명]         # 파일 내용 출력
file [파일명]        # 파일 정보 확인
more [파일명]        # 페이지 단위로 파일 보기
ls -l [파일명]       # 파일 상세 정보 및 권한 확인
```

**파일 타입 구분:**

- `-`: 일반 파일
- `d`: 디렉토리

<br>

## 5. 파일 조작 명령어
---
### 복사 (Copy)

```bash
# 파일 복사
cp [원본] [대상]
cp [원본] [대상]/[새이름]

# 디렉토리 복사
cp -r [원본] [대상]
```

### 이동/이름변경 (Move)

```bash
# 파일 이동
mv [원본] [대상]
mv [원본] [대상]/[새이름]

# 디렉토리 이동
mv [원본] [대상]
```

### 삭제 (Remove)

```bash
# 파일 삭제
rm [파일명]

# 디렉토리 삭제
rm -r [디렉토리명]

# 강제 삭제
rm -rf [대상]
```

<br>

## 6. Vi 에디터
---
### 모드

- **명령모드**: 기본 모드
- **입력모드**: `i`, `a`, `o` 등으로 진입

### 주요 명령

```
/[검색어]     # 검색
n            # 다음 검색 결과
N            # 이전 검색 결과
:[줄번호]     # 특정 줄로 이동
dd           # 현재 줄 삭제
[숫자]dd      # 지정 줄 수만큼 삭제
:wq          # 저장 후 종료
:q!          # 강제 종료
```

<br>

## 7. 사용자 및 권한
---
### 사용자 관리

```bash
useradd [사용자명]    # 사용자 생성
exit                 # 현재 세션 종료
```

### /etc/passwd 구조

```
root:x:0:0:root:/root:/usr/bin/zsh
```

순서대로:

1. 계정 이름
2. 비밀번호 (x = 숨김, 실제는 /etc/shadow)
3. UID (User ID)
4. GID (Group ID)
5. 사용자 설명
6. 홈 디렉토리
7. 기본 셸

<br>

## 8. 권한 (Permission)
---
### 권한 종류

- **r (read, 4)**: 읽기
    - 파일: 파일 내용 읽기
    - 디렉토리: 디렉토리 내용 확인
- **w (write, 2)**: 쓰기
    - 파일: 파일 수정
    - 디렉토리: 파일/디렉토리 생성
- **x (execute, 1)**: 실행
    - 파일: 파일 실행
    - 디렉토리: 디렉토리 접근(cd)

### 권한 표기 해석

```
-rw-r--r-- 1 root root 20 Apr 25 21:42 test
```

- `-`: 파일 타입
- `rw-`: 소유자 권한
- `r--`: 그룹 권한
- `r--`: 기타 사용자 권한
- `1`: 하드링크 수
- `root`: 소유자
- `root`: 그룹
- `20`: 파일 크기(byte)
- `Apr 25 21:42`: 수정 날짜
- `test`: 파일명

### 권한 변경 (chmod)

**기호 방식:**

```bash
chmod u+x [파일]    # 소유자에게 실행 권한 추가
chmod g-w [파일]    # 그룹에서 쓰기 권한 제거
chmod o+r [파일]    # 기타 사용자에게 읽기 권한 추가
```

- `u`: 소유자 (user)
- `g`: 그룹 (group)
- `o`: 기타 사용자 (others)

**숫자 방식:**

```bash
chmod 644 [파일]    # rw-r--r--
chmod 755 [파일]    # rwxr-xr-x
chmod 777 [파일]    # rwxrwxrwx
```

<br>

## 9. 특수 권한
---
### SetUID

```
-rwsr-xr-x
```

- 파일 실행 시 소유자 권한으로 실행
- `s`: 실행 권한 있음 + SetUID
- `S`: 실행 권한 없음 + SetUID

### SetGID

```
-rwxr-sr-x
```

- 파일 실행 시 그룹 권한으로 실행
- `s`: 실행 권한 있음 + SetGID
- `S`: 실행 권한 없음 + SetGID

### Sticky Bit

```
drwxrwxrwt
```

- 공유 디렉토리에 주로 사용
- 누구나 파일 생성 가능, 삭제는 소유자만 가능
- 예: `/tmp` 디렉토리
- `t`: 실행 권한 있음 + Sticky Bit
- `T`: 실행 권한 없음 + Sticky Bit

<br>

## 10. 데이터 스트림 & 리다이렉션
---
### 표준 스트림

- **0**: 표준 입력 (stdin)
- **1**: 표준 출력 (stdout)
- **2**: 표준 에러 (stderr)

### 리다이렉션

**출력 리다이렉션:**

```bash
pwd > result.txt          # 출력을 파일로 저장 (덮어쓰기)
pwd >> result.txt         # 출력을 파일에 추가
```

**에러 리다이렉션:**

```bash
find / -name "test" 2> error.log     # 에러만 파일로 저장
find / -name "test" 2> /dev/null     # 에러 메시지 무시
```

### 파이프 (Pipe)

```bash
명령어A | 명령어B
```

명령어A의 출력을 명령어B의 입력으로 전달

**예시:**

```bash
ifconfig | grep inet
ls /bin | grep "find"
cat /etc/passwd | wc -l
```

<br>

## 11. 실무 활용 예시
---
### 시스템 파일 검색

```bash
find / -name "rockyou.txt.gz" 2> /dev/null
```

### 네트워크 정보 필터링

```bash
ifconfig | grep inet
```

### 특정 권한 파일 찾기

```bash
find / -perm -4000 2> /dev/null    # SetUID 파일 찾기
```

### 로그 실시간 모니터링

```bash
tail -f /var/log/syslog | grep error
```

<br>

## Related Posts
---
- 

<br>

## References
---
- [Segfault Academy](https://academy.segfaulthub.com)
