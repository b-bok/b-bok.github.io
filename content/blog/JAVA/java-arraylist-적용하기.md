---
title: Java ArrayList 적용하기
date: 2020-07-22 21:07:64
category: JAVA
draft: false
---
[참고]: https://coding-factory.tistory.com/551



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



![찾았다 이놈](C:\Users\user2\Desktop\찾았다 이놈.jpg)



그래서,,, 

## ArrayList가 무엇?


