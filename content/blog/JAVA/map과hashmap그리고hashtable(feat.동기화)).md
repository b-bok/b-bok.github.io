---
title: Map과HashMap그리고HashTable(feat.동기화))
date: 2021-01-28 15:01:88
category: java
draft: false
---

## Map과 HashMap

#### Map을 간단하게 정의해보자.

Map은 key와 value를 가진 집합으로, 중복을 허용하지 않는다.

#### HashMap은??

HashMap은 Map interface를 implements한 클래스로 중복을 허용하지 않는다.

Map의 특징인 key value를 쌍으로 이루며, null값을 허용한다.

동기화(Synchronization)을 지원하지 않는다.

속도 측면에서 동기화를 지원하지 않는 HashMap이 HashTable보다 빠르다.

- HashMap은 저장공간보다, 값이 추가로 들어올 경우 List처럼 저장 공간을 추가로 늘리지만, 저장공간을 두배로 늘립니다. 그렇기 때문에 저장할 데이터를 알고 있다면 초기 값을 지정해주는 것이좋습니다.

```java
HashMap<String,String> map4 = new HashMap<>(10);
//초기 용량(capacity)지정
```

https://coding-factory.tistory.com/556

> 동기화(Synchronization)?
>
> 프로세스 또는 스레드들이 수행되는 시점을 조절하여 서로 알고 있는 정보가 일치하는 것을 의미한다.
>
> 동기화된 메소드는 동시에 호출되더라도 겹치지 않는다.
>
> = 스레드가 동기화된 메소드를 실행하면, 그 스레드가 종료될때까지 모든 스레드는 중지된다.

> 스레드(Thread)??
>
> 프로세스의 특정한 수행 경로를 의미한다.
>
> 프로세스가 할당 받은 자원을 이용하는 실행의 단위

> 프로세스(process)?
>
> 메모리에 올라와 실행되고 있는 프로그램의 인스턴스(독립된 개체)
>
> Code, Data, Stack, Heap의 구조로 되어있는 독립된 메모리 영역

> 간단하게 예를 들어보자
>
> a= 2라는 자원 이있고, P1라는 프로세스는 a라는 값을 이용해서 로직을 수행합니다. 그런데 그 사이에 P2라는 프로세스가 a의 값을 3으로 바꾼다면?

a를 공유 자원이라고 말하며

경쟁상태 : 이렇게 두개 이상의 프로세스 또는 스레드가 동기화 없이 접근하는 현상

동기화 : P1과 P2의 알아고있는 정보를 일치시키는 것을 말합니다.

https://ooeunz.tistory.com/94

https://gmlwjd9405.github.io/2018/09/14/process-vs-thread.html

#### HashTable도??

HashMap과 유사하지만, key 나 value에 null값을 허용하지 않는다.

동기화를 보장하므로, 멀티쓰레드 환경에서는 데이터 일관성 유지를 위해 HashTable을 사용해야한다.

https://genie247.tistory.com/11

#### ConcurrentHashMap

HashTable의 동기화 속도가 느려, 동기화가 보장되는 HashMap라고 보면 된다.

동기화 보장하며, Null값은 불가능하다.

https://12216715011126.tistory.com/53
