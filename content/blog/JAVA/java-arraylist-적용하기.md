---
title: Java ArrayList 적용하기
date: 2020-07-31 16:07:28
category: JAVA
draft: false
---
# ArrayList를 알아보자!

1. 배열을 쓰다보면 배열은 항상 저장용량을 설정해줘야한다!

```java
int[] arr = new int[5];
double[] dArr = new double[7];
```

저장 용량을 설정해주지 않으면  이 문구를 만나기 쉽다!

`Variable must provide either dimension expressions or an array initializer`

배열 초기화 또는 할당을 해달라는 내용이다!

2. 배열은 저장용량을 초과하면 자동으로 늘어나지 않는다!

위의 이유로 더 나은 클래스를 찾아보기로 했다!

![findArray](http://t1.daumcdn.net/liveboard/samanco/201505/1431051050452.jpg)

그래서,,,

## ArrayList를 발견했다!

#### ArrayList란?

* ArrayList는 List인터페이스를 상속받은 클래스로 크기가 가변적으로 변하는 선형 리스트!
* * 선형 리스트 :  리스트에 나열한 데이터들이 순서를 갖고 있을 때 저렇게 부른다!
  * 추 후 cs[자료구조]를 더 공부하자!



자 그럼 ArrayList를 한번 사용해 보자!

**1. ArrayList는 java.util.ArrayList에 있으므로 import 해줘야 한다!**
`import java.util.ArrayList`
**2. ArrayList를 사용하기 위해 객체를 생성해주자!**
정수값을 넣을 수 있도록 설정했다! <Integer>
`ArrayList<Integer> arrayList = new ArrayList<>();`
`int[] arr = new int[5]`
보다시피 배열을 생성할 때 처럼 크기를 할당 할 필요가 없다.
ArrayList는 메모리가 허용하는 동안 유동적으로 크기가 변한다!


## 그럼, 본격적으로 ArrayList 를 사용해보자!

> ArrayList 선언

```java
ArrayList list = new ArrList(); // 타입을 설정하지 않으면, Object로 선언!
// Student객체로 타입 설정!  Student 객체만 사용 가능!
ArrayList<Student> member = new ArrayList<Student>(); 
// int 타입으로 설정!
ArrayList<Integer> num = new ArrayList<Integer>(); 
// new에서는 타입 생략 가능!
ArrayList<Integer> num2 = new ArrayList();
// 초기 용량(capacity) 지정 가능!
ArrayList<Integer> list2 = new ArrayList<Integer>(10);
//생성과 동시에 초기화 역시 가능!
ArrayList<Integer> list3 = new ArrayList<Integer>(Array.asList(1,2,3,4));
// 추후 Wrapper클래스, 제너릭스(Generics)개념을 설명 하도록 하겠습니다!
```



#### ArrayList  크기 구하기 :  size()

```java
ArrayList<Integer> list = new ArrayList<Integer>(Arrays.asList(1,2,3));
//list 크기 : 3
System.out.println("list 크기 : " + list.size()); 
```

* 크기 구하기 메소드 :  .size()

<hr/>

#### ArrayList 값 추가 :  add

```java
ArrayList<Integer> list = new ArrayList<Integer>();
// add ==> 값 추가 메소드
list.add(3);
// add(index,value) 형태
list.add(1,10);
```

* Array List의 값 추가 메소드 :   add([index], value)  index는 생략 가능

<hr/>

#### ArrayList 값 삭제 : remove, clear

```java
ArrayList<Integer> list = new ArrayList<Integer>(Arrays.asList(1,2,3));
// index 2 제거
list.remove(2);
// 모든값 제거
list.clear();
```

* Array List의 값 삭제 메소드 :   remove(index)  객체 제거하면 바로 뒤 인덱스 부터 마지막 인덱스 까지 모두 앞으로 1씩 당겨집니다!
* clear() 메소드는 모든 값을 한번에 제거할 수 있습니다.

<hr/>

#### ArrayList 값 출력 :  Iterator, get

```java
ArrayList<Integer> list = new ArrayList<Integer>(Arrays.asList(1,2,3,4,5));
//0번째 인덱스 출력 
System.out.println(list.get(0)); 

//향상된 for문으로 전체 출력
for(Integer i : list) {
    System.out.Println(i);
}

// Iterator 선언
Iterator iter = list.iterator(); 
// 다음 값이 있는지 확인
while(iter.hasNext()) {
    //값 출력
    System.out.println(iter.next());
}


```

* 값 출력 : get(index) 		전체 출력 : for문, Iterator 사용 출력!

<hr/>

#### ArrayList  값 검색 : indexOf, contains

```java
ArrayList<Integer> list = new ArrayList<Integer>(Arrays.asList(1,2,3));
//list에 2가 있는지 검색 : true, false 로 반환
System.out.println("list 배열에 2가 있는지 : " + list.contains(1)); 
//list에 2가 있는지 검색 : 2가 있는 인덱스 반환 // 없으면 -1 반환
System.out.println("list 배열에 2가 있는지 : " + list.indexOf(2)); 
```

* 찾고자 하는 값 검색  : contains(value)
* 값이 있는 인덱스 검색 : indexOf(value)

<hr/>

