---
title: Map과hashMap을 자바 API문서를 해석해보았다.
date: 2021-01-27 01:01:98
category: java
draft: false
---

## 2021.01.26 면접 복기

면접에서 중요했던것은 이 기술,자료구조 등이 어떠한 것인지,

그리고 어떠한 이유로 사용되는지 정확히 알아야한다는 것이다.

#### Map과 HashMap

1. Map의 정의를 자바 API 공식문서에서 살펴보자.

이 오브젝트는 key에 value를 매핑합니다. 맵은 중복된 키를 가질 수 없고, 각각의 key에는 하나의 value를 가집니다.

이 인터페이스는 Dictionary 클래스를 대신합니다. 이 맵 인터페이스는 세가지의 컬렉션 뷰를 제공합니다. key들의 집합, value들의 집합, key 와 value들의 집합 세가지 이다.

맵의 순서의 경우에는 iterator를 이용해서 각 요소들을 리턴하기도 합니다.

몇몇의 맵의 implements들 TreeMap클래스는 순서를 보장하지만, HashMap은 순서가 없습니다.

> 몇몇의 변형가능한 객체(mutable)들은 맵의 키로 사용할 경우 주의가 필요합니다.

맵의 이러한 행위는 명확하지 못합니다. 객체가 맵에서 key로 있는 동안 동일비교의 영향을 주는 방법으로 객체의 값이 변화되는 경우에 말입니다. 금지되는 특별한 케이스는 맵 스스로 키를 가지지 못할 경우를 말할 수 있습니다. 반면에 맵 그자체로 값을 가지는 형태는 가능할 수 있습니다. 굉장히 조심하라고 충고하고싶습니다. equls와 hashCode메서드는 맵처럼 잘 정의하지 못합니다.

맵의 implements들의 일반적인 목표는 두개의 기본 구조체를 제공합니다. void constructor 은 비어있는 맵을 만들고, 하나의 전달값을 가지는 constructor은 전달값으로 매핑된 key-value를 갖는 새로운 맵을 만듭니다. 후자의 구조체의 경우는 사용자가 어떤 맵으로든 복사가 가능하고, 원하는 클래스의 맵으로 동일하게 만들게끔 합니다.

인터페이스의 경우 구조체를 포함하고 있지 않기 때문에, 후자의 방법을 쓰게끔 강요할 수는 없지만 JDK의 일반적인 목적으로서의 맵의 implements는 후자의 방법을 따르고 있습니다.

분해하는(destructive) 매서드들은 인터페이스에 포함되어있습니다. 맵을 동작하는 이러한 매서드들은 UnsupportedOperationException에러를 throw하게 명시하게합니다. 맵이 그 동작을 지원하지 못하면 말이죠. 이러한 케이스의 경우, 앞의 메서드들이 UnsupportedOperationException에러를 throw 요구하는 것은 아닙니다. 만약 맵의 호출에 영향이 없다면 말이죠. 예를들어 putAll 매서드를 호출하는 것은 수정불가능한 맵의 경우에지만 반드시 요구되는 것은 아닙니다.

몇몇의 map implements들은 key와 value에 제한상응을 가지고 있습니다. 예를들어 몇몇의 implements는 null값이 key와 value에 들어가는 것을 금지합니다. 타입에 제한을 두는 경우도 있습니다. 자격이 없는 key와 value를 넣으려고 할 때, 일반적으로NullPointerException or ClassCastException 발생합니다. 맞지 않는 쿼리의 경우에도 마찬가지입니다.

#### HashMap은??

hashtable을 베이스로한 Map 인터페이스의 implements입니다. hashMap은 대부분의 map의 operation을 제공합니다. null value와 null key가 들어가는 것을 허용합니다. 간단하게 hashtable과 hashMap은 동일하지만 hashtable은 null 값을 허용하지 않습니다. hashMap은 순서를 보장하지 않습니다.

hashMap은 get과 put의 경우 일관성있는 시간 퍼포먼스를 제공합니다.해시 함수가 요소를 버킷 사이에 적절히 분산시킨다고 가정할 경우에 말이죠.

> 버킷 : entry들이 저장되는 공간

반복되는 컬렉션 뷰는 시간 비례 hashMap 인스턴스(+key value 매핑 수까지 더한)를 요구합니다. 그래서 최초에 capacity를 지정하지 않는 것은 performance에 굉장히 중요합니다.

hashMap 성능에 영향을 미치는 두개의 파라미터가 있습니다. 최초 capacity와 부하계수 입니다. capacity는 해시테이블의 버킷의 수입니다. 간단히 말해 해시테이블이 생성되는데 capacity를 의미합니다. 부하 계수는 capacity가 자동적으로 증가하기전에 어떻게 해시테이블이 채워지는가에 따라 측정됩니다.

entries의 수가 부하계수와 현재 capacity를 초과할 경우, 해시테이블은 다시 재구성됩니다. 그렇기 때문에 해시테이블은 두배의 버킷을 가지고 있습니다.

일반적으로 기본 부하계수는 시간과 공간비용에 적절하게 트레이드합니다. 더 높은 value는 공간의 오버헤드를 줄이지만, lookup 비용을 증가시킵니다. 예상되는 entries의 수는 최초에 세팅되는 맵과 부하계수에 의해 정해집니다. 그렇기 때문에 rehash 동작을 최소화하기 위해서는 최초의 capacity가 중요합니다. 만약 최초의 capacity가 부하계수로 나눈 entries보다 크다면, rehash는 발생하지 않습니다.

hashMap에 저장된 많은 매핑값들은 충분히 넓은 capacity에 생성한다면, 자동적으로 생성되어 rehashing되어 커지는 테이블보다 효율적입니다.

> hashMap은 동기화되지 않습니다.

만약 hashMap에 멀티쓰레드가 동시에 접근한다면, 적어도 한 쓰레드는 구조적으로 수정될 것입니다. 외부적으로 동기화 될것입니다. 삽입과 삭제같은 것이 구조적인 수정입니다. 인스턴스가 이미 포함하고 있는 키와 관련된 값만 변경하는 것은 구조적인 수정이 아닙니다. 이것은 일반적으로 캡슐화된 맵으로 동기화가 완수됩니다. 이와 같은 객체가 없다면, 그 map은 Collections.synchronizedMap 매서드로 "wrapped"되어야합니다. 이 방법이 동기화되지 않는 접근을 막을 수 있습니다.

https://docs.oracle.com/javase/7/docs/api/index.html

ps. 해석해보았으나 전혀모르겠다.... 얼추 감이 오기때문에 구글링으로 더욱 기반을 단단히 만들어야겠다..
