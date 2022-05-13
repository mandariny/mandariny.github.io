---
layout: single
title: "[SQL] 조건문"
---

**key word** : mysql, conditional, if, case

<br><br>

구문 내에서 조건문을 사용하는 방식에 대해 정리한다. MySQL을 기준으로 정리하지만 다른 DB에서도 비슷하게 동작할 것이라 생각한다.

<br><br>

## IF

IF(조건, 참, 거짓)
`SELECT IF(1 > 5, 'TRUE', 'FALSE');`

중첩 사용도 가능하다.

<br><br>

## CASE ... WHEN

CASE <br>
WHEN 조건1 <br>
THEN 실행1 <br>
WHEN 조건2 <br>
THEN 실행2 <br>
ELSE 실행3 <br>
END

```
SELECT
    CASE
        WHEN a > b
        THEN 'a'
        WHEN a = b
        THEN 'equal'
        ELSE 'b'
    END
FROM TABLE;
```
