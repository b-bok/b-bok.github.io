---
title: ORACLE 함수(FUNCTION)_PART01
date: 2020-08-12 22:08:11
category: oracle
draft: false
---
##   함수  FUNCTION

   - 자바로 치면 메소드 같은 존재
   - 전달값을 읽어 계산한 결과를 반환

    > 단일행 함수 : N개의 값을 읽어서 N개의 결과 리턴 ( 매 행마다 함수 실행 결과 반환)
    > 그룹 함수 : N개의 값을 읽어서 1개의 결과를 리턴 ( 하나의 그룹별로 함수 실행 결과 반환)
    
    * 단일 행 함수와 그룹함수는 함께 사용 할 수 없음 !! : 결과 행의 갯수 가 다르기 때문
    
    * 함수를 쓸 수 있는 위치 : SELECT 절, WHERE 절, ORDER BY 절 , GROUP BY 절, HAVING 절  


## 단일행 함수



### LENGTH(STRING) / LENGTHB(STRING)

 < 문자 관련 함수>
    * LENGTH / LENGTHB
    

    LENGTH(STRING) : 해당 문자의 글자 수 반환
    LENGTHB(STRING) : 해당 문자의 바이트 수를 반환    



결과값을 NUMBER 값으로 반환

 STRING : 문자에 해당하는 컬럼 | '문자값'

'가', '강', '나' 한글 한 글자당 3 BYTE로 취급

'A', 'a', '1', '!' 한 글자당 1BYTE로 취급

```plsql
SELECT LENGTH('오라클'), LENGTHB('오라클!')	-- 3 출력, 4 출력!
FROM DUAL; --> 가상테이블 (DUMMY TABLE)
```



### INSTR(STRING, '문자', [찾을위치의시작값, [순번] ]) 

([] = 생략 가능)

 문자열로부터 특정 문자의 위치값 반환
    

    INSTR(STRING, '문자', [찾을위치의시작값, {순번] ])
    => 결과값 NUMBER 타입
    
    > 찾을위치의 시작값
    1 : 앞에서부터 찾겠다! (기본값)
    -1 : 뒤에서부터 찾겠다!

```plsql
SELECT INSTR('AABAACAABBAA', 'B') FROM DUAL; -- 찾을 위치 시작값, 순번 생략시 앞에서부터 첫번째의 B의 위치값
-- 3
SELECT INSTR('AABAACAABBAA', 'B', 1) FROM DUAL; -- 위와 동일
-- 3
SELECT INSTR('AABAACAABBAA', 'B', -1) FROM DUAL;
-- 10
SELECT INSTR('AABAACAABBAA', 'B', 1, 2) FROM DUAL;
-- 9
SELECT INSTR('AABAACAABBAA', 'B', -1, 2) FROM DUAL;
-- 9
```



### SUBSTR(문자값, 시작위치, 얼마만큼?)

문자열로부터 특정 문자열을 추출해서 반환

 (자바로 치면 문자열.substring() 메소드와 유사)

    SUBSTR(STRING, POSITION, LENGTH)
    => 결과값 CHRACTER 타입 반환
    > STRING : 문자타입 컬럼 또는 '문자값'
    > POSITION : 문자열을 잘라낼 시작위치값
    > LENGTH : 추출할 문자 개수( 생략시 끝까지 의미)


```plsql
SELECT SUBSTR('SHOWMETHEMONEY', 7) FROM DUAL;	-- 7번째부터 모두 출력 THEMONEY
SELECT SUBSTR('SHOWMETHEMONEY',5, 2) FROM DUAL;	-- 5번째부터 두글자 ME
SELECT SUBSTR('SHOWMETHEMONEY',1, 6) FROM DUAL; -- 1번째부터 6글자 SHOWME
SELECT SUBSTR('SHOWMETHEMONEY',-8, 3) FROM DUAL; -- 시작위치를 음수값으로 제시하면 뒤에서부터 위치를 찾음 THE 출력
```



### LPAD/RPAD(문자값, 최종 문자길이(바이트), [덧불일 문자])

문자에 대해 통일감있게 보여주고자 할 때 사용



    LPAD/RPAD(STRING, 최종적으로 반환할 문자의 길이(바이트), [덧붙이고자하는 문자])
    => 결과값 CHARACTER 타입
    제시한 문자열에 임의의 문자를 왼쪽 또는 오른쪽 덧붙여 최종 N길이 만큼 문자열 반환
    > 덧붙이고자 하는 문자 생략시 기본값이 공백으로 처리

