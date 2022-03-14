---
layout: single
title: "[Algorithm / Java] 프로그래머스 신규 아이디 추천"
---

**key word** : 동적계획법, Dynamic Programming
<br><br>

## [문제](https://programmers.co.kr/learn/courses/30/lessons/42898)

---

집에서 학교까지 가는 길을 좌표로 나타냈을 때, 학교에 가는 최단 거리의 경수의 수를 구하는 문제이다. 단, 오른쪽과 아래로만 움질일 수 있고, 중간에 지날 수 없는 웅덩이가 있을 수 있으며, 경우의 수를 1,000,000,007로 나눈 나머지를 return해야 한다.

<br><br>

## 아이디어

---

문제 자체는 어렵지 않게 풀 수 있었다. 오른쪽과 아래로만 움질일 수 있기 때문에, 좌표상 윗칸까지의 경우의 수와 왼쪽칸까지의 경우의 수를 더하면 해당 칸까지 올 수 있는 경우의 수를 구할 수 있다. 웅덩이의 경우 0으로 두면 계산에 영향을 미치지 않을 수 있다.

<br><br>

## 구현

---

```
class Solution {
    public int solution(int m, int n, int[][] puddles) {
        int[][] dp = new int[n][m];
        dp[0][0] = 1;

        for(int i=0; i<puddles.length; i++){
            dp[puddles[i][1] - 1][puddles[i][0] - 1] = -1;
        }

        for(int i=0; i<n; i++){
            for(int j=0; j<m; j++){
                if(i == 0 && j == 0) continue;
                if(dp[i][j] == -1){
                    dp[i][j] = 0;
                    continue;
                }
                if(i > 0){
                    dp[i][j] += dp[i - 1][j];
                }

                if(j > 0){
                    dp[i][j] += dp[i][j - 1];
                }

                dp[i][j] %= 1000000007;
            }
        }

        return dp[n - 1][m - 1];
    }
}
```

<br><br>

## 오류

---

1. puddles로 주어진 웅덩이의 좌표 [열, 행] 순으로 데이터가 들어있었다. 데이터의 순서를 간과하고 문제를 풀어 런타임에러(아마도 Array Index Out of Bounds)가 발생했다.

2. 1000000007로 나눈 나머지를 리턴하는 것인데 그 부분 또한 잊고 경우의 수를 리턴했었다. 문제의 입출력을 제대로 확인하는 습관을 들여야겠다.

3. 효율성 검사 문제를 다 틀렸다. 매 배열마다 1000000007로 나누어줌으로써 해결했다. `a % c + b % c = (a + b) % c`라는 성질을 이용했다. 모듈러 연산의 특징 중 하나이다. 이를 이용해 int 범위를 벗어나지 않게 연산할 수 있었다.
