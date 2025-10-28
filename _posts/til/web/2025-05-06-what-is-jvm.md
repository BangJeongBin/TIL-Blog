---
title: JVM(자바 가상 머신)이란?
description: JVM(Java Virtual Machine)에 대하여
author: bin
date: 2025-05-06 09:00:00 +0800
categories: [TIL, Language]
tags: [Language, Java, JVM]
pin: true
math: true
mermaid: true
image:
 path: https://bangjeongbin.github.io/TIL-Blog/assets/img/posts/common/http-main-image.png
 alt: Baekjoon Online Judge
---

## Java 프로그램 실행 단계
---
![java_compiler](https://velog.velcdn.com/images/jungmyeong96/post/840f842a-f7c0-4fce-be20-cb66a321e57f/image.png)

Java 컴파일 과정[^1]

Java로 작성된 프로그램은 일련의 과정을 거칩니다. 소스 코드가 실행되면 JVM을 통해 해당 OS에 도달하기 때문에 OS에서 인식 가능한 기계어로 바로 컴파일 되는 것이 아니라 위 그림과 같이Bytecode(.class)로 컴파일 됩니다.

>Java compiler는 JDK를 설치하면 bin에 존재하는 `javac.exe`이다. 즉, JDK에 Java compiler가 포함되어 있음.
>javac 명령어를 통해 .java를 .class로 컴파일 할 수 있다.

<br>

## JVM 이란?
---
**JVM(Java Virtual Machine)**이란 Java의 바이트 코드를 실행할 수 있는 가상 머신을 뜻합니다.

JVM은 Java 프로그래밍 언어와 기본 하드웨어 간의 인터프리터 역할을 하기 때문에 <u>특정한 OS에 종속받지 않고 CPU가 JAVA를 인식, 실행할 수 있게 하는 가상 컴퓨터</u>입니다. 이로써 Java 애플리케이션이 다양한 플랫폼 및 운영 체제에서 실행될 수 있는 런타임 환경을 제공합니다.

![JVM](https://velog.velcdn.com/images/god1hyuk/post/cdfbd59a-3518-4c62-bfe7-4a1a3b5d8925/image.png)

JVM[^2]

<br>

## JVM의 구조
---
![JVM_Structure](https://velog.velcdn.com/images/bluegrate/post/5914ccc8-fdb6-498c-9e68-102c7ba23e28/image.png)

JVM의 구조[^3]

- **Class Loader**(클래스 로더)
	
- **Execution Engine**(실행 엔진)
	- **Interpreter**(인터프리터)
    - **Just-In-Time**(JIT 컴파일러)
    - **Garbage Collector**(가비지 콜렉터)
    
- **Runtime Data Area**(런타임 데이터 영역)
    - **Method Area**(메소드 영역)
    - **Runtime Data Area**(힙 영역)
    - **PC Register**(프로그램 카운터 레지스터)
    - **JVM Stack**(스택 영역)
    - **Native Method Stack**(네이티브 메소드 스택 영역)
    
- **JNI** - **Native Method Interface**(네이티브 메소드 인터페이스)
- **Native Method Library**(네이티브 메소드 라이브러리)

<br>

## JVM의 동작 방식
---
![How_to_work_JVM](https://images.velog.io/images/raejoonee/post/febb74dc-1b88-45d7-b019-3728f7f1ba93/jvm.png)

JVM의 동작 방식[^4]

1. Java 프로그램이 실행되면 JVM은 OS로 부터 이 프로그램이 필요로 하는 메모리를 할당 받는다.

2. 자바 컴파일러(javac)가 자바 소스코드(.java)를 읽어들여 자바 바이트코드(.class)로 변환 시킨다.

3. **Class Loader**를 통해 자바 바이트코드(.class) 파일들을 JVM으로 로딩한다.

4. 로딩 된 자바 바이트코드(.class) 파일들은 **Execution Engine**을 통해 해석된다.

5. 해석 된 바이트 코드는 **Runtime Data Area**에 배치 되어 실질적인 프로그램의 수행으로 이루어지게 된다.

<br>

## 마무리
---
- JVM의 여러가지 특징이 있지만 가장 두드러지는 장점은 **플랫폼 독립성**입니다. 바이트 코드로 컴파일된 Java 응용 프로그램은 호환되는 JVM이 설치된 모든 운영 체제 또는 플랫폼에서 실행할 수 있습니다. 즉, `Windows` 시스템에서 개발된 Java 프로그램은 적절한 JVM이 있는 한 수정 없이 `Linux` 시스템에서 실행할 수 있습니다.

- 이어서 다음 포스트는 JVM의 각 구성요소들의 기능 및 프로그램 실행 시 할당되는 메모리 영역에 대해서 설명하겠습니다.

<br>

## <i class="fa-solid fa-notes-medical"></i> 추천 게시물
---
- [JVM(자바 가상 머신)의 구성 요소들](https://bangjeongbin.github.io/TIL-Blog/posts/configuration-of-jvm/)

<br>

## Reference
---
- [Lenovo - JVM이란 무었입니까?](https://www.lenovo.com/kr/ko/glossary/jvm/?orgRef=https%253A%252F%252Fwww.google.com%252F&srsltid=AfmBOopBrRBZyZguBjMSTUtioPDSHkPCh2hU2nBHf2qcax39Lmpq29R5)
- [☕ JVM 내부 구조 & 메모리 영역 💯 총정리](https://inpa.tistory.com/entry/JAVA-%E2%98%95-JVM-%EB%82%B4%EB%B6%80-%EA%B5%AC%EC%A1%B0-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EC%98%81%EC%97%AD-%EC%8B%AC%ED%99%94%ED%8E%B8)
- [(JAVA기초) JVM이란?](https://velog.io/@jungmyeong96/JAVA%EA%B8%B0%EC%B4%88-JVM%EC%9D%B4%EB%9E%80)
- [(Java) JVM 개념 및 동작 원리](https://min-gyeong.tistory.com/72)

<br>

[^1]: 출처 : https://velog.io/@jungmyeong96/JAVA%EA%B8%B0%EC%B4%88-JVM%EC%9D%B4%EB%9E%80
[^2]: 출처 : https://0soo.tistory.com/12
[^3]: 출처 : https://velog.io/@bluegrate/java%EC%9D%98-%EB%8F%99%EC%9E%91%EA%B3%BC%EC%A0%95%EA%B3%BC-JVM%EC%9D%98-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EA%B5%AC%EC%A1%B0
[^4]: 출처 : https://velog.io/@raejoonee/about-jvm
