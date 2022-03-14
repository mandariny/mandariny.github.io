---
layout: single
title: "[Algorithm / Java] 프로그래머스 입국심사"
---

**key word** : 이분 탐색, 이진 검색, Binary Search
<br><br>

## [문제](https://programmers.co.kr/learn/courses/30/lessons/43238#)

---

입국심사를 위해 기다리는 사람 n과 각각의 입국 심사대에 있는 심사원들의 심사 시간이 담긴 배열을 받아 모든 사람을 심사하는데 걸리는 최소 시간을 구하는 문제이다.

이진 검색 문제인걸 알고 접근했는데도 이런 유형의 문제를 거의 처음 풀다보니 풀이법을 찾기가 어려웠다. 뭘 기준으로 이진 탐색을 해야하는지 전혀 감이 안와 다른 사람들의 풀이를 참고했다.

<br><br>

## 아이디어

---

최소 시간을 구하는 문제라는 점을 상기하면 생각보다 쉽게 접근할 수 있는 문제였다. 그동안은 특정 배열에 대한 이진 탐색만 해봤기때문에 심사 시간의 배열을 가지고 풀어야하는 문제인가 고민하느라 시간을 허비했다. 총 심사 시간을 가지고 이진 탐색을 진행하며 각 시간마다 심사할 수 있는 사람의 수를 기준으로 탐색하면 되는 문제였다.

가능한 가장 오래 걸리는 시간은 n \* 최대 심사 시간이지만 times 배열을 정렬해야하므로 그냥 Long.MAX_VALUE를 최대 시간으로 집고 시작했다. 중간에 인원수를 세는 부분이 들어간다는 것 외에는 일반적인 이진 탐색 구현 방식과 같다.

<br><br>

## 구현

---

```
class Solution {
    public long solution(int n, int[] times) {
        return binarySearch(n, times);
    }

    public long binarySearch(int n, int[] times){
        long left = 0;
        long right = Long.MAX_VALUE;

        while(left <= right){
            long mid = (left + right) / 2;
            long sum = 0;

            for(int i : times){
                sum += mid / i;

                if(sum >= n)
                    break;
            }

            if(sum < n){
                left = mid + 1;
            }else{
                right = mid - 1;
            }
        }
        return right + 1;
    }
}
```

<br><br>

## 후기

---

이진 탐색 알고리즘 자체는 꽤 쉽다고 생각해서 금방 문제를 해결할 수 있을줄 알았는데 생각보다 많이 헤맸다. 역시 이론적으로 배웠다하더라도 실제로 문제에 적용해보고 활용해보지 않으면 내 것이 되지는 못하는 것 같다. 다양한 문제를 더 접해봐야겠다고 생각하는 계기가 됐다.
