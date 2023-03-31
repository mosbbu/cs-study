# SQL Injection 🦠

악의적인 사용자가 임의의 SQL문으로 데이터베이스가 비정상적인 동작을 하도록 조작하는 행위

## 공격 종류 및 방법

### 1) Error based SQL injection

```sql
SELECT * FROM USERS WHERE ID = ''OR 1=1 --' AND Password = 'INPUT2'
```

- `'OR 1=1 --` 을 주입하여 WHERE절을 모두 참으로 만들고 뒤의 구문을 주석처리 하는 코드를 삽입하는 경우
- USER 테이블의 모든 정보를 조회하여 가장 먼저 만들어진 계정으로 로그인할 수 있게 된다. (주로 관리자 계정)

### 2) Union based SQL injection

```sql
SELECT * FROM BOARD WHERE Title LIKE '%'UNION SELECT null,id,password FROM USERS --%' AND contents '% UNION SELECT null,id,password FROM USERS -- %'
```

- 이 공격도 값에 대한 검증이 없기 때문에 발생한다

### 3) Blind SQL Injection

- 서버로부터 특정한 응답 대신 참/거짓 응답을 통해 DB의 정보를 유추하는 기법
- SLEEP과 BENCHMARK 함수를 주로 이용

---

### 정보 보안 개론 - 웹 보안

일반적인 로그인 과정은 사용자가 아이디와 패스워드를 입력한 후 이를 바탕으로 SELECT문을 실행한 결과값이 확인되면 해당 사용자의 이름을 넘겨 주고 로그인한다.

- SQL 결과값에 NULL이 나오지 않고 출력값이 나오게 하면 로그인에 성공할 수 있다는 취약점이 존재할 수 있다.
- SQL문에서 WHERE로 입력되는 조건 값에 `'or''='`을 입력하면 조건문을 항상 참으로 만들 수 있다. (`'or'1'='1`, `'or'='--` 과 같이 SQL문이 결과적으로 참이되는 모든 SQL문은 SQL 삽입 공격에 사용될 수 있다.
- 아래 예시와 같은 쿼리문이 만들어지면 WHERE문에서 패스워드 부분은 or 조건으로 인해 항상 만족되므로 사용자 인증에 성공하게 된다.

```sql
SELECT * FROM "USER"
WHERE email_address = 'aaa@bbb.com' and passowrd='' or ''=''
```

- SQL 삽입 공격은 로그인뿐만 아니라 사용자의 입력값을 토대로 DB에 데이터를 요청하는 모든 경우에 가능하다

## 2. 대응 방안

- 입력값 검증
- Prepared Statement 구문 사용
- 에러 메시지 노출 금지

---

## Reference

- [정보 보안 개론 4판](http://www.yes24.com/Product/Goods/102486031)
- [SQL Injection이란? (SQL 삽입 공격)](https://noirstar.tistory.com/264)
