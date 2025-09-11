---
title: HTTP란 무엇인가?
description: HTTP의 정의와 구조 설명
author: bin
date: 2025-05-05 09:00:00 +0800
categories: [TIL, Web]
tags: [Web, session, cookie]
pin: false
math: true
mermaid: true
image:
 path: https://bangjeongbin.github.io/TIL-Blog/assets/img/posts/common/http-main-image.png
 alt: Baekjoon Online Judge
---

## HTTP 개요
---
HTTP는 "**H**yper**T**ext **T**ransfer **P**rotocol"의 약자로 월드 와이드 웹의 토대이며 하이퍼텍스트 링크를 사용하여 HTML 문서와 같은 리소스들을 가져오고 웹 페이지를 로드하는 데 사용되는 프로토콜입니다. 

HTTP는 네트워크 장치 간에 정보를 전송하도록 설계된 애플리케이션 계층 프로토콜이며 네트워크 프로토콜 스택의 다른 계층 위에서 실행됩니다. HTTP를 통한 일반적인 흐름에는 클라이언트 시스템에서 서버에 요청한 다음 서버에서 응답 메시지를 보내는 작업이 포함됩니다.

HTTP는 웹에서 이루어지는 모든 데이터 교환의 기초이며, 클라이언트-서버 프로토콜이기도 합니다. 클라이언트-서버 프로토콜이란 (보통 웹브라우저인) 수신자 측에 의해 요청이 초기화되는 프로토콜을 의미합니다. 하나의 완전한 문서는 텍스트, 레이아웃 설명, 이미지, 비디오, 스크립트 등 불러온(fetched) 하위 문서들로 재구성됩니다.

