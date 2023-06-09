## Transaction ⚡️

데이터베이스의 상태를 변화시키기 위해 수행하는 작업 단위

- 동시성 제어: 다수의 사용자가 데이터베이스에 동시에 접근하도록 허용하면서 데이터베이스의 일관성을 유지함
- 회복: 데이터베이스를 갱신하는 도중에 시스템이 고장나도 데이터베이스의 일관성을 유지함
- 기본적으로 각각의 SQL 문이 하나의 트랜잭션으로 취급됨

<br/>

### 트랜잭션의 특성 (ACID 특성)

**원자성 (Atomicity)**

- 한 트랜잭션 내의 모든 연산들이 완전히 수행되거나 전혀 수행되지 않음 (All or Nothing)

**일관성 (Consistency)**

- 어떤 트랜잭션이 수행되기 전 DB가 일관된 상태를 가졌다면 트랜잭션이 수행된 후에도 DB는 또 다른 일관된 상태를 가짐 (트랜잭션 수행 중에는 일시적인 불일치 상태 발생)

**고립성 (Isolation)**

- 한 트랜잭션이 데이터를 갱신하는 동안 이 트랜잭션이 완료되기 전에는 갱신 중인 데이터를 다른 트랜잭션들이 접근하지 못하도록 해야 함

**지속성 (Durability)**

- 일단 한 트랜잭션이 완료되면 이 트랜잭션이 갱신한 것은 그 이후에 시스템이 고장나더라도 손실되지 않음

💡 동시성 제어 모듈은 일관성, 고립성 보장
💡 회복 모듈은 원자성, 지속성 보장
💡 무결성 제약 조건은 일관성 보장

<br/>

### 트랜잭션의 완료와 철회

- 완료(COMMIT): 트랜잭션에서 변경하려는 내용이 DB에 완전하게 반영됨 (성공적인 종료)
- 철회(ROLLBACK): 트랜잭션에서 변경하려는 내용이 DB 일부에만 반영된 경우, 원자성을 보장하기 위해 트랜잭션이 갱신한 사항을 이전으로 되돌림 (비성공적인 종료)

<br/>

---

<br/>

## Reference

- 2022-1 데이터베이스 전공 강의
