## 🫡 정규화(Normalization)

**정규화(Normalization)** : [이상현상](https://velog.io/@sukyeongs/Database-Anomaly)이 있는 릴레이션을 분해하여 이상현상을 없애는 과정

정규화는 이상현상이 존재하는 릴레이션을 **분해**하여 여러 개의 릴레이션을 생성한다.
정규화는 단계별로 구분되는데, **정규형 단계가 높아질수록 이상현상은 줄어든다**.

<br>

### 정규화의 목적

- **데이터의 중복을 없애면서** 불필요한 데이터를 최소화시킨다.
  → **무결성을 유지**할 수 있다.
- 데이터베이스 변경 시 **이상 현상(Anomaly)을 제거**할 수 있다.
- 테이블 구성을 논리적이고 직관적으로 할 수 있다.
- DB 저장 용량을 효율적으로 관리할 수 있다.

<br>

### 정규화 단계

정규화에는 여러가지 단계가 있으며, 대체적으로 **1~3단계** 정규화까지의 과정을 거친다.

<br>

#### 제1정규화(1NF)

`제1정규화`는 테이블 **컬럼**이 **원자값**(= 하나의 값)을 갖도록 테이블을 분리시키는 과정이다.

아래의 규칙들을 만족해야 한다.

> 1. 각 컬럼이 **하나의 속성**(원자값)만을 가져야 한다.
> 2. 하나의 컬럼은 **같은 종류나 타입**(type)의 값을 가져야 한다.
> 3. 각 컬럼이 **유일한**(unique) 이름을 가져야 한다.
> 4. 컬럼의 순서가 상관없어야 한다.

![](https://velog.velcdn.com/images/sukyeongs/post/5104e862-83df-4860-9eaf-64c7dce24427/image.png)

위 테이블에서, Customer ID가 123인 customer의 전화번호가 원자값이 아닌 2개의 값을 갖는다.
이런 경우 **제1정규화의 규칙을 만족하지 않는 것**이다.

제1정규화 규칙을 만족시키기 위해 아래와 같이 분해할 수 있다.
![](https://velog.velcdn.com/images/sukyeongs/post/c1e676f6-fb4d-4bde-a8c7-32b8d6a7204b/image.png)

<br>

#### 제2정규화(2NF)

`제2정규화`는 테이블의 모든 컬럼이 **완전 함수적 종속을 만족**하도록 하는 과정이다.

쉽게 말하자면, 테이블에서 기본키가 복합키로 묶여있는 경우 두 키 중 **하나의 키만으로 다른 컬럼을 결정지을 수 있으면 안 된다**는 것이다.

즉, 기본키의 부분집합 키가 결정자가 되어선 안 된다는 것이다.

아래의 규칙들을 만족해야 한다.

> 1. **제1정규형**을 만족해야 한다.
> 2. 모든 컬럼이 **완전 함수 종속**을 만족해야 한다.

![](https://velog.velcdn.com/images/sukyeongs/post/7c51c27f-cbb3-4333-8576-9a7ceff732ec/image.png)

위 테이블은 `Manufacturer` 필드와 `Model` 필드를 기본키로 하고 있다.

그 중 Manufacturer Country 필드는 Model 이 무엇이든 상관없이, Manufacturer 에 따라 결정된다.
즉, Model이 없어도 `Manufacturer` 만 알면 `Manufacturer Country`를 알 수 있다.

이는 Manufacturer Country 컬럼이 (Manufacturer, Model)에 종속되지 않고 **Manufacturer에만 종속**되는 `부분 종속`인 상태인 것이다. **완전 함수적 종속을 충족시키지 못하고 있다**는 의미이다.

제2정규화 규칙을 만족시키기 위해 아래와 같이 분해할 수 있다.
![](https://velog.velcdn.com/images/sukyeongs/post/7c00def3-45c3-43d3-b17d-4bb10863e5ff/image.png)

<br>

#### 제3정규화(3NF)

`제3정규화`는 제2정규화가 진행된 테이블에서 **이행적 종속**을 없애기 위해 테이블을 분리하는 과정이다.

> 이행적 종속 : A → B, B → C 면 A → C 가 성립한다. 쉽게 말하자면 삼단논법

아래의 규칙들을 만족해야 한다.

> 1. **제2정규형**을 만족해야 한다.
> 2. 기본키를 제외한 속성들 간의 **이행 종속성(Transitive Dependency)이 없어야** 한다.
>    즉, 기본키가 아닌 속성들은 **기본키에 의존**해야 한다.

![](https://velog.velcdn.com/images/sukyeongs/post/a3599860-6dbc-4d57-b4f3-cf52fb18a29c/image.png)

위 테이블은 `Tournament`와 `Year`을 기본키로 하고 있다.

`Winner`는 이 두 복합키를 통해 결정된다. 즉, **Tournament**와 **Year** 속성을 알면 해당 레코드의 Winner 속성도 알 수 있다.

그러나 `Winner Date of Birth` 는 **Winner** 속성 값에 의해 결정된다.

이는 **Tournament, Year** 속성 값을 알면 Winner Date of Birth 속성 값도 알 수 있음을 의미한다.

> Tournament, Year → Winner
> Winner → Winner Date of Birth
> ➡️ Tournament, Year → Winner Date of Birth

제3정규화 규칙을 만족시키기 위해 아래와 같이 분해할 수 있다.
![](https://velog.velcdn.com/images/sukyeongs/post/bd6fe90b-1408-48e2-a12f-9479d6113de6/image.png)

<br>

#### BCNF(Boyce-Codd Normal Form)

`BCNF` 는 제3정규형을 좀 더 강화한 버전이다.

아래의 규칙들을 만족해야 한다.

> 1. 제3정규형을 만족해야 한다.
> 2. 모든 결정자가 후보키 집합에 속해야 한다.
>    → 후보키 집합에 없는 컬럼이 결정자가 되어서는 안된다.

<br>

#### 제4정규화 이상

![](https://velog.velcdn.com/images/sukyeongs/post/682aefc4-4225-4b85-a42f-6786294b715a/image.png)

보통 BCNF 까지만 하는 경우가 많으며, 그 이상 정규화를 진행한다면 정규화의 단점이 나타날 수도 있다.

<br>

---

<br>

## Reference

- <a href="https://gyoogle.dev/blog/computer-science/data-base/Normalization.html" target="_blank"> 신입 개발자 전공 지식 & 기술 면접 백과사전 </a>
- <a href="https://code-lab1.tistory.com/48" target="_blank"> 정규화(Normalization)란?</a>
