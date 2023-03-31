## 🔗 Join

- 두 개 이상의 테이블을 묶어서 하나의 결과물을 만드는 것
- 두 개 이상의 테이블이나 데이터베이스를 연결하여 **데이터를 검색하는** 방법
- 보통 PK나 FK를 이용하여 두 테이블을 연결한다

<br/>

### 1) 내부 조인 (Inner join)

- 두 테이블 간의 교집합

```sql
SELECT
A.NAME,
B.AGE
FROM EX_TABLE A
INNER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP AND A.DEPT = B.DEPT
```

### 2) 왼쪽 조인 (Left outer join)

- 왼쪽 테이블을 기준으로 JOIN 하는 것이라 생각하면 된다
- 즉, A 테이블의 모든 데이터와 A 테이블과 B 테이블의 중복되는 값이 검색된다

```sql
SELECT
A.NAME,
B.AGE
FROM EX_TABLE A
LEFT OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP AND A.DEPT = B.DEPT
```

### 3) 오른쪽 조인 (Right outer join)

- 오른쪽 테이블을 기준으로 JOIN 하는 것이라 생각하면 된다
- 즉, B 테이블의 모든 데이터와 A 테이블과 B 테이블의 중복되는 값이 검색된다

```sql
SELECT
A.NAME,
B.AGE
FROM EX_TABLE A
RIGHT OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP AND A.DEPT = B.DEPT
```

### 4) 합집합 조인 (Full outer join)

- 두 테이블 간의 합집합 - A와 B 테이블의 모든 데이터가 검색된다

```sql
SELECT
A.NAME,
B.AGE
FROM EX_TABLE A
FULL OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP AND A.DEPT = B.DEPT
```

### 5) 크로스 조인 (Cross join)

- 모든 경우의 수를 전부 표현해 주는 방식이다
- 기준 테이블이 A일 경우, A의 데이터인 한 개의 Row를 B 테이블 전체와 JOIN 하는 방식이다

```sql
SELECT
A.NAME,
B.AGE
FROM EX_TABLE A,JOIN_TABLE B
```

### 6) 셀프 조인 (Self join)

- 자기 자신을 조인하는 것이다
- 자신이 가지고 있는 컬럼을 다양하게 변형시켜 활용할 때 사용된다

```sql
SELECT
A.NAME, --A테이블의 NAME조회
B.AGE --B테이블의 AGE조회
FROM EX_TABLE A,EX_TABLE B
```

<br/>

---

## Reference

- 2022-1 데이터베이스 전공 강의
- [면접을 위한 CS 전공지식 노트](http://www.yes24.com/Product/Goods/108887922)
- [JOIN의 종류설명 및 사용법 & 예제](https://coding-factory.tistory.com/87)
