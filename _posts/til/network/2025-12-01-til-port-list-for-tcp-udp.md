---
title: TCP/UDP의 자주 사용되는 포트 목록
description: 자주 사용되는 포트 목록들과 그 분류
author: bin
date: 2025-12-01 09:00:00 +0800
categories: [TIL, Network]
tags: [Network, Port, TCP, UDP]
pin: true
math: true
mermaid: true
image:
 path: https://bangjeongbin.github.io/TIL-Blog/assets/img/posts/common/til-logo.png
 alt: Today I Learnd
---

## 포트의 분류
---
#### 잘 알려진 포트 (Well-Known Port)
- 범위: 0 ~ 1023
- 특징: **System Port**, 인터넷 표준화 기관(IANA)에 의해 특정 서비스(예: 웹, 이메일, 원격 접속)에 미리 할당되어 있디.

<br>
#### 등록된 포트 (Registered Port)
- 범위: 1024 ~ 49151
- 특징: **User Port**, 특정 애플리케이션이나 서비스에 의해 등록되어 사용되는 포트이다. 잘 알려진 포트보다 덜 보편적이지만, 특정 소프트웨어(예: 데이터베이스, 게임)에서 자주 사용. 

<br>

#### 동적/개인 포트 (Dynamic/Private Port)
- 범위: 49152 ~ 65535
- 특징: **Private Port**, 임시 포트로, 사용자가 애플리케이션을 실행할 때 동적으로 할당되거나 개인적인 용도로 사용. 클라이언트 프로그램이 서버에 접속할 때 주로 사용한다. 

<br>

## 자주 사용되는 포트 목록
----

| 포트 번호    | 프로토콜    | 서비스명       | 설명                                                                                            |
| -------- | ------- | ---------- | --------------------------------------------------------------------------------------------- |
| 20, 21   | TCP     | FTP        | File Transfer Protocol. 20번은 데이터 전송, 21번은 제어 연결에 사용. 파일 업로드/다운로드 서비스. **암호화되지 않아 크리덴셜 노출 위험** |
| 22       | TCP     | SSH        | Secure Shell. 암호화된 원격 접속 및 파일 전송(SFTP, SCP) 서비스                                               |
| 23       | TCP     | Telnet     | 암호화되지 않은 원격 접속 프로토콜. 보안상 취약하여 현재는 SSH로 대체. **암호화되지 않아 크리덴셜 노출 위험**                            |
| 25       | TCP     | SMTP       | Simple Mail Transfer Protocol. 이메일 송신에 사용                                                     |
| 53       | TCP/UDP | DNS        | Domain Name System. 도메인 이름을 IP 주소로 변환. UDP가 주로 사용되며, 512바이트 이상일 때 TCP 사용                      |
| 67, 68   | UDP     | DHCP       | Dynamic Host Configuration Protocol. IP 주소 자동 할당. 67번은 서버, 68번은 클라이언트                         |
| 80       | TCP     | HTTP       | Hypertext Transfer Protocol. 암호화되지 않은 웹 트래픽                                                   |
| 110      | TCP     | POP3       | Post Office Protocol v3. 이메일 수신 프로토콜 (메일 다운로드)                                                |
| 123      | UDP     | NTP        | Network Time Protocol. 시스템 시간 동기화                                                             |
| 143      | TCP     | IMAP       | Internet Message Access Protocol. 이메일 수신 프로토콜 (서버에 메일 보관)                                     |
| 161, 162 | UDP     | SNMP       | Simple Network Management Protocol. 네트워크 장비 모니터링 및 관리. 161번은 에이전트, 162번은 트랩                   |
| 389      | TCP/UDP | LDAP       | Lightweight Directory Access Protocol. 디렉토리 서비스 접근                                            |
| 443      | TCP     | HTTPS      | HTTP Secure. SSL/TLS로 암호화된 웹 트래픽                                                              |
| 445      | TCP     | SMB        | Server Message Block. Windows 파일 및 프린터 공유. WannaCry 랜섬웨어 공격 경로로 유명                            |
| 465, 587 | TCP     | SMTPS      | SMTP over SSL/TLS. 암호화된 이메일 송신. 587번이 표준                                                      |
| 514      | UDP     | Syslog     | 시스템 로그 메시지 전송 프로토콜                                                                            |
| 636      | TCP     | LDAPS      | LDAP over SSL. 암호화된 LDAP                                                                      |
| 993      | TCP     | IMAPS      | IMAP over SSL. 암호화된 IMAP                                                                      |
| 995      | TCP     | POP3S      | POP3 over SSL. 암호화된 POP3                                                                      |
| 1433     | TCP     | MS SQL     | Microsoft SQL Server 데이터베이스                                                                   |
| 1521     | TCP     | Oracle DB  | Oracle Database 기본 리스너 포트                                                                     |
| 3306     | TCP     | MySQL      | MySQL/MariaDB 데이터베이스                                                                          |
| 3389     | TCP     | RDP        | Remote Desktop Protocol. Windows 원격 데스크톱 연결. **무차별 대입 공격(Brute Force)의 주요 타겟**                |
| 5432     | TCP     | PostgreSQL | PostgreSQL 데이터베이스                                                                             |
| 5900     | TCP     | VNC        | Virtual Network Computing. 원격 데스크톱 제어                                                         |
| 6379     | TCP     | Redis      | Redis 인메모리 데이터베이스                                                                             |
| 8080     | TCP     | HTTP-Alt   | HTTP 대체 포트. 웹 프록시, 개발 서버 등에 사용                                                                |
| 27017    | TCP     | MongoDB    | MongoDB 데이터베이스                                                                                |

<br>

<!-- ## Related Posts
---
- 

<br> -->

## Reference
---
- [TCP/UDP의 포트 목록 - Wikipedia](https://ko.wikipedia.org/wiki/TCP/UDP%EC%9D%98_%ED%8F%AC%ED%8A%B8_%EB%AA%A9%EB%A1%9D)
- [포트(Port)의 종류](https://m.blog.naver.com/zerogo/220738577430)
