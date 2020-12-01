---
title: 파이썬 기본 개념 익히기(feat.코테)
date: 2020-12-01 19:12:77
category: Python
draft: false
---

## 왜 파이썬을 공부하죠?
1. 풍부한 라이브러리
2. 선택한 교재의 추천 언어

# 파이썬 기본 자료형



# 소수부가 0 일때 0 생략가능

a = 5.
print(a)

# 정수부가 0 일때 0 생략가능

a = .7
print(a)

# 실수값 정확하지 않기 때문에 round 사용하기

a = 0.3 + 0.6
print(a)

if a == 0.9 : 
    print(True)
else :
    print(False)
    

# round(실수형 데이터, (반올림하려는 위치 -1))

print(round(a,4))
if round(a,4) == 0.9 : 
    print(True)
else :
    print(False)

# 파이썬에서는 나누기 연산, 실수형으로 반환

a = 7
b = 3

print(a/b)

# 몫 구하기

print(a//b)

# 거듭제곱

a = 4
b = 2
print(4**2)


# 빈 리스트 만들기

a = list()
b = []
print(a)
print(b)
a = [1,2,3,4,5]

print(a)

print(a[2])

# 크기가 n인 1차원 리스트 만들기

n = 10
a = [0] * n
print(a)

# 리스트 맨뒤에서 접근

a = [1,2,3,4,5]
print(a[-1]) #5


# 리스트 컴프리핸션 == 대괄호 안에 조건문 반복문 가능!

array = [ i for i in range(20) if i % 2 == 1]

print(array)    

array = [ i * i for i in range(1,10) ]

print(array)

# n x m 크기의 2차원 리스트 초기화

n = 3
m = 4

array = [ [0] * m for _ in range(n)]

print(array)

# _는 반복을 위한 변수값을 무시해도될 때 사용하기 좋다

# 자연수는 표기하는게 좋지만 문자열은 상관 없음

for _ in range(5) :
    print("Hello")
    
    

# 리스트 관련 메서드

a = [1,2,3,4]


# 리스트 원소 삽입

a.append(2)
print("삽입 후 : " , a ) # 12342

# 오름차순 정렬

a.sort()
print("오름차순 정렬 후 ", a)

# 내림차순 정렬

a.sort(reverse = True)
print("내림차순 정렬 후 " , a)

# 리스트 원소 뒤집기

a.reverse()
print("뒤집은 후", a)

# 특정 인덱스에 값 추가

# 속도 느림, 남발 주의   시간초과됨

a.insert(2, 3)
print("2번 인덱스에 3 추가",a)

# 특정 값 데이터 갯수 세기

print("a에서 3 데이터 개수 : ", a.count(3))

# 특정 값 삭제

a.remove(2)

print("2 삭제후 값 : ",a)


# 특정값이 포함되지 않는 값만 저장

a = [1,2,3,4,5]
removeSet = [2,5]

a = [i for i in a if i not in removeSet ]
print(a)

# 큰따옴표 출력하고 싶다면 \사용하기

print("do you like \"pizza\"?")

# 문자열 * 정수는 ?

print("Stirng " * 3)

# 튜플 자료형은 수정이 불가하다

# 튜플은 () 사용

# 튜플은 리스트보다, 공간이 효율적, 원소 성질이 다를 때 사용

# 사전 자료형

data = dict()
data['사과'] = 'apple'
data['바나나'] = 'banna'
data['커커낫'] = 'coconut'

print(data)

# 리스트, 문자열, 튜블은 순차자료를 담는 자료형 == iterable 자료형

# in문법은 iterable 모두 사용가능

if '사과' in data : 
    print('사과를 키로 가지는 데이터 가 있오!')
else :
    print('그런 친구는 없는데?')
    

# keys() 키값 뽑기 // values() 밸류값 뽑기

# 키값만 담은 리스트

keyList = data.keys()

# 밸류값만 담은 리스트

valueList = data.values()

# 키에 따른 값 뽑아보기

for key in keyList :
    print(data[key])
    

# 집합 자료형 중복허용 하지않고, 순서가 없다.

# 인덱스 불가

# 특정 데이터 등장한적 있는지 체크할때 효과적

data = {1,2,3,4,4,5,5}
print(data)
data = set([1,2,3,4,4,5])
print(data)

# 합집합은 |, 교집합은 & 차집합은 - 

a = {1,2,3,4}
b = {2,3}

print("합집합 : ",a | b)
print("교집합 : ",a & b)
print("차집합 : ",a - b)

# 데이터 추가 .add(),

# 데이러 여러개 추가 .updata()

# 특정값 제거 .remove()


# 조건문

x = 10

if x>= 10 :
    print("10보다 같거나 크네요")
elif x < 10 :
    print("10보다 작아요!")
    

# 파이썬은 띄어쓰기 4번이 공식적이다 습관으로 만들자!

# 비교 연산자는 자바와 동일하다!

# 논리연산자 역시 자바와 동일!

# x in 리스트 => 리스트 안에 x가 있을 때 참

# x not in 리스트 => 리스트 안에 x가 없을 때 참

a = [1,2,3,4,5,6]
remove_set = [3,5]

a =[ i for i in a if i not in remove_set ]

print(a)

# 반복문


i = 1
result = 0

while i<= 9 :
    if i % 2 == 1 :
        result += i
    i += 1
    
print(result)    



# for문 range() 안에 숫자 하나면 0부터 시작

scores = [80, 90, 95, 98, 100]

for i in range(5) :
    if scores[i] >= 80 :
        print( i+1, "학생은 합격입니다.")
        

#  함수 와 람다식

# 람다식 함수를 매우 간단하게 작성 가능

def add (a, b) :
    return a + b

# 일반적인 add()메서드 사용

print(add(3,7))

# 람다로 구현 

print((lambda a,b: a+b)(3,7))



# 입출력

# list(map(int,intput().split()))


# 데이터 개수 입력

n = int(input())

# 각 데이터를 공백으로 구분하여 입력

data = list(map(int, input().split()))

data.sort(reverse = True)
print(data)


# n, m, k를 공백으로 구분하여 입력

n, m, k = map(int, input().split())
print(n,m,k)



# input보다 빠른 함수!

import sys

data = sys.stdin.readline().rstrip()
print(data)

# print ,가 띄어쓰기로 구분되어 출력// 기본 줄바꿈

# 파이썬 숫자 + 문자열일 경우

# 1. , 구분해주기

# 2. str() 묶어주기

# 3. f-string

answer = 7
print(f"정답은 {answer}입니다.")

# 내장 함수

# sum, min, max

# eval("수식") 계산해서 출력해줌!

# sorted(list) 오름차순

# sorted(list, revere = True) 내림차순


# itertool

# permutations => 모든 순열 구하기

from itertools import permutations
from itertools import combinations
from itertools import product
from itertools import combinations_with_replacement
data = {'a', 'b', 'c'}

result = list(permutations(data,3))

print(result)

# combinations => 조합 구하기

# product => 모든 순열 구하지만, 중복 허용

result = list(product(data, repeat=2))

print(result)

#combinations_with_replacement

# combinations와 같이 r개 데이터 뽑아  순서 고려하지 않고, 나열

result = list(combinations_with_replacement(data,2))

print(result)


import heapq
#heapq

#힙 원소 삽입 : heapq.heappush()
#힙 원소 꺼낼때 : heapq.heappop()
#힙 정렬 

def heapsort(iterable) :
    h = []
    result = []
    

    # 모든 원소 차례대로 힙 삽입
    for value in iterable:
        heapq.heappush(h, value)
    # 힙에 삽입된 모든 원소 차례대로 꺼내 담기    
    for i in range(len(h)) :
        result.append(heapq.heappop(h))
    return result

result = heapsort([1,3,5,7,9,2,4,6,8,0])
print(result)


# 내림차순 힙 정렬

# 원소 부호를 반대로 바꿨다가

# 꺼낼때 다사 바꿔주면 됨!

def heapReverseSort(iterable) :
    h = []
    result = []
    

    # 모든 원소 차례대로 힙 삽입
    for value in iterable:
        heapq.heappush(h, -value)
    # 힙에 삽입된 모든 원소 차례대로 꺼내 담기    
    for i in range(len(h)) :
        result.append(-heapq.heappop(h))
    return result

result = heapReverseSort([1,3,5,7,9,2,4,6,8,0])
print(result)



from itertools import permutations
from itertools import combinations
from itertools import product
from itertools import combinations_with_replacement

import heapq

from bisect import bisect_left, bisect_right

# 정렬된 배열에서 특정원소 찾을 때 매우 효과적


# bisect_left(a, x) : 정렬 유지하면서 리스트 a에 데이터 x를 삽입할 가장 왼쪽 인덱스를 찾는 메서드

# bisect_right(a, x) : 정렬 유지하면서 리스트 a에 데이터 x를 삽입할 가장 오른쪽 인덱스를 찾는 메서드

a = [1, 2,4,4,8]
x = 4

print(bisect_left(a,x))
print(bisect_right(a,x))


# 값이 [left_value, right_value]인 데이터 개수 반환 하는 함수

def count_by_range(a, left_value, right_value) :
    right_index = bisect_right(a, right_value)
    left_index = bisect_left(a, left_value)
    return right_index - left_index
    
    

# 리스트 선언

a = [1,2,3,3,3,3,4,4,8,9]

# 값이 4인 데이터 개수 출력

print(count_by_range(a,4,4))

# 값이 [-1, 3] 범위에 있는 데이터 개수 출력

print(count_by_range(a,-1,3))


# deque는 스택이나 큐 기능 모두 포함하고 있음

# 인덱싱과 슬라이싱 불가능하지만, 데이터의 끝과 시작에 데이터 삽입 삭제는 효과적

from collections import deque

data = deque([2,3,4])

# 맨왼쪽 추가

data.appendleft(1)

# 맨오른쪽 추가

data.append(5)

print(data)
print(list(data))

# Counter은 등장횟수 세는 기능

from collections import Counter

counter = Counter(['red','blue','red', 'green','blue','blue'])

print("blue가 등장한 횟수 : ",counter['blue'])

print(dict(counter))


# math

import math

# 5! 출력

print(math.factorial(5))

#x의제곱근 sprt(x)

# 최대 공약수 gcd(a,b)

# math.pi 파이 

# math.e 자연상수
