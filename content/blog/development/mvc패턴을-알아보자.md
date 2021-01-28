---
title: MVC패턴을 알아보자
date: 2021-01-28 17:01:42
category: development
draft: false
---

### MVC패턴을 알아보자!

디자인 패턴 중의 하나로 말할 수 있다!

Model, View,Controller의 약자로, 프로젝트 구성할때 구성요소를 세가지 역할로 구분하는 패턴을 의미한다.

![](https://user-images.githubusercontent.com/68044188/106104238-84b60c80-6185-11eb-9049-8475ec6a4c9e.png)

##### 디자인패턴?

프로그램 개발시 자주 겪는 문제상황에 대한 일반적이고, 재사용 가능한 해결책을 의미한다.

즉, 소프트웨어 개발방식을 공식화 한것을 의미한다.

### Model

애플리케이션의 정보, 데이터를 나타낸다. 프로그램이 목표하는 작업을 잘 수행하기 위해 필요한 물리적 개체, 규칙, 작업 요소를 구분해 놓은 것을 의미하며 DTO등을 말할 수 있다.

몇가지 규칙이 있는데..

1. 사용자가 편집하길 원하는 데이터를 가지고 있어야한다. 2. 뷰나 컨트롤러에대해 정보를 노출해서는 안된다. 3. 변경 시, 변경에 대한 처리방법이 구현되어야한다.

### View

사용자가 보는 화면에 입출력 결과및 과정을 보여주기 위한 역할.

도메인의 로직을 담고 있어서는 안되고, 객체를 전달받아 출력하능 역할만을 담당해야한다.

### Controller

controller는 model과 view를 연결시켜주는 역할을 한다고 보면 좋다.

controller에서는 model과 view 각각 어떤 역할과 책임을 지는지 알고 있어야한다.

### MVC패턴의 장점

Model, View, Controller 각각의 맡은바에 집중하여 개발 가능하다. 유지보수, 확장성, 유연성을 높여주며, 중복 코딩의 문제를 해결가능하다.

> 유연성 : 유연성이 높으면 클라이언트의 새로운 요구사항에 대해 최소한의 비용으 대처 가능하다는 것을 의미한다.

https://m.blog.naver.com/jhc9639/220967034588

https://velog.io/@ljinsk3/MVC-%ED%8C%A8%ED%84%B4

### MVC패턴의 단점

화면이 복잡하고, 데이터가 필요한 화면의 경우 Controller에 다수의 Model과 View가 연결 되어있어서 View와 Model의 의존성이 높아집니다.

또한, 이럽게 복잡해지고, 비대해진 MVC는 새로운 기능 추가시 코드분석, 테스트가 어려워집니다.

### MVC패턴 model1과 model2

JSP를 사용할 경우,

model1 : JSP에서 출력과 로직을 전부 처리합니다.

- 웹 브라워저 사용자의 요청을 받은 JSP가 자바 빈, 서비스 클래스를 이용해서 요청한 작업을 처리하고 그 결과를 출력합니다.

  ![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F6SIUm%2FbtqzYCsgeQE%2FIYkMcagYXWwMf7NSbRFJu0%2Fimg.png)

model2 : JSP에서 출력만 처리합니다.

​ \* 웹 브라우저 사용자의 요청을 Servlet이 받습니다. Servlet은 요청을 받아 View보여줄 것인지, Model로 부여줄 것인지 정하여 전송합니다. model2방식은 HTML과 JAVA를 분리해 놨기 때문에 유지보수성이 훨씬 좋습니다.

https://coding-factory.tistory.com/69

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FGSBZ4%2FbtqzZdec5re%2F4LYL59sQl6B72Ak4tlknP0%2Fimg.png)

https://wooaoe.tistory.com/15
