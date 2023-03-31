## 데이터베이스(Database)

---

### PK, FK란?

> PK : 기본키를 의미하는 Primary Key의 약자로, 한 릴레이션에서 튜플을 유일하게 구별할 수 있는 속성이다.
>
> FK : 외래키를 의미하는 Foreign Key의 약자로, 두 테이블을 서로 연결하는 데 사용되는 키이다.

<br>

### 조인의 의미, 조인의 종류

> 조인(Join) : 둘 이상의 테이블을 연결하여 데이터를 검색하는 것(하나의 결과를 도출하는 것)이다.
>
> 조인의 종류엔 `INNER JOIN`, `LEFT OUTER JOIN`, `RIGHT OUTER JOIN`, `FULL OUTER JOIN`, `CROSS JOIN`, `SELF JOIN` 이 있다.
>
> `INNER JOIN` : 교집합으로, 기존 테이블과 조인 테이블의 공통 부분을 나타낸다.
>
> `LEFT/RIGHT OUTER JOIN` : 공통 부분 + 왼/오른쪽의 데이터를 포함한다.
>
> `FULL OUTER JOIN`: 합집합으로, 기존 테이블과 조인 테이블의 모든 데이터를 포함한다.
>
> `CROSS JOIN` : 조인 가능한 모든 경우의 수를 나타낸다.
>
> `SELF JOIN` : 자기 자신과 조인하는 것을 의미한다.

<br>