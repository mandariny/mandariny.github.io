---
layout: single
title: "[Algorithm / Java] 프로그래머스 타켓 넘버"
---

**key word** : BackTracking, DFS
<br><br>

## [문제](https://programmers.co.kr/learn/courses/30/lessons/43165)

정수의 배열과 타켓인 정수가 각각 주어졌을 때, 배열의 순서 등을 바꾸지 않고 오로지 더하거나 빼는 것만으로 타겟 정수를 만들 수 있는 경우의 수를 구하는 문제이다.
<br><br>

## 아이디어

따로 정리하진 않았지만 [백준 1182번 부분수열의 합](https://www.acmicpc.net/problem/1182) 문제의 풀이와 유사하다고 생각했다.

당시에는 유튜브에서 바킹독님의 풀이를 보고 참고해서 풀었는데, 부분 수열의 모든 경우의 수는 2의 n제곱승으로 n은 원소의 개수이다. 각 원소를 기준으로 생각해보면 부분수열에 들어가거나, 들어가지 않거나 둘 중 하나이기 때문이다. 결론적으로 문제를 풀 때 해당 원소가 들어가는 경우와 들어가지 않은 경우에 대해 각각 재귀 함수를 호출하는 방식으로 문제를 풀었다.

이 문제 또한 각 원소에 해당하는 정수가 +이거나 -인 상황이고 모든 경우의 수 중에 결과로 타겟 정수를 만드는 경우를 카운트해주면 된다고 생각했다.

<br><br>

## 구현

```
class Solution {
    public int answer = 0;

    public int solution(int[] numbers, int target) {
        recursion(numbers, target, 0, 0);

        return answer;
    }

    public void recursion(int[] numbers, int target, int k, int sum){
        if(k == numbers.length){
            if(sum == target) answer++;
            return;
        }

        recursion(numbers, target, k + 1, sum + numbers[k]);
        recursion(numbers, target, k + 1, sum - numbers[k]);
    }
}
```

<br><br>

## 후기

확실히 프로그래머스는 입력을 따로 받지 않아도 돼서 코드가 훨씬 짧아진다. 간만에 오류 없이 깔끔하게 푼데다가 한 번 배운걸 기억해내 사용한 거라 풀고 나서 더 뿌듯함이 느껴졌다.

DFS로 풀었다는 풀이도 봤는데 아직 알고리즘의 개념이 좀 덜 잡혔는지 그 풀이가 내가 BackTracking으로 푼 것과 매우 유사하다고 느껴졌다. 문제 풀이에 개념 공부도 더 해야겠다.
