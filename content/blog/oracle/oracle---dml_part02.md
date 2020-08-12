---
title: ORACLE - DML_PART02
date: 2020-08-12 22:08:16
category: oracle
draft: false
---
## SELECT



### BETWEEN END

몇이상 몇이하의 범위에 대한 조건 제시할 때 사용

```plsql
[표현법]
WHERE 비교대상 컬럼명 BETWEEN 조건 AND 조건;
```

```plsql
-- 350만 이상, 600 이하의 경우
SELECT EMP_NAME, EMP_ID, JOB_CODE

FROM EMPLOYEE

WHERE SALARY BETWEEN 3500000 AND 6000000;

-- 350 미만, 600 미만 일경우에는

WHERE SALARY NOT BETWEEN 3500000 AND 6000000;

-- BETWEEN AND 연산자는 DATE 형식에도 사용가능

-- 입사일 '90/01/01' ~ '01/01/01' 사원 컬럼 조회

SELECT *

FROM EMPLOYEE

WHERE HIRE DATE BETWEEN '90/01/01' AND '01/01/01';
```



#### LIKE

비교하려는 컬럼 값이 내가 지정한 특정 패턴에 만족될 경우 조회

- 특정패턴에 '%', '_'를 와일드 카드로 사용 할 수 있음

  > '%' : 0글자 이상
  >
  > EX) 	비교대상컬럼명 LIKE '문자%' => 컬럼값 중에 '문자 '로 시작되는 것을 조회한다!
  > 		 비교대상컬럼명 LIKE '%문자' => 컬럼값 중에 '문자'로 끝나는 것을 조회한다!
  >   	 비교대상컬럼명 LIKE '%문자%' => 컬럼값 중에 '문자'가 "포함"되는 것을 조회

    > '' : 1글자
    > EX)    비교대상컬럼명 LIKE '문자' => 컬럼값 중에 '문자 '앞에 무조건 한글자가 올 경우 조회!
    >   	비교대상컬럼명 LIKE '__문자' => 컬럼값 중에 '문자 '앞에 무조건 두글자가 올 경우 조회!



```plsql
-- 이름 중 '중' 가 포함된 사원 사원명 , 주민번호, 부서코드 조회
 SELECT EMP_NAME, EMP_NO, DEPT_CODE
 FROM EMPLOYEE
 WHERE EMP_NAME LIKE '%중%';

-- 전화번호 5번째 자리가 3로 시작하는 사원들의 사번, 사원명, 전화번호, 이메일 조회
SELECT EMP_ID, EMP_NAME, PHONE, EMAIL
FROM EMPLOYEE
WHERE PHONE LIKE '____3%';

-- 이메일 중에 _앞글자가 3글자인 이메일 주소를 가진 사원들의 사번, 이름, 이메일 조회
-- 이메일 4번째 자리가 _로 시작하는 사원
SELECT EMP_ID, EMP_NAME, EMAIL
FROM EMPLOYEE
WHERE EMAIL LIKE '___$_%' ESCAPE '$';  -- 와일드 카드로 사용되는 문자와 실제 담겨있는 컬럼값이 동일할 경우 문제 발생
-- WHERE EMAIL LIKE '___^_%' ESCAPE '^'; -- 와일드 카드로 ^ 사용한 경우

-- 어떤게 와일드 카드고 어떤게 데이터 값인지 구분지어주면됨!!
-- 와일드 카드로 $를 사용했습니다!
-- 데이터값으로 인식시킬 값 앞에 임의로 나만의 와일드 카드 제시, 나만의 와일드카드를 ESCAPE로 등록
```



### IS NULL / IS NOT NULL


    [표현법]
    비교대상컬럼 IS NULL : 컬럼값이 NULL일 경우
    비교대상컬럼 IS NOT NULL : 컬럼값이 NULL이 아닐 경우


```plsql
-- 보너스 받지 않는 사원 사번, 이름 급여, 보너스
SELECT EMP_ID, EMP_NAME, SALARY, BONUS
FROM EMPLOYEE
WHERE BONUS IS NULL;

-- 보너스를 받는 사원을 조회하겠다!
SELECT EMP_ID, EMP_NAME, SALARY, BONUS
FROM EMPLOYEE
WHERE BONUS IS NOT NULL;
```



