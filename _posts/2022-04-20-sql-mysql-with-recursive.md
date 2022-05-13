---
layout: single
title: "[MySQL] WITH"
---

**key word** : mysql, with recursive, with, cte

<br><br>

프로그래머스에서 sql [문제](https://programmers.co.kr/learn/courses/30/lessons/59413)를 풀다가 처음 알게 된 문법이다. 0시부터 23시까지 시간대별로 입양이 이뤄진 건수를 출력해야하는데 데이터에 새벽 시간대가 없었다. 그래서 0시부터 23시까지의 테이블을 만들고 조인을 해야하는데 WITH RECURSIVE를 이용해 테이블을 만들어 사용하는 사람이 있었다. 새로 알게 된 문법이라 정리해보려고 한다.

<br><br>

## WITH

MySQL의 WITH절은 CTE(Common Table Expression)을 구현하기 위한 구문이다. MySQL 8.0 이후부터만 사용 가능하니 주의해야 한다. CTE는 한 구문 내에서 사용할 수 있는 임시 테이블이라고 생각할 수 있다. 즉 WITH을 이용해 임시로 테이블을 만들어 사용하고, 구문이 끝날 때 자연히 소멸시킬 수 있다. 기본적인 구현은 다음과 같이 한다.

```
WITH cte_name (col1, col2 ...)
AS(
    query
)
SELECT * FROM cte_name;
```

```
WITH
  cte1 AS (SELECT a, b FROM table1),
  cte2 AS (SELECT c, d FROM table2)
SELECT b, d FROM cte1 JOIN cte2
WHERE cte1.a = cte2.c;
```

1. SELECT 외에 UPDATE, DELETE도 가능하지만 주로 SELECT를 사용한다.
2. 한 번에 여러 cte를 만들어 사용할 수 있다.
3. 서브쿼리에서도 사용이 가능하다.
4. ISERT, REPLACE 등과 같이 SELECT문을 사용하는 구문 내에서 SELECT 바로 앞에 사용 가능하다.

<br><br>

## WITH RECURSIVE

WITH RECURSIVE는 재귀적으로 cte를 구성하고 사용할 때 사용하는 구문이다. 서브쿼리에서 자기 자신을 참조한다.

```
WITH RECURSIVE cte (n) AS
(
  SELECT 1
  UNION ALL
  SELECT n + 1 FROM cte WHERE n < 5
)
SELECT * FROM cte;
```

1. WITH절 안에서 자기 자신을 참조하는 경우에는 항상 RECURSIVE를 함께 명시해줘야한다.
2. RECURSIVE CTE에서는 UNION ALL이나 UNION(UNION DISTINCT)로 나눠지는 두 서브쿼리가 존재하게 된다. 첫 번째 서브쿼리에는 행의 초기값을, 두 번째 서브쿼리에서는 이어질 행을 정의한다.

<br><br>

## 참고

이것이 MySQL이다(개정판), 우재남, 한빛미디어, 2021
<br>
https://dev.mysql.com/doc/refman/8.0/en/with.html#common-table-expressions
