## 📈 트랜잭션 격리 수준

**트랜잭션 격리 수준** : 트랜잭션에 **일관성 없는 데이터를 허용**하도록 하는 수준

<br>
<br>

### 트랜잭션 격리 수준의 필요성

데이터베이스는 ACID 특징과 같이, 트랜잭션이 **독립적인 수행**을 하도록 한다.

따라서 `Locking`을 통해 트랜잭션이 DB를 다루는 동안 **다른 트랜잭션이 관여하지 못하도록** 막는 것이 필요하다.

하지만 무조건 Locking으로 동시에 수행되는 수많은 트랜잭션들을 순서대로 처리하는 방식으로 구현하게 되면 **데이터베이스의 성능**은 떨어지게 될 것이다.

그렇다고 성능을 높이기 위해 Locking의 범위를 줄인다면 **잘못된 값이 처리**될 문제가 발생하게 된다..!

➡️ **최대한 효율적인 Locking 방법**이 필요하다 !

<br>
<br>

### 트랜잭션 격리 수준의 종류

#### 1. Read Uncommitted (Level 0)

![](https://velog.velcdn.com/images/sukyeongs/post/760c6005-b24e-4ea6-abc1-1d35e20b2d07/image.png)

`Read Uncommitted` 단계는 **SELECT** 문장이 수행되는 동안 해당 데이터에 **Shared Lock이 걸리지 않는** 단계이다.

각 트랜잭션에서의 변경 내용이 `Commit` 인지 `Rollback` 인지의 여부에 **상관없이** 다른 트랜잭션에서 값을 읽을 수 있다.

> **Shared Lock**(공유잠금)
>
> - 읽기 잠금(Readlock)이라고도 불린다.
> - 리소스를 다른 사용자가 **동시에 읽을 수 있게** 하되 **변경은 불가**하게 하는 것이다.

트랜잭션이 처리중이거나 아직 Commit 되지 않은 데이터를 다른 트랜잭션이 읽는 것을 허용한다.

➡️ 데이터베이스의 일관성을 유지하는 것이 불가능하다.

<br>

#### 2. Read Committed(Level 1)

![](https://velog.velcdn.com/images/sukyeongs/post/673db2cc-07f7-4d31-a230-5513e046a026/image.png)

`Read Committed` 단계는 **SELECT** 문장이 수행되는 동안 해당 데이터에 **Shared Lock이 걸리는** 단계이다.

**Commit이 이루어진 트랜잭션만 조회** 가능하며,
트랜잭션이 수행되는 동안 다른 트랜잭션이 접근할 수 없어 대기하게 된다.

위의 이미지에서, Busan을 Jeju로 업데이트 하는 과정에서 Busan을 조회하는 명령어가 들어온다면, **Undo 영역에 백업된 레코드 값**을 가져온다.
➡️ 따라서 Jeju를 조회하는 것이 아니라 Busan을 읽게 된다. (아직 Jeju로 바뀌는 중이므로 = Uncommitted 상태이므로)

대부분의 **SQL 서버가 Default로 사용**하는 Isolation Level이다. (MySQL은 Level 2가 기본값)

<br>

#### 3. Repeatable Read(Level 2)

![](https://velog.velcdn.com/images/sukyeongs/post/0eeb1f30-fe0d-428e-9c08-fcc2ae51f4f3/image.png)

`Repeatable Read` 단계는 트랜잭션이 완료될 때까지 **SELECT** 문장이 사용되는 **모든 데이터에 Shared Lock**이 걸리는 단계이다.

MySQL에서는 트랜잭션마다 트랜잭션 ID를 부여하여, **트랜잭션 ID보다 작은 트랜잭션 번호에서 변경한 것**만 읽게 된다.

> Level 2는 MySQL에서 Default로 사용하는 Isolation Level이다.

**Undo 영역에 백업**해두고 실제 레코드 값을 변경한다.

> 백업된 데이터가 많아지면 MySQL 서버의 처리 성능이 떨어질 수 있으므로 백업된 데이터가 불필요하다고 판단되는 시점에 주기적으로 삭제한다.
>
> 이러한 변경 방식을 `MVCC`(Multi Version Concurrency Control)이라고 부른다.

트랜잭션이 범위 내에서 조회한 데이터 내용이 항상 동일함을 보장한다.

다른 사용자는 트랜잭션 영역에 해당되는 데이터에 대한 수정이 불가능하다.

<br>

#### 4. Serializable(Level 3)

`Serializable` 단계는 완벽한 읽기 일관성 모드를 제공하며, 가장 단순한 격리수준이지만 가장 엄격한 격리 수준이다.

성능 측면에서는 동시 처리성능이 가장 낮으며, 거의 사용되지 않는다.

<br>
<br>

### ‼️ 격리 수준 선택 시 고려사항

Isolation Level에 대한 조정은 동시성과 데이터 무결성에 연관되어 있다.

동시성을 증가시키면 데이터 무결성에 문제가 발생하고, 데이터 무결성을 유지하면 동시성이 떨어지게 된다.

#### 낮은 단계 Isolation Level을 사용할 때 발생하는 현상

- **Dirty Read**

  - 커밋되지 않은, 수정 중인 데이터를 다른 트랜잭션이 읽을 수 있도록 허용할 때 발생하는 현상
  - 발생 Level: `Read Uncommitted`

- **Non-Repeatable Read**

  - 한 트랜잭션에서 같은 쿼리를 두 번 수행할 때 그 사이에 다른 트랜잭션 값을 수정 or 삭제하면서 두 쿼리의 결과가 상이하게 나타나는, 일관성이 깨진 현상
  - 발생 Level: `Read Uncommitted` , `Read Committed`

- **Phantom Read**
  - 한 트랜잭션 안에서 일정 범위의 레코드를 두 번 이상 읽었을 때, 첫번째 쿼리에서 없던 레코드가 두번째 쿼리에서 나타나는 현상
  - 트랜잭션 도중 새로운 레코드 삽입을 허용하기 때문에 나타나는 현상이다.
  - 방지하기 위해서는 쓰기 잠금을 걸어야 한다.
  - 발생 Level: `Read Uncommitted` , `Read Committed` , `Repeatable Read`

<br>

---

<br>

## Reference

- <a href="https://gyoogle.dev/blog/computer-science/data-base/Transaction%20Isolation%20Level.html">신입 개발자 전공 지식 & 기술 면접 백과사전</a>
- <a href="https://jeong-pro.tistory.com/94">Exclusive lock과 Shared lock의 차이</a>
- <a href="https://nesoy.github.io/articles/2019-05/Database-Transaction-isolation">트랜잭션의 격리 수준이란?</a>