### IN

 비교대상컬럼값에 목록들 중에 일치하는 값이 있는지

```plsql
[표현법]
    비교대상 컬림 IN (값, 값, 값, ....)
```



```plsql
-- 부서코드가 D6이거나 또는 D8이거나 또는 D5인 사원들의 사원명, 부서코드, 급여 조회

SELECT EMP_NAME, DEPT_CODE, SALARY
FROM EMPLOYEE
WHERE DEPT_CODE IN ('D6', 'D8', 'D5');

-- 그 외인 사원들?

SELECT EMP_NAME, DEPT_CODE, SALARY
FROM EMPLOYEE
-- WHERE NOT DEPT_CODE IN ('D6', 'D8', 'D5');
WHERE DEPT_CODE NOT IN ('D6', 'D8', 'D5');
```



### 연결 연산자 ||

- 여러 컬럼값들을 하나의 컬럼인것처럼 연결시켜주는 연산자
- 컬럼과 리터럴 (임의의 문자열)을 연결할 수도 있다.

```java
-- System.out.println("num : " + num);
-- +와 같은 역할이라고 보면 된다!
```



```plsql
-- 사번, 사원명, 급여를 하나의 컬럼으로 합쳐서 조회
SELECT EMP_ID || EMP_NAME || SALARY
FROM EMPLOYEE;

-- XXX번 XXX의 월급은 XXXXX원입니다.
SELECT EMP_ID || '번 ' || EMP_NAME || '의 월급은 ' || SALARY || '원입니다.' AS "월급명세서"
FROM EMPLOYEE;
```



#### 꿀팁!

    <연산자 우선순위>
    0. ()
    1. 산술연산자
    2. 연결연산자
    3. 비교연산자
    4. IS NULL,     LIKE,      IN
    5. BETWEEN AND
    6. NOT
    7. AND(논리연산자)
    8. OR(논리연산자)


### ORDER BY

-  SELECT문 가장 마지막에 기입하는 구문
-  SELECT문 가장 마지막에 작성하는 것 뿐만아니라 실행 순서 역시 가장 마지막에 동작

```
 [표현법]
    SELECT 조회할 컬럼, 컬럼.....
    FROM 조회할 테이블 명
    WHERE 조건식
    ORDER BY 정렬시키고자하는컬럼명 |별칭| 컬럼 순번 [ASC | DESC]    [NULLS FIRST|NULLS LAST]
```

​    

    - ASC : 오름차순 정렬 (생략시 기본값)
    - DESC :  내림차순 정렬 
    
    - NULLS FIRST : 정렬하는 컬럼값에 NULL 을 맨앞으로 정렬
    - NULLS LAST :  정렬하는 컬럼값이 NULL 을 맨뒤로 정렬


​    
​    ** 실행 순서 **
​    1. FROM 절
​    2. WHERE 절
​    3. SELECT 절
​    4. ODER BY 절


```plsql
-- 전 사원들을 보너스별 오름차순 정렬 조회
SELECT *
FROM EMPLOYEE
-- ORDER BY BONUS; -- ASC 또는 DESC 생략시 기본값이 ASC

--ORDER BY BONUS ASC; -- 오름차순 정렬은 기본적으로 NULLS LAST
--OREDER BY BONUS ASC NULLS FIRST;
--ORDER BY BONUS DESC; -- 내림차순 정렬은 기본적으로 NULLS FIRST
ORDER BY BONUS DESC, SALARY ASC; -- 첫번째 제시한 정렬 컬럼값이 일치할 경우, 두번째 제시한 정렬기준을 가지고 정렬

-- 연봉별 내림차순 정렬로 조회(사원명, 연봉)
SELECT EMP_NAME, SALARY*12 연봉
FROM EMPLOYEE
--ORDER BY 연봉 DESC; -- 별칭 사용
ORDER BY 2 DESC;    -- 컬럼 순번 역시 사용 가능
```




