## 🤞Join

`Join` : 둘 이상의 테이블을 연결하여 하나의 결과를 만들어내는 것

- 연결하고자 하는 테이블들이 적어도 하나의 컬럼을 공유하고 있어야 한다.
  - 공유하는 컬럼을 PK or FK 값으로 사용한다.

➡️ 두 테이블의 조인을 위해서는 기본키(PK)와 외래키(FK) 관계로 맺어져야 한다.

<br>

### Join의 종류

1. **INNER** JOIN
2. **LEFT OUTER** JOIN
3. **RIGHT OUTER** JOIN
4. **FULL OUTER** JOIN
5. **CROSS** JOIN
6. **SELF** JOIN

<br>

### 1. INNER JOIN

<img src="https://velog.velcdn.com/images/sukyeongs/post/088b2705-977a-43ca-a518-a1d5588655b0/image.png" height=300>

- **교집합**
- 기준 테이블과 join 테이블의 중복된 값을 보여준다.
- **두 테이블에 모두 지정한 열의 데이터**가 있어야 한다.

```SQL
SELECT A.ID, A.ENAME, A.KNAME
FROM A INNER JOIN B
ON A.ID = B.ID;
```

<br>

### 2. LEFT (OUTER) JOIN

<img src="https://velog.velcdn.com/images/sukyeongs/post/fc9861b8-208b-407e-b874-ea15071531b6/image.png" height=300>

- JOIN 기준 왼쪽에 있는 테이블 모두 SELECT 된다.
- 공통 부분 + 왼쪽 테이블 데이터

```SQL
SELECT A.ID, A.ENAME, A.KNAME
FROM A LEFT OUTER JOIN B
ON A.ID = B.ID;
```

<br>

### 3. RIGHT OUTER JOIN

<img src="https://velog.velcdn.com/images/sukyeongs/post/38d71ff2-0dfe-40c7-a1bc-e6d0ebcc9904/image.png" height=300>

- JOIN 기준 오른쪽에 있는 테이블 모두 SELECT 된다.
- 공통 부분 + 오른쪽 테이블 데이터

```SQL
SELECT A.ID, A.ENAME, A.KNAME
FROM A RIGHT OUTER JOIN B
ON A.ID = B.ID;
```

<br>

### 4. (FULL) OUTER JOIN

<img src="https://velog.velcdn.com/images/sukyeongs/post/a31c61f1-4ab1-4c14-93e0-4ba30326f1cd/image.png" height=300>

- **합집합**
- A 테이블의 데이터, B 테이블의 데이터 모두 SELECT

```SQL
SELECT A.ID, A.ENAME, A.KNAME
FROM A FULL OUTER JOIN B
ON A.ID = B.ID;
```

<br>

#### 5. CROSS JOIN

<img src="https://velog.velcdn.com/images/sukyeongs/post/9d634aa3-29b9-4070-869b-2c3ac85794c1/image.png" height=300>

- **모든 경우의 수**를 전부 표현하는 방식
- A 테이블의 데이터가 3개, B 테이블의 데이터가 4개인 경우, 총 3 \* 4 = 12개의 데이터가 검색된다.
- 대개 테스트로 사용할 **대용량의 테이블**을 생성할 경우에 사용된다.

```SQL
SELECT A.ID, A.ENAME, A.KNAME
FROM A
CROSS JOIN B
```

> ‼️ `CROSS JOIN`은 상호 모든 행에 대한 결합이 발생하는 것이므로, `ON` 구문을 사용할 수 없다.

<br>

#### 6. SELF JOIN

<img src="https://velog.velcdn.com/images/sukyeongs/post/82ba9814-3c23-4506-84bd-96374e2bfbda/image.png" height=300>

- **자기 자신과 조인**하는 것
- 하나의 테이블을 여러번 복사하여 조인하는 것과 같다.
  자신이 갖고 있는 컬럼을 다양하게 변형시켜 활용할 때 자주 사용한다.

<p align=center><img src="https://velog.velcdn.com/images/sukyeongs/post/d43bc96f-ed7e-47ad-b750-2e526863aa52/image.png" height=300>

- Output의 Manager는 모두 Input 데이터로부터 나온 것이다.
  ➡️ **테이블내 동일한 값이 다른 의미**를 갖는 경우(다른 컬럼에 존재하는 경우) 두 테이블을 서로 SELF JOIN시켜 정보를 확인할 수 있다.

<br>
