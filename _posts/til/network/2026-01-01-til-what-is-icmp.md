---
title: ICMP란?
description: ICMP(Internet Control Message Protocol) 란 무엇인가?
author: bin
date: 2026-01-01 09:00:00 +0800
categories: [TIL, Network]
tags: [Network, Protocol, ICMP]
pin: true
math: true
mermaid: true
image:
 path: https://bangjeongbin.github.io/TIL-Blog/assets/img/posts/common/til-logo.png
 alt: Today I Learnd
---

![icmp image](https://img.stibee.com/83505_1712292356.png)

ICMP란?[^1]
## ICMP란 무엇인가?
---
ICMP란 Internet Control Message Protocol의 약자로 **"인터넷 제어 메시지 프로토콜"**이라고 한다. OSI 3 Layer의 장치에서 <u>네트워크 통신 문제를 진단하는 데 사용하는 Protocol</u>이다. 

일반적으로 발신자와 수신자 간에 메시지를 교환할 때 예상치 못한 오류가 발생하는 경우가 있다. 예를 들어 메시지가 너무 길거나 데이터 패킷이 순서에 맞지 않게 도착하여 수신자 측에서 메시지를 조합하지 못할 수도 있다. 이러한 경우에 **수신자는 ICMP를 사용하여 발신자에게 오류 메시지를 알리고 메시지 재전송을 요청**한다.

<br>

## ICMP의 용도
---
ICMP는 라우터와 엔드포인트 디바이스를 비롯하여 네트워크에 연결된 모든 디바이스가 ICMP 메시지를 처리할 수 있다. 또한 ICMP는 IPv4와 IPv6 모두에서 작동한다.

일반적인 ICMP의 용도는 **2가지** 정도가 있다.


### 1. 오류보고
---
인터넷을 통해 두 개의 장치가 연결될 때마다 ICMP를 사용하여 <u>일부 데이터가 예상대로 도착하지 않은 경우 수신 장치에서 전송 장치로 이동할 수 있는 오류를 생성</u>한다. 예를 들어, 데이터 패킷이 라우터에 비해 너무 큰 경우. 이럴 때 라우터는 데이터 패킷을 폐기하고 ICMP 메시지를 발신자에게 전송하여 문제를 알린다.

ICMP 오류 메시지는 연결할 수 없는 대상, 시간 초과 또는 조각화(Fragmentation) 문제와 같은 네트워킹 오류를 보고한다. 이 메시지는 비연결 통신 모델을 사용하는 사용자 데이터그램 프로토콜(UDP)에 있어서 특히 중요하다.

UDP는 안정적이고 순차적인 패킷 전송을 제공하지 않는데 UDP 패킷이 전송된 경우 패킷이 손실되었거나, 체크섬 오류 같은 오류와 함께 전송된 것일 수 있습니다. 이 경우 수신자는 ICMP 오류 보고 메시지를 발신자에게 다시 보내 문제를 알린다.

<br>

### 2. 네트워크 진단
---
ICMP는 **ping** 및 **traceroute** 명령에 가장 많이 사용된다.

- **ping 명령**은 traceraute의 단순화 버전으로 ICMP <u>에코 요청 패킷을 대상 디바이스에 전송하여 네트워크 디바이스의 연결 가능 여부를 테스트</u> 한다. 두 장치 간의 연결 속도를 테스트하고 데이터 패킷이 대상에 도달하고 발신자의 장치로 돌아오는 데 걸리는 시간(**RTT, Round Trip Time**)을 정확히 보고. 디바이스에 연결할 수 있는 경우 ICMP 에코 응답을 반환. 높은 신뢰도로 네트워크 지연 시간을 검사하고 디바이스가 사용 가능한 상태인지 확인한다.

- **traceroute 명령**은 <u>소스에서 대상까지 패킷이 이동하는 라우팅 경로를 추적</u>한다. 라우팅 경로는 요청이 대상에 도달하기 전에 통과해야 하는 연결된 라우터의 실제 물리적 경로를 뜻한다. 한 라우터와 다른 라우터 간의 여정을 **'hop'**이라고 하며, traceroute는 여정 중 각 hop에 필요한 시간도 보고한다. 이는 네트워크 지연의 원인을 확인하는 데 유용하다. 이를 위해 이 명령은 에코 요청 및 에코 응답 메시지를 해당 대상에 보낸다.

에코 요청에는 패킷이 라우터를 통과할 때마다 1씩 감소하는 **TTL(Time to Live)** 값이 포함되는데 TTL이 0인 라우터에 패킷이 도달하면, 해당 라우터는 ICMP 메시지를 소스로 다시 보낸다.

<br>

## ICMP의 작동방식
---
ICMP는 일반적으로 TCP/IP 또는 UDP와 같은 <u>다른 네트워크 프로토콜과 함께 작동</u>. 호스트와 라우터는 특정 네트워크 이벤트가 발생할 때 **ICMP 메시지 또는 ICMP 패킷을 교환**한다.

ICMP 패킷은 일반 IP 헤더 뒤에 ICMP 헤더를 포함한다. 라우터나 서버가 오류 메시지를 보내야 하는 경우, ICMP 패킷 본문 또는 데이터 섹션에는 항상 오류를 일으킨 패킷의 IP 헤더 사본이 포함된다.

ICMP **패킷은 ICMP 패킷 헤더**와 **ICMP 데이터 섹션**으로 구성되어 있다.

![When Are ICMP Redirects Sent](https://www.cisco.com/c/dam/en/us/support/docs/ip/routing-information-protocol-rip/13714-43-01.gif)

ICMP의 작동방식 [^2]

<br>

### ICMP 패킷 헤더
---
ICMP 헤더에는 패킷 유형, 코드, 체크섬 및 식별자에 대한 정보가 들어 있다. ICMP 패킷이 전송되면 메시지 수신자가 헤더 정보를 읽고, 패킷의 유형에 따라 적절한 작업을 수행한다.


### ICMP 데이터 섹션
---
ICMP 메시지의 데이터 섹션에는 대상의 IP 주소 또는 장애 원인과 같은 정보가 들어 있다. 또한 오류를 식별하는 오류 코드 또는 숫자 코드도 들어 있다.

<br>

## ICMP를 이용한 DDos 공격
---
![icmp flood attack](https://www.cloudflare.com/img/learning/ddos/ping-icmp-flood-ddos-attack/ping-icmp-flood-ddos-attack-diagram.png)

ICMP Flooding 방법 [^3]

### ICMP Flooding
---
ICMP 에코 요청 패킷으로 대상 장치를 압도하려고 시도하는 경우이다. 대상은 각 패킷을 처리하고 응답해야 하며, 컴퓨팅 리소스를 소비하여 나중에는 합법적인 사용자가 서비스를 받을 수 없게 된다.

### Ping of Death
---
공격자가 패킷에 허용되는 최대 크기(MTU)보다 큰 ping을 대상 시스템에 보내 시스템이 정지하거나 충돌하게 만드는 경우이다. 패킷은 대상으로 가는 도중에 분할되지만, 대상에서 패킷이 원래의 최대 초과 크기로 재조립되면 패킷 크기로 인해 버퍼 오버플로가 발생.

### SMURF 공격
---
공격자는 스푸핑된 소스 IP 주소가 있는 ICMP 패킷을 보낸다. 네트워킹 장비는 패킷에 응답하여 스푸핑된 IP에 응답을 보내고 원치 않는 ICMP 패킷으로 피해 장비를 폭주시킨다.

<br>

<!-- ## Related Posts
---
- 

<br> -->

## Reference
---
- [ICMP란 무엇인가요? - AWS](https://aws.amazon.com/ko/what-is/icmp/)
- [인터넷 제어 메시지 프로토콜(ICMP)이란? - Cloudflare](https://www.cloudflare.com/ko-kr/learning/ddos/glossary/internet-control-message-protocol-icmp/)
- [ICMP(인터넷 제어 메시지 프로토콜) - Fortinet](https://www.fortinet.com/kr/resources/cyberglossary/internet-control-message-protocol-icmp)

[^1]: 출처 : https://stibee.com/api/v1.0/emails/share/4WYO3IaUVak7EcDbUBu_x_hSqueKmrs
[^2]: 출처 : https://www.cisco.com/c/en/us/support/docs/ip/routing-information-protocol-rip/13714-43.html
[^3]: 출처 :https://www.cloudflare.com/ko-kr/learning/ddos/glossary/internet-control-message-protocol-icmp/
