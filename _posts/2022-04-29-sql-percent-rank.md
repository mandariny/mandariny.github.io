---
layout: single
title: "[SQL] PERCENT_RANK()"
---

**key word** : mysql, percent_rank

<br><br>

MySQL에서 이용 가능한 window 함수이다. MySQL의 document를 보면 각 행에 대해 관련있는 행을 이용해 계산하는 함수라고 한다. 집계함수는 아니지만, 다른 행들을 이용해 각 행을 계산할 수 있는 함수라고만 일단 이해했다. 다른 글들을 참고해보니 집계함수와 달리 계산된 내용을 테이블에 추가한다고 한다.

<br><br>

## PERCENT_RANK()

window함수 중에서도 각 행이 해당 열의 값들 중 몇 퍼센트에 포함되는지 구할 수 있는 함수이다. Oracle의 경우 median() 등을 이용해 중앙값을 찾을 수 있지만 MySQL에서는 지원하지 않아 이런 함수를 활용해야 한다.

```
PERCENT_RANK ()
OVER (
    [PARTITION BY partition_expression]
    [ORDER BY order_list]
)
```

위와 같은 형태로 사용한다. 반환값은 0~1 사이의 실수이다.

- `PARTITION BY`는 `GROUP BY`와 같은 용도로 사용되고
- `ORDER BY`는 해당 열을 정렬해 함수를 적용하고자 할 때 사용한다. 일단 옵션이긴 하지만 PERCENT_RANK()에서 ORDER BY를 지정하지 않으면 모든 행에 대해 0이 반환된다. 사실상 제대로 사용하려면 꼭 지정해줘야하는 부분이다.

<br><br>

## Formula

PERCENT_RANK()가 해당 행의 백분위값을 구할 때 사용하는 공식은 다음과 같다.

`(x - 1) / (the number of rows in the window or partition -1)`

x는 계산하려는 현재 행의 순위이고, x에서 1을 뺀 값을 전체 행의 수 혹은 그룹화한 행의 수에서 1을 뺀 값으로 나누어준다.

<br><br>

## 참고

왜인지 MySQL document보다도 AWS의 document가 더 자세했다.

https://docs.aws.amazon.com/redshift/latest/dg/r_WF_PERCENT_RANK.html
