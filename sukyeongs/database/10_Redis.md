## 🏬 Redis

**Redis** : **Key, Value** 구조의 비정형 데이터를 저장하고 관리하기 위한 오픈 소스 기반의 **비관계형 데이터베이스** 관리 시스템(DBMS)이다.

`데이터베이스`, `캐시`, `메시지 브로커`로 사용되며 **인메모리 데이터 구조**를 가진 저장소이다.

> **인메모리** 데이터 구조 : 컴퓨터의 **주 메모리**에 모든 조직 또는 개인의 **데이터를 저장**하는 구조

<br>

보통 데이터베이스는 하드 디스크나 SSD에 저장하지만, Redis는 메모리(RAM)에 저장하여 **디스크 스캐닝이 필요없어 매우 빠르다**는 장점이 있다.

➡️ **캐싱**도 가능하여 실시간 채팅에 적합하며 세션 공유를 위해 **세션 클러스터링**에도 활용된다.

<br>

**Single Treaded** 방식으로, 한 번에 하나의 명령만 처리할 수 있다. 따라서 중간에 처리 시간이 긴 명령어가 들어오면 그 뒤의 명령어들은 앞의 명령어가 처리될 때까지 대기가 필요하다.

<br>
<br>

### 가능한 Value

- **String** (text, binary data) - 가장 일반적인 key - value 구조 형태로 512MB까지 저장할 수 있다.
- **set** - String의 집합으로, 여러개의 값을 하나의 Value에 넣을 수 있다.
- **sorted set** - 정렬된 set
- **Hash**
- **List** - Array 형식이며 양방향 연결리스트도 가능하다.

<br>
<br>

### 백업 과정

**휘발성인 RAM**에 데이터베이스를 저장하는 구조이기에, 이를 막기 위한 백업 과정이 존재한다.

- **snapshot** : 특정 지점을 설정하고 디스크에 백업한다.
- **AOF(Append Only File)** : 명령이 실행될 때마다 해당 명령을 파일에 저장한다. (명령이 실행되자마자 작성하는 것이 아니라 버퍼에 두었다가 주기적으로 파일에 쓴다.)

<br>

---

<br>

## Reference

- <a href="https://gyoogle.dev/blog/computer-science/data-base/Redis.html">신입 개발자 전공 지식 & 기술 면접 백과사전</a>
- <a href="https://wildeveloperetrain.tistory.com/21">Redie란?</a>
- <a href="https://www.tibco.com/ko/reference-center/what-is-an-in-memory-database">인메모리 데이터베이스란 무엇입니까?</a>
