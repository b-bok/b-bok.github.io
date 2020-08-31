---
title: C언어 어려웠던 것 정리
date: 2020-08-31 15:08:09
category: computerscience
draft: false
---



## C언어 문자와 버퍼의 관계!

남아있는 버퍼를 지워주자!

```java
Scanner sc = new Scanner(System.in);

System.out.print("숫자 입력 : " );

int a = sc.nextInt();



sc.nextLine();	// 이 역할이 입력 퍼버를 지워 주는 것이다, 지워주지 않는다면, \n이 문자열로 들어가버릴것이다!!



System.out.print("문자열 입력 :  ");

String str = sc.nextLine();


```



```c++
int main(void) {
int a;
char c;
scanf("%d",&a);
printf("%d\n",a);
int temp;
// 한 자씩 받아서 파일의 끝이거나, 개행 문자를 만나면 입력을 멈추므로 항상 입력버퍼 비우기
while ((temp= getchar() != EOF && temp != '\n')) {} //비어있으면 아무것도 안하도록!
scanf("%c", &c);
printf("%c\n", c);
system("pause");
return 0;
}
```



## 포인터와 배열

배열의 이름은 배열의 첫번째 원소의 주소라는 것!

```c++

int main(void) { 

int a[5] = {1,2,3,4,5};
int* b = &a[0];	// == int *b = a;
printf("%d\n",b[2]);
system("pause");
return 0;
}
```


마찬가지로 포인터를 배열처럼!

```c++
int main(void) {
	int a[5] = {1,2,3,4,5};
	int i;
	for (i = 0; i < 5; i++) {
		printf("%d",*(a+ i)); // *(a+i) == a[i]
	}
	system("pause");
	return 0;
 }
```





## 동적 메모리 할당

우리가 원하는 만큼만 메모리를 할당해 사용하고자 할 때

동적 == 프로그램 실행 도중에



| 코드영역 |     데이터 영역      |     힙영역     |      스택영역      |
| :------: | :------------------: | :------------: | :----------------: |
| 소스코드 | 전역변수 /  정적변수 | 동적 할당 변수 | 지역변수, 매개변수 |



## 중요

 스택 영역에 선언된 변수는 프로그램 종료와 동시에 메모리에서 사라지므로 따로 메모리 해제 해주지 않아도 된다!

<b>BUT</b> 힙 영역에 동적으로 할당된 변수는 반드시 <b><font color = "red">free()</font></b>함수로 메모리 해제 해줘야함!!





> malloc(); 와 free(); 한쌍이라는 것 잊지 말자!

```c++
#include <stdio.h>
#include<stdlib.h>

int main(void) {
	int* a = malloc(sizeof(int));
	printf("%d\n",a);
	free(a);
	a = malloc(sizeof(int));
	printf("%d\n",a);
	free(a);
	system("pause");
	return 0;
 }
```





> memset(포인터, 값, 크기); == 문자열 과 굉장히 유사

> 일괄적인 범위의 메모리를 모두 특정값으로 설정 하려할 때!

```c++
#include <stdio.h>
#include<stdlib.h>
#include<string.h>	// memset은 이 라이브러리에 선언되어있다.

int main(void) {
	char* a = malloc(100);
	memset(a, 'A',100); // 포인터, 값, 크기
	for (int i = 0; i < 100; i++) {
		printf("%c\n", a[i]);
	}

	system("pause");
	return 0;

 }
```



> 출력값을 예상해보자!

```c++
int main(void) {
	int** p = (int**)malloc(sizeof(int*) * 3); 
	// int **p == 2차원 배열 만들거야!
	// 포인터는 배열과 비슷하다는 것을 기억하고,
	// int* => int형 배열만든다! => int* * 3 => 그 1차원 배열이 3개다!
	// (int**) => 1차원 배열 3개 통째로 => int ** p라는 것이지

	for (int i = 0; i < 3; i++) {
		*(p + i) = (int*)malloc(sizeof(int) * 3);
	// 그리고 보면, 1차원 배열마다 초기화 안되어있음!
	// 배열의 첫번째 주소(*p + i) == 배열 
	// 각 1차원 배열(int*)마다 3개 int값(int) 갖도록 초기화

	}
	for (int i = 0; i < 3; i++) {
		for (int j = 0; j < 3; j++) {
			*(*(p + i) + j) = i * 3 + j;
	// 2중 포문으로 값을 넣어준다.
		}

	}
	for (int i = 0; i < 3; i++) {
		for (int j = 0; j < 3; j++) {
			printf("%d ",*(*(p+i)+j));
		}
		printf("\n");
	}
	free(p);
	system("pause");
	return 0;
 }
```





이해가 어렵다면...

[참고하기]: https://www.youtube.com/watch?v=_1PiJAjB7Io&amp;list=PLRx0vPvlEmdDNHeulKC6JM25MmZVS_3nT&amp;index=20	" 동적 할당값을 이용한 2차원배열 추가 설명 유튜브"


