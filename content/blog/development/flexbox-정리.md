---
title: Flexbox 정리
date: 2020-12-02 00:12:87
category: development
draft: false
---

# FLEXBOX



## justify-content



flex- start : 요소들을 컨테이너 왼쪽 정렬

flex - end : 요소들을 컨테이너 오른쪽 정렬

center :  요소들을 컨테이너 가운데로 정렬

space-between : 요소들 사이에 동일한 간격으로 두기(맨앞과 맨뒤는 제외되더라!)

space-around : 요소들 주위에 동일한 간격을 두기



## align-items

flex-start : 요소의 컨테이너의 꼭대기로 정렬

flex-end : 요소의 컨테이너의 바닥으로 정렬

center : 요소의 컨테이너의 세로 가운데 정렬

baseline : 요소들의 컨테이너를 시작위치에 정렬

stretch :  요소들을 컨테이너에 맞도록 늘림





## flex-direction

row :  요소들을 텍스트방향과 동일하게 정렬

row -reverse : 요소들을 텍스트 반대방향으로 정렬

column : 요소들을 위에서 아래로 정렬

column : 요소들을 아래에서 위로 정렬



** column-reverse, row-reverse를 사용하면 start와 end 순서 바뀝니다. **

****

** column-reverse, row-reverse를 사용하면 justify-content의 방향은 세로, align-items의 방향이 가로로 바뀝니다.**



## flex-wrap



nowrap: 모든 요소 한줄에 정리

wrap : 요소들을 여러줄에 걸쳐 정렬

wrap-reverse : 요소들을 반대로 여러줄에 걸쳐 정렬





## align-self

align-items가 와 같지만, 개별 요소에 적용이 가능하다.



## flex-flow  =  flex-direction flex-wrap





## align-content

flex-start : 여러줄을 컨테이너 꼭대기로

flex-end : 여러줄을 컨테이너 바닥으로

center : 여러줄을 세로상 가운데로

space-between : 여러줄 사이에 동일 간격을 둡니다.

space-around : 여러줄 주위로 동일간격을 둡니다.

stretch : 여러줄들을 컨테이너에 맞도록 늘립니다.