```plsql
-- 891201-2***** 형식으로 주민번호 출력      => 총 글자수 : 14글자, 숫자는 1BYTE
SELECT RPAD('891201-2', 14, '*') FROM DUAL;	

-- 함수 중첩으로 사용 가능
SELECT EMP_NAME, RPAD(SUBSTR(EMP_NO, 1, 8),14,'*') "주민번호 암호화"
FROM EMPLOYEE;
```



### LTRIM / RTRIM (문자값, [제거하고자하는 문자들] )

   문자열의 왼쪽 혹은 오른쪽에서 제거하고자하는 문자들을 찾아서 제거한 나머지 문자열을 반환

```plsql
SELECT LTRIM('     K H      ') FROM DUAL;	-- K H
SELECT LTRIM('00012345600', '0') FROM DUAL;	-- 12345600
SELECT LTRIM('123123KH123', '123') FROM DUAL; -- 해당하는 문자를 다 지운다! 순서 상관없이! -- KH123
SELECT LTRIM('ACABACCKH', 'ABC') FROM DUAL;  -- 해당하는 문자를 다 지운다! 순서 상관없이!  KH
SELECT LTRIM('578123KH', '0123456789') FROM DUAL; --  해당하는 문자를 다 지운다! 순서 상관없이!  KH
```



### TRIM

문자열의 앞/뒤/양쪽 있는 특정 문자를 제거한 나머지 문자열을 반환



```plsql
-- 기본적으로 양쪽에 있는 문자 제거
SELECT TRIM('  K H  ') FROM DUAL;   -- 제거하고자 하는 문자 생략시 기본값이 공백

SELECT TRIM('Z' FROM 'ZZZZKHZZZZ') FROM DUAL;

SELECT TRIM(LEADING'Z' FROM 'ZZZZKHZZZZ') FROM DUAL; -- LEADING : 앞		결과값 : KHZZZZ
SELECT TRIM(TRAILING'Z' FROM 'ZZZZKHZZZZ') FROM DUAL; -- TRAILING(후행) : 뒤	결과값 : ZZZZKH
SELECT TRIM(BOTH 'Z' FROM 'ZZZKHZZZ') FROM DUAL;    -- BOTH(양쪽) : 기본값	결과값 : KH

-- TRIM([LEADING|TRAILING|BOTH] ['제거하고 싶은 문자' FROM ] STRING)
-- => 결과값 CHARACTER 타입
```



### LOWER / UPPER / INITCAP



LOWER : 다 소문자로

UPPER : 다 대문자로

INITCAP : 단어 앞글자마다 대문자로 
    

    LOWER/UPPER/INITCAP (STRING = 특정 문자값, 문자 타입의 컬럼 값)



```plsql
SELECT LOWER('Welcome To My World') FROM DUAL;	-- 결과값 : welcome to my world
SELECT UPPER('Welcome To My World') FROM DUAL;	-- 결과값 : WELCOME TO MY WORLD
SELECT INITCAP('welcome to myworld') FROM DUAL; -- 공백을 기준으로 한 단어 판단 후, 앞글자를 대문자로 바꾼다. 
-- 결과값 : Welcome To Myworld
```



### CONCAT(문자값, 문자값)

CONCAT(STRING, STRING) : 두개 문자열 합치기!
=> 결과값 CHARACTER 타입



```plsql
SELECT CONCAT('가나다라','ABCD') FROM DUAL;	-- 결과값 : 가나다라ABCD
SELECT '가나다라' || 'ABCD' FROM DUAL;		-- 결과값 : 가나다라ABCD

-- SELECT CONCAT('가나다, 'ABC', 'DEF') FROM DUAL; CONCAT은 두개의 문자열만 가능
SELECT '가나다' || 'ABC' || 'DEF' FROM DUAL;
```



### REPLACE(문자값, 바꾸고싶은 부분 값, 바꿀 값)

REPLACE(STRING, STR1, STR2)

STRING으로 부터 STR1 찾아서 STR2로 바꾼 문자열을 반환



```plsql
SELECT REPLACE('서울시 강남구 역삼동', '역삼동', '삼성동') FROM DUAL;
-- 결과값  : 서울시 강남구 역삼동 --> 서울시 강남구 삼성동
```



