---
title: java non static과 static의 차이
date: 2020-12-23 18:12:07
category: python
thumbnail: { thumbnailSrc }
draft: false
---

## java의 non-static 멤버와 static 멤버의 차이

#### non-static 맴버란?

1. 공간적 특성 : 객체마다 별도로 존재
   1. 인스턴스 맴버라고 부름
2. 시간적 특성 : 객체 생성시 함께 생성
   1. 객체가 생성되어야 맴버도 사용가능
   2. 객체가 사라지면 맴버 역시 사라짐
3. 공유 불가
   1. 객체 내의 각각의 공간을 유지

#### static 맴버?

1. 공간적 특성 : 맴버는 클래스당 하나(?)가 생성됨!
   1. 객체 내부가아니라, 다른 공간(?)에 생성
   2. 클래스 맴버 라고 부름
2. 시간적 특성 : 클래스 로딩시에 맴버가 생성
   1. 객체가 생성되기 전에 미리 생성되어있음
   2. 객체 생성하지 않아도 사용 가능
   3. 객체가 사라져도, static맴버는 사라지지 않는다.
   4. 프로그램이 종료될 때 사라진다.
3. 공유 가능 : 동일한 클래스 객체에 한해서

##### 그러고보니 java main method 역시 static인데??

```
그것은 JVM은 인스턴스가 없는 클래스 main()을 호출 해야하기 때문에 static 이어야한다.
```

> static이어야만 프로그램 실행시, 객체 생성하지 않아도 사용가능하다

##### JVM과 static의 관계

1.  코드 실행시, 컴파일러가 .java 코드를 .class 로 변환!
2.  클래스 로더가 .class파일을 메모리영역(Runtime Data Area)(?)에 로드한다.
3.  메모리 영역중 Method Area(=Class are = Static area)라고 불리는 영역에 Class Variable(전역변수)가 저장, static 변수 역시 여기에 포함된다!
4.  JVM은 Method Area에 로드된 main()을 실행!!

![image](https://user-images.githubusercontent.com/68044188/102980144-73585f80-454a-11eb-919f-1f3da3a2e7e5.png)

###### Runtime Data Area??

Jvm은 시스템으로부터 프로그램 수행시 필요한 메모리를 할당, 용도에 맞게 여러 영역에 나누어 관리한다!

1. JAVA Compiler : JAVA코드를 ByteCode 즉, .class로 변환
2. JAVA API, Class File : 컴파일을 마친 자바 클래스 파일
3. Class Loader System : 컴파일이 끝난 자바 클래스 파일 메모리에 적재
4. Execution Engine : ByteCode 실행가능하도록 해석

#### Runtime Data Area ??!

> Method Area Heap은 모든 Thread에 공유된다!

##### PC Registers

Thread가 생성될때 마다 생기는 공간으로, Thread가 어떤 명령을 실행하게 될지를 기록

##### Method Area

JVM이 프로그램 실행중 클래스가 사용되면 인스턴스변수, 메소드 코드를 여기에 저장 + 클래스 변수도함께 생성

##### Heap

객체를 동적으로 생성하면 인스턴스가 Heap영역의 메모리에 할당되어 사용되어진다. 즉 Heap영역은 GC의 대상이다.

##### JVM Stacks

Thread 제어를 위해 사용되는 메모리 영역
