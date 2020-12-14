---
title: java 와 c,c++ 차이점
date: 2020-12-14 20:12:39
category: discovering
draft: false
---

# JAVA 와 C/C++ 차이점!

#### c++과 java는 문법적로 비슷하지만,

#### java는 보안, 이식성, 빠른개발에 중점을

- 가상머신 바이트 코드로 컴파일하며, 가상머신이 필요( JVM)
- ?JVM??

자바는 완전한 기계어가 아닌, 바이트코드 (.class)로 구성됨

이 바이트 코드를 JVM이 번역해줘 다양한 운영체제에서 사용될수 있게 도와줌!

- 소스파일 컴파일 되면 => 클래스 파일 => JVM 실행

#### c++는 속도와 c언의 하위 호환성에 중점을 두었다.

- 각 머신에 맞는 기계어로 컴파일함!
- 소스 파일 컴파일되어 => 목적파일 링크 => 하나의 실행프로그램이 되는 구조

- 목적파일은 기계어에 준하는 코드라고 보면된다!

#### C언어란?

운영체제 개발 목적으로 만들어, 시스템 프로그래밍이 가능한 언어!

#### C/C++ 특징은?

1. 호환성이 좋다!

   - 대부분의 컴퓨터에서 C언어를 지원한다.

2. 작고 효율적이다!

   - 다른 프로그래밍 언어에 비해 소스파일 크기가 작다
   - 즉, 실행 속도가 매우 빠르다!

3. 절차지향 프로그래밍 언어

   - 순차적인 처리로 실행속도가 빠르다는점
   - 유지보수가 어렵고, 디버깅이 어려운점

> 과거에는 하드웨어와 소프트웨어 개발 속도가 크지 않았지만,

> 소프트웨어 언어 발달과 컴파일러의 발달로 하드웨어가 소프트웨어 발달을 따라오지 못하는 상황
>
> 발생! =>> 객체지향 언어 등장!!

> 컴파일러??

소스파일로 작성된 코드를 해석하여 기계어로 바꾸는 것을 의미한다!

#### JAVA란?

객체지향 프로그래밍 언어이다!

##### 객체지향(OOP : Object Oriented Programming) ?

개발하려는 것을 기능으로 모듈화 해서 하드웨어가 중복 연산하지 않고!

> 모듈이란?

프로그램 구성하는 구성요소로, 간단하게 기능 별로 구분되 단위라고 보면된다!

> 예를 들어보자 !!

```java
package com.kh.spring.common.template;

import com.kh.spring.common.model.vo.PageInfo;

public class Pagination {

public static PageInfo getPageInfo(int listCount, int currentPage, int pageLimit, int boardLimit) {

	// * maxPage : listCount, boardLimit 영향 받음

	int maxPage = (int)Math.ceil((double)listCount/boardLimit);

	//* startPage : currentPage, pageLimit
	int startPage = (currentPage - 1) / pageLimit * pageLimit +1;

	// * endPage : startPage, pageLimit, maxPage
	int endPage = startPage + pageLimit -1;
	if(endPage > maxPage) {
		endPage = maxPage;
	}

	return new PageInfo(listCount, currentPage, startPage,maxPage, endPage, pageLimit, boardLimit);
	}
}
```

> 매번 페이징 처리 구문을 쓸 필요가 없다! 모듈화! 객체지향!

모듈 재활용으로 하드웨어 처리량 획기적을 줄여줌

##### 자바의 특징은?

1. JVM을 통해 여러 운영체제 실행가능!

- 윈도우에서 개발하고, 리눅스, 맥에서도 실행가능!

2. 메모리 자동정리

- GC를 통해서 자동으로 메모리 관리해준다!

> 그 결과 빠른 개발 가능! //

3.  멀티 쓰레드 쉽게 구현

- 스레드 생성 및 제어 관련 라이브러 api 제공

4. 동적 로딩을 지원!

- 애플리케이션 실행시, 모든 객체가 생성되는 것이아니라, 필요한 시점에 클래스를 동적 로딩하여 생성
- 즉, 유지보수가 쉬움!

5. 다형성

- 하나의 메소드나 클래스가 다양한 방법으로 동작하는 것을 으미

- 오버라이딩과 오버로딩은 다형성을 알기 가장 좋다!

  - Overloading

  - Overwriting

```java
public class Overloadingtest {

    // test() 호출
    void test(){
        System.out.println("매개변수 없음");
    }

    // test에 매개변수로 int형 2개 호출
    void test(int a, int b){
        System.out.println("매개변수 "+ a + "와 " + b);
    }

    // test에 매개변수 double형 1개 호출
    void test(double d){
        System.out.println("매개변수 " + d);
    }
}

public class test {

    public static void main(String[] args) {

        // Overloadingtest 객체 생성
        Overloadingtest ob = new Overloadingtest();

        // test() 호출
        ob.test();

        // test(int a, int b) 호출
        ob.test(10, 20);

        // test(double d) 호출
        ob.test(50);

        // test(double d) 호출
        ob.test(123.4);
    }
}






```

​

```java
public class Employee{

    public String name;
    public int age;

    // print() 메소드
    public void print(){
        System.out.println("사원의 이름은 "+this.name+ "이고, 나이는" + this.age+"입니다.");
    }
}


// Employee 상속
public class Manager extends Employee{

    String jobOfManage;

    // print() 메소드 오버라이딩
    public void print(){
        System.out.println("사원의 이름은 "+this.name + "이고, 나이는" + this.age + "입니다.");
        System.out.println("관리자 "+this.name+"은 "+this.jobOfManage+" 담당입니다.");
    }
}

public class test {

    public static void main(String[] args) {

     // Manager 객체 생성
     Manager lee = new Manager();

     // 변수 설정
     lee.name = "하이언";
     lee.age = 30;
     lee.jobOfManage="프로젝트 매니저";

// Overriding된 Manager객체의 print()호출
      lee.print();
    }
}



```

|    구분     | 오버로딩 | 오버라이딩 |
| :---------: | :------: | :--------: |
| 메소드 이름 |   동일   |    동일    |
|  매개변수   |   다름   |    동일    |
|  리턴타입   | 상관없음 |    동일    |

```
C와 JAVA의 가장 큰 차이점이라고 하자면
C : 절차지향 => 데이터 중심 함수 구현
JAVA : 객체지향 => 기능 중심으로 메서드 구현
```

![image](https://user-images.githubusercontent.com/68044188/102073906-57b4d100-3e47-11eb-9045-f225dbc1dc49.png)

끝!
