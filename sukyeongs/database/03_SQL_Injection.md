## 😈 SQL Injection

`SQL Injection` : 코드 인젝션의 한 기법으로, 클라이언트의 입력값을 조작하여 서버의 데이터베이스를 공격하는 공격방식

- 악의적인 사용자가 **보안상의 취약점**을 이용하여, 임의의 SQL 쿼리문을 데이터베이스에 주입해 비정상적인 동작을 하도록 조작하는 공격 기법이다.
- SQL 삽입, SQL 주입으로도 불린다.
- 공격이 비교적 쉬운 편이며, 공격에 성공할 경우 큰 피해를 입힐 수 있는 공격이다.

<br>

### ⚔️ 공격 방법

#### 1) Error based SOL Injection

![](https://velog.velcdn.com/images/sukyeongs/post/3eb27d09-6da7-4787-8245-bceba76d0a6c/image.png)

- **논리적 에러**를 이용한 SQL Injection
- 가장 많이 쓰이는 공격 기법이다.

위 사진은 해커가 임의의 SQL 구문(' OR 1=1 --)을 주입하여 SQL을 조작하고 있음을 보여준다.

- `OR 1=1` : 참으로 만든다. (원래는 id, password로 User find 해야함)
- `--` : 뒤에 오는 구문을 주석처리 한다 = password 검증을 못 하게 된다.

간단한 구문이지만, Users 테이블에 있는 **모든 데이터를 조회**함으로써 더 큰 피해를 발생시킬 수 있게 된다.

<br>

#### 2) Union based SQL Injection

![](https://velog.velcdn.com/images/sukyeongs/post/891e8105-917a-443a-944e-3234d4db30d2/image.png)

> **Union** : 두 개의 쿼리문에 대한 결과를 통합하여 하나의 테이블로 보여주는 키워드

- **Union** 명령어를 이용한 SQL Injection
- Union Injection이 성공하기 위해서는 1) Union 하는 두 **테이블의 컬럼 수가 같아야** 하고, 2) **데이터 타입이 같아야** 한다

위 사진의 Injection 구문에는 사용자의 id와 password를 요청하는 쿼리가 담겨 있다.

➡️ Injection이 성공하게 되면 사용자의 개인정보가 게시글과 함께 노출되게 된다.

<br>

#### 3) Blind SQL Injection - Boolean based SQL

![](https://velog.velcdn.com/images/sukyeongs/post/e2acae46-4270-4a04-8740-321253d97c7e/image.png)

- **Blind SQL Injection** : 데이터베이스로부터 특정한 값이나 데이터를 전달받지 않고, **참과 거짓**의 정보만 알 수 있을 때 사용한다.
- 서버가 응답하는 성공 or 실패 메시지를 이용하여 DB 테이블 정보 등을 추출한다.

<br>

#### 4) Blind SQL Injection - Time based SQL

![](https://velog.velcdn.com/images/sukyeongs/post/2d54e123-1080-4bc0-939c-23a541c801d7/image.png)

- 3과 마찬가지로 서버로부터 특정한 응답 대신 참 or 거짓의 응답을 통해 데이터베이스의 정보를 유추하는 기법이다.
- Time based SQL은 위 사진의 `SLEEP` 함수 같은 시간 관련 함수를 사용하여 주어진 조작 구문이 참이라면 SLEEP(2)가 동작, 거짓이라면 동작하지 않는다는 것을 원리로 SQL Injection 하는 것이다.

<br>

#### 5) Stored Procedure SQL Injection

> 💡 **Stored Procedure** : 일련의 쿼리를 마치 하나의 함수처럼 실행하기 위한 쿼리의 집합

- 저장된 Procedure에서의 SQL Injection
- 공격자가 시스템 권한을 획득해야 하므로 공격 난이도가 높다.
- 공격에 성공한다면 서버에 직접적인 피해를 입힐 수 있다.

<br>

#### 6) Mass SQL Injection

- 다량의 SQL Injection 공격 (`DDos`)
- 보통 데이터베이스 값을 변조하여 데이터베이스에 악성스크립트를 삽입해서, 사용자들이 변조된 사이트에 접속하면 좀비PC로 감염시키는 방법을 사용한다.

<br>

### 방어 방법

#### 1) 입력 값에 대한 검증

- 서버 단에서 `화이트리스트` 기반으로 SQL Injection에 사용되는 기법, 키워드인지 아닌지를 확인해야 한다.

> 🚫 블랙리스트로 검증하지 않는 이유?
>
> ➡️ 수많은 차단리스트를 등록해야 하며, 리스트에서 하나라도 빠지게 되면 공격에 성공하기 때문이다.

<br>

#### 2) Error Message 노출 금지

- 공격자가 SQL Injection을 수행하기 위해선 **DB 정보**(테이블명, 컬럼명 등)가 필요하다.
- 데이터베이스 관련 에러 발생 시 별다른 처리를 하지 않았다면 **에러가 발생한 쿼리문** + **에러 관련 내용**을 응답으로 반환한다.

→ 이 과정에서 **테이블명, 컬럼명, 쿼리문 등이 노출**될 수 있다.

➡️ 따라서 데이터베이스 관련 에러 발생 시 사용자에게만 보여지는 새로운 창을 띄우는 등 처리를 해야한다.

<br>

#### 3) Prepared Statement 사용

- Prepared Statement를 사용하면 사용자의 입력 값이 데이터베이스의 파라미터로 들어가기 전 **DBMS가 미리 컴파일**하여 실행하지 않고 대기한다.

➡️ 입력 값만을 문자열로 인식하여 공격쿼리가 입력으로 들어간다고 하더라도 의도대로 작동하지 않는다.

<br>

#### 4) 웹 방화벽 사용

- 웹 공격 방어에 특화된 **웹 방화벽**을 사용한다.

- **웹 방화벽** : SW형, HW형, Proxy형으로 나눌 수 있다.
  - **SW**형 : 서버 내에 직접 설치
  - **HW**형 : 네트워크 상에서 서버 앞 단에 하드웨어 장비로 설치
  - **Proxy**형 : DNS 서버주소를 웹 방화벽으로 바꿔, 서버로 가는 트래픽이 방화벽을 먼저 거치도록 만드는 방법

---

## Reference

- [신입 개발자 전공 지식 & 기술 면접 백과사전](https://gyoogle.dev/blog/computer-science/data-base/SQL%20Injection.html)
- https://noirstar.tistory.com/264