![Web Document](https://mdn.github.io/shared-assets/images/diagrams/http/overview/fetching-a-page.svg)
Web Document[^1]

![How the Web Works](https://velog.velcdn.com/images/andy3400/post/632ce2c9-37df-4348-8c48-1cfefbea10bd/image.png)
Web의 작동 원리[^3]

<br>

### HTTP 헤더
---
HTTP 헤더는 클라이언트와 서버가 요청 또는 응답으로 부가적인 정보를 전송할 수 있도록 해줍니다. HTTP 헤더는 대소문자를 구분하지 않는 이름과 콜론 ':' 다음에 오는 값(줄 바꿈 없이)으로 이루어져있습니다. 값 앞에 붙은 빈 문자열은 무시됩니다.

![Google Chrome header](https://www.cloudflare.com/img/learning/ddos/glossary/hypertext-transfer-protocol-http/http-request-headers.png)
Google Chrome header의 헤더 예[^2]

종단간 헤더는 반드시 메시지의 최종 수신자에게 전송되어야 합니다. 즉, 요청에 대해서는 서버, 응답에 대해서는 클라이언트입니다. 중간 프록시는 반드시 종단 간 헤더를 수정되지 않은 상태로 재전송해야하며 캐시는 이를 반드시 저장해야합니다.

<br>

### HTTP 세션
---
HTTP와 같은 클라이언트-서버 프로토콜에서, 세션은 다음의 세 가지 과정으로 이루어집니다.

1. 클라이언트가 TCP 연결을 수립합니다(또는 전송 계층이 TCP가 아닌 다른 적당한 연결로).
2. 클라이언트는 요청을 전송한 뒤 응답을 기다립니다.
3. 서버는 요청에 대해 처리하고 그에 대한 응답을 상태 코드 그리고 요청에 부합하는 데이터와 함께 돌려보냅니다.

>HTTP/1.1부터는 세번째 과정 이후 클라이언트가 해당 시점에 또 다른 요청을 보낼 수 있도록 연결을 더 이상 닫지 않습니다. 그러므로 두번째, 세번째 과정이 몇 번에 걸쳐 일어날 수 있습니다

<br>

#### 연결 수립
---
클라이언트-서버 프로토콜에, 클라이언트는 연결을 수립합니다. HTTP에서 연결을 여는 것은 보통의 경우 TCP인 기본적인 전송 계층 내에서 연결을 수립하는 것을 뜻합니다.

TCP를 이용할 경우, 컴퓨터 상의 HTTP 서버를 위한 기본 포트는 80인데 8000 혹은 8080처럼 다른 포트들도 자주 사용되곤 합니다. 요청을 위한 페이지 URL은 도메인 이름과 포트 번호 둘 다 포함하지만 포트 번호가 80일 경우 생략 가능합니다.

<br>

#### 요청 예
---
[develper.mozilla.org](https://developer.mozilla.org/)의 최상위 페이지를 가져오도록 요청하고, 가능하다면 서버에게 사용자-에이전트가 해당 페이지에 대해 프랑스어로 된 페이지를 원한다고 알려줍니다.

```
GET / HTTP/1.1
Host: developer.mozilla.org
Accept-Language: fr
```

헤더 블록으로부터 데이터 블록을 구분짓는 첫번째 빈줄에 주목하세요. 헤더 중에 `Content-Length:` 헤더가 없으므로, 데이터 블록은 비어있고 서버는 헤더의 마지막을 나타내는 빈 줄을 받는 즉시 요청을 처리할 수 있습니다.

다음은 결과 전송 형식입니다.

```
POST /contact_form.php HTTP/1.1
Host: developer.mozilla.org
Content-Length: 64
Content-Type: application/x-www-form-urlencoded

name=Joe%20User&request=Send%20me%20one%20of%20your%20catalogue
```

<br>

#### 응답 예
---
성공적인 수신 `200 OK`
```
HTTP/1.1 200 OK
Date: Sat, 09 Oct 2010 14:28:02 GMT
Server: Apache
Last-Modified: Tue, 01 Dec 2009 20:18:22 GMT
ETag: "51142bc1-7449-479b075b2891b"
Accept-Ranges: bytes
Content-Length: 29769
Content-Type: text/html

<!DOCTYPE html... (here comes the 29769 bytes of the requested web page)
```

<br>

요청 자원이 영구적으로 옮겨졌다는 내용의 알림 `301 Moved Permanently`
```
HTTP/1.1 301 Moved Permanently
Server: Apache/2.2.3 (Red Hat)
Content-Type: text/html; charset=iso-8859-1
Date: Sat, 09 Oct 2010 14:30:24 GMT
Location: https://developer.mozilla.org/ (this is the new link to the resource; it is expected that the user-agent will fetch it)
Keep-Alive: timeout=15, max=98
Accept-Ranges: bytes
Via: Moz-Cache-zlb05
Connection: Keep-Alive
X-Cache-Info: caching
X-Cache-Info: caching
Content-Length: 325 (the content contains a default page to display if the user-agent is not able to follow the link)

<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>301 Moved Permanently</title>
</head><body>
<h1>Moved Permanently</h1>
<p>The document has moved <a href="https://developer.mozilla.org/">here</a>.</p>
<hr>
<address>Apache/2.2.3 (Red Hat) Server at developer.mozilla.org Port 80</address>
</body></html>
```

<br>

요청된 자원이 존재하지 않는다는 내용의 알림 `404 Not Found`
```
HTTP/1.1 404 Not Found
Date: Sat, 09 Oct 2010 14:33:02 GMT
Server: Apache
Last-Modified: Tue, 01 May 2007 14:24:39 GMT
ETag: "499fd34e-29ec-42f695ca96761;48fe7523cfcc1"
Accept-Ranges: bytes
Content-Length: 10732
Content-Type: text/html

<!DOCTYPE html... (contains a site-customized page helping the user to find the missing resource)
```
  
<br>

> 상태 코드에 대한 정보는 [[HTTP 상태코드에 대하여]]

<br>

#### 요청 메서드
---
HTTP 동사라고도 불리는 HTTP 메서드는 HTTP 요청이 쿼리된 서버에서 기대하는 작업을 나타냅니다. 예를 들어, 가장 일반적인 두 가지 HTTP 메서드는 'GET'과 'POST'입니다. 'GET' 요청은 응답으로 정보를 기대하는 반면(일반적으로 웹 사이트 형식으로) 'POST' 요청은 일반적으로 클라이언트가 웹 서버에 정보를 제출하고 있음을 나타냅니다(양식 정보 등. 예: 제출된 사용자 이름 및 비밀번호).

자세한 정보는 [[HTTP 메서드란 무엇인가?]]

<br>

## Reference
---
- [MDN Web Docs](https://developer.mozilla.org/ko/)
- [Cloudflare Learning Center](https://www.cloudflare.com/ko-kr/learning/)

[^1]: 출처 : https://developer.mozilla.org/ko/docs/Web/HTTP/Guides/Overview
[^2]: 출처 : https://www.cloudflare.com/ko-kr/learning/ddos/glossary/hypertext-transfer-protocol-http/
[^3]: 출처 : https://velog.io/@andy3400/%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80-%EA%B5%AC%EC%A1%B0-%EC%9E%91%EB%8F%99%EC%9B%90%EB%A6%AC
