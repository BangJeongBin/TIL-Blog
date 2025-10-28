---
title: JVM(자바 가상 머신)의 구성 요소들
description: JVM의 구성 요소와 각각의 기능들을 정리
author: bin
date: 2025-05-07 09:00:00 +0800
categories: [TIL, Language]
tags: [Language, Java, JVM]
pin: true
math: true
mermaid: true
image:
 path: https://bangjeongbin.github.io/TIL-Blog/assets/img/posts/common/http-main-image.png
 alt: Baekjoon Online Judge
---

## JVM의 구조
---
![JVM_Structure](https://velog.velcdn.com/images/bluegrate/post/5914ccc8-fdb6-498c-9e68-102c7ba23e28/image.png)

JVM의 구조[^1]

- **Class Loader**(클래스 로더)
	
- **Execution Engine**(실행 엔진)
	- **Interpreter**(인터프리터)
    - **Just-In-Time**(JIT 컴파일러)
    - **Garbage Collector**(가비지 콜렉터)
    
- **Runtime Data Area**(런타임 데이터 영역)
    - **Method Area**(메소드 영역)
    - **Runtime Data Area**(힙 영역)
    - **PC Register**(PC 레지스터)
    - **JVM Stack**(스택 영역)
    - **Native Method Stack**(네이티브 메소드 스택 영역)
    
- **JNI** - **Native Method Interface**(네이티브 메소드 인터페이스)
- **Native Method Library**(네이티브 메소드 라이브러리)

<br>

### Class Loader (클래스 로더)
---
- 클래스 로더는 클래스가 참조될 때 JVM의 메모리에 클래스(.class)를 로드하는 작업을 담당함. 필요한 클래스 파일을 검색하여 메모리에 로드하여 <u>각 클래스가 한 번만 로드되도록</u> 한다. 
	
- Runtime 시 **동적으로** 로드. .jar 파일 내 저장 된 클래스들을 JVM 위에 탑재하고, 사용하지 않는 클래스들은 메모리에서 삭제함.
	
- 클래스 로더는 로드된 클래스의 무결성 확인 및 클래스 간의 종속성 해결과 같은 중요한 작업도 수행함.

<br>

### Execution Engine (실행 엔진)
---
- 클래스 로더가 JVM내의 Runtime Data Area에 바이트코드(.class)를 배치시키면 실행엔진이 해석. 즉, JVM 만이 바이트코드를 이해할 수 있기 떄문에 실행엔진이 기계가 이해할 수 있게 변환함.
	
- Java는 2가지의 방식을 혼합하여 바이트코드를 해석하는데 **인터프리터**와 **JIT 컴파일러**다. **인터프리터**는 한 줄씩 해석하기에 방식이 속도가 느리기에 이 단점을 보완하기 위해 새로운 해석 방식인 **JIT 컴파일러**이다.

- **Interpreter(인터프리터)**
	- JVM은 기본적으로 **인터프리터 방식**으로 동작한다. 다만 같은 메소드 라도 <u>여러번 호출이 된다면 매번 해석하고 수행해야 되서 전체적인 속도는 느리다.</u>

- Just-In-Time Compiler(JIT 컴파일러)
	- 바이트 코드 전체를 컴파일하여 **Native Code**로 변경하고 이후에는 해당 메서드를 더 이상 인터프리팅 하지 않고 캐싱해 두었다가 **Native Code**로 직접 실행하는 방식이다.
	- 하지만 바이트 코드를 **Native Code**로 변환하는 데에도 비용이 소요되므로, JVM은 모든 코드를 JIT 컴파일러 방식으로 실행하지 않고 <u>인터프리터 방식을 사용하다 일정 기준이 넘어가면 JIT 컴파일 방식으로 명령어를 실행하는 식</u>으로 진행한다.

>**Native Code** : C언어나, C++, 어셈블리어로 구성된 코드를 의미

<br>

### Garbage Collector (G.C, 가비지 컬렉터)
---
- JVM이 **Heap Area**를 감시하다가 더 이상 **사용되지 않는 객체(== 참조되지 않는 객체)**를 자동으로 메모리에서 해제하는 기능.

>C나 C++의 `free()`나 `delete`를 직접 호출하지 않아도, 자바는 **JVM의 가비지 컬렉터(GC)**가 알아서 필요 없는 객체를 정리함

<br>

#### G.C 동작 과정
---
1. 객체 생성 --> **Heap Area**에 저장됨

2. 변수 참조가 끊김 --> 객체를 가리키는 **Reference**가 없어짐

3. GC 탐색(Reachability Analysis)
	- 루트(root) 객체에서 접근할 수 없는 객체를 **Garbage**로 판단

4. Mark and Sweep (표시하고 쓸기)
	- **Mark 단계** : 살아있는 객체 표시
	- **Sweep 단계** : 표시되지 않은 객체(가비지) 제거
	- **Compact 단계**(선택적) : 남은 객체들을 메모리 앞쪽으로 모아 단편화 해소

<br>

### Runtime Data Area (런타임 데이터 영역)
---
![Runtime_Data_Area1](https://hongchangsub.com/content/images/2021/06/-----------2021-06-28------11.02.11.png)

Runtime Data Area 1[^2]

- JVM이 자바 프로그램을 실행할 때 사용하는 **메모리 영역 구조** 이다. 각 영역은 서로 다른 목적(클래스 정보 저장, 스택 관리, 힙 객체 저장 등)을 가지고 있음.

- 사진과 같이 **Method Area**, **Heap Area**는 모든 **쓰레드(Thread)**가 공유하는 영역이고, 나머지 **Stack Area**, **PC Register**, **Native Method Stack** 은 각 쓰레드 마다 생성되는 개별 영역이다.

| 영역                                    | 특징 / 역할                                       | 생성 시점    | 스레드 공유 여부 |
| ------------------------------------- | --------------------------------------------- | -------- | --------- |
| **Method Area (메서드 영역)**              | 클래스의 구조 정보(메서드, 필드, static 변수, 상수 등)를 저장      | JVM 시작 시 | 공유        |
| **Heap Area (힙 영역)**                  | `new`로 생성된 객체와 배열 저장                          | JVM 시작 시 | 공유        |
| **Stack Area (스택 영역)**                | 각 스레드의 메서드 호출 정보 저장 (지역 변수, 매개변수, return 값 등) | 스레드 생성 시 | 개별        |
| **PC Register (프로그램 카운터)**            | 현재 실행 중인 JVM 명령어 주소를 저장                       | 스레드 생성 시 | 개별        |
| **Native Method Stack (네이티브 메서드 스택)** | C/C++ 등 네이티브 코드 실행용 스택                        | 스레드 생성 시 | 개별        |

![Runtime_Data_Area2](https://goldenrabbit.co.kr/wp-content/uploads/2021/11/%E1%84%8C%E1%85%A1%E1%84%87%E1%85%A1-%E1%84%86%E1%85%A6%E1%84%86%E1%85%A9%E1%84%85%E1%85%B5-%E1%84%86%E1%85%A9%E1%84%83%E1%85%A6%E1%86%AF_02.png)

Runtime Data Area 2[^3]

<br>

#### Method Area (메서드 영역)
---
- 클래스 로더가 읽어온 **클래스, 메서드, 필드, static 변수, 상수** 등의 정보를 저장
    
- 프로그램 전체에서 **공유되는 영역**으로, 모든 스레드가 접근할 수 있음
    
- JDK 8 이후에는 **Metaspace**로 대체되어, 네이티브 메모리 영역에 저장

<br>

#### Heap Area (힙 영역)
---
- `new` 키워드로 생성된 **객체와 배열**이 저장되는 영역
    
- <u>GC(Garbage Collector)가 동작하는 유일한 영역</u>
    
- 모든 스레드가 공유하며, <u>가장 큰 메모리 공간을 차지함</u>

<br>

#### Stack Area (스택 영역)
---
- 메서드 호출 시 생성되는 **스택 프레임(지역 변수, 매개변수, 리턴 값 등)**을 저장
    
- **스레드마다 독립적**으로 생성되어 다른 스레드와 공유되지 않음
    
- 메서드가 종료되면 해당 스택 프레임은 **자동으로 소멸**함

<br>

#### PC Register (프로그램 카운터 레지스터)
---
- 현재 JVM 명령어의 **실행 위치(주소)를 저장**
    
- 각 스레드마다 존재하며, **멀티스레드 환경에서 실행 흐름을 추적**
    
- JVM이 어떤 명령을 다음에 실행할지를 결정하는 데 사용

<br>

#### Native Method Stack (네이티브 메서드 스택)
---
- C, C++ 등 **자바 외부 언어(JNI)**로 작성된 메서드 실행 시 사용
    
- 각 스레드마다 생성되며, 네이티브 코드 호출 시 **스택 프레임 관리**를 담당
    
- 자바 스택과 유사하지만, **JVM 외부 코드 실행용**이라는 점이 다름

<br>



## <i class="fa-solid fa-notes-medical"></i> 추천 게시물
---
- [JVM(자바 가상 머신)이란?](https://bangjeongbin.github.io/TIL-Blog/posts/what-is-jvm/)

<br>

## Reference
---
- [☕ JVM 내부 구조 & 메모리 영역 💯 총정리](https://inpa.tistory.com/entry/JAVA-%E2%98%95-JVM-%EB%82%B4%EB%B6%80-%EA%B5%AC%EC%A1%B0-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EC%98%81%EC%97%AD-%EC%8B%AC%ED%99%94%ED%8E%B8)
- [(Java) JVM 이해하기](https://hongchangsub.com/java3/)
- [java의 동작과정과 JVM의 메모리 구조](https://velog.io/@bluegrate/java%EC%9D%98-%EB%8F%99%EC%9E%91%EA%B3%BC%EC%A0%95%EA%B3%BC-JVM%EC%9D%98-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EA%B5%AC%EC%A1%B0)

<br>

[^1]: 출처 : https://velog.io/@bluegrate/java%EC%9D%98-%EB%8F%99%EC%9E%91%EA%B3%BC%EC%A0%95%EA%B3%BC-JVM%EC%9D%98-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EA%B5%AC%EC%A1%B0
[^2]: 출처 : https://hongchangsub.com/java3/
[^3]: 출처 : https://goldenrabbit.co.kr/2021/11/03/%EC%9E%90%EB%B0%94-%EC%BD%94%EB%93%9C%EC%99%80-%EB%A9%94%EC%84%9C%EB%93%9C-%EC%8A%A4%ED%83%9C%ED%8B%B1-%EB%B3%80%EC%88%98-%EB%93%B1%EC%9D%80-%EB%A9%94%EB%AA%A8%EB%A6%AC%EC%9D%98-%EC%96%B4%EB%94%94/
