---
layout: single
title: "[Algorithm / Java] N으로 표현"
---

**key word** : DP, Dynamic Programming, 동적계획법
<br><br>

## [문제](https://programmers.co.kr/learn/courses/30/lessons/42895)

처음 봤을 때 생각할 수 있는 경우의 수가 너무 많아 어떻게 접근해야 할지부터 막막했던 문제였다. 질문하기 탭에서 문제의 접근법에 대해 친절히 써주신 분이 계셔 참고해 구현했다. [해당 링크](https://programmers.co.kr/questions/25218)를 첨부한다.

<br><br>

## 아이디어

지금까지 내가 풀어봤던 dp 문제는 주로 최소 혹은 최대가 되는 경우의 수를 저장하고 그걸 가지고 또 이후의 경우의 수를 계산하는 문제들이었다. 그래서 자연히 number 길이의 배열을 선언하고 경우의 수를 계산해나가는 방식으로 접근하려 했다.

하지만 생각할 수 있는 경우의 수가 너무 많았고, 이전 숫자들로부터 새로운 숫자를 만들 수 있는 경우의 수를 계산하기에는 그 사이에 특정한 규칙이 없었다. 그래서 질문하기 탭에서 힌트를 얻을 수 없을까 했는데 굉장히 친절히 문제의 해설을 적어준 분이 계셨다.

요약하자면 N이라는 숫자를 몇 번 사용했는지를 dp에 기록하는 방식으로 문제에 접근하며, 8번 이상인 경우엔 어차피 -1이므로 그 이상 계산할 필요는 없다. N을 1번 사용하는 경우는 N 하나뿐이고, 2개를 사용하는 경우는 NN을 포함해 N을 자기 자신과 사칙연산하는 4개의 경우가 더 있다. 3개 이상부터는 경우의 수가 급격히 많아지는데 이는 자세히 살펴보면 N을 1개 사용했을 때와 2개 사용했을 때 나왔던 모든 경우의 수에 대해 서로 사칙연산해 구할 수 있다. N을 8번 사용한 경우는 1번 사용한 경우와 7번 사용한 경우를 사칙연산한 결과, 2번 사용한 경우와 6번 사용한 경우를 사칙연산한 결과 3번 사용한 경우와 5번 사용한 경우, 이런 식으로 나누어 구할 수 있다.

이를 구현하기 위해 중복된 값을 제외하고 저장할 수 있는 HashSet을 사용했으며, 0의 경우 더하기나 곱하기 빼기에는 영향이 없고 나누는 경우에는 예외를 발생할 수 있어 저장할 때 제외했다.

<br><br>

## 구현

```
import java.util.HashSet;

public class NExpression {
    public static void main(String[] args) {
        System.out.println(solution(5, 12));
    }

    public static int solution(int N, int number) {

        HashSet<Integer>[] dp = new HashSet[8];

        int n = 0;
        for (int i = 0; i < 8; i++) {
            n += Math.pow(10, i) * N;
            dp[i] = new HashSet<Integer>();
            dp[i].add(n);
        }

        dp[1].add(N + N);
        dp[1].add(N * N);
        dp[1].add(N / N);

        for (int i = 2; i < 8; i++) {
            for (int j = 0; j < i; j++) {
                for (int a : dp[j]) {
                    for (int b : dp[i - j - 1]) {
                        dp[i].add(a + b);
                        dp[i].add(a * b);
                        if (a - b > 0)
                            dp[i].add(a - b);
                        if (a / b > 0)
                            dp[i].add(a / b);
                    }
                }
            }
        }

        for (int i = 0; i < 8; i++) {
            if (dp[i].contains(number))
                return i + 1;
        }

        return -1;
    }
}

```

<br><br>

## 후기

지금까지의 경험에 기대어 사용 횟수로 dp 배열을 구성할 생각을 하지 못했던 게 가장 큰 실수인 것 같다. 새로운 접근 방식을 배웠으니 다른 문제를 풀 때에 적용해 볼 수 있으면 좋겠다. 또 다른 분이 구현한 것을 보니 구분은 반복문의 j를 i/2까지만 돌리셨다. a - b와 b - a의 연산 결과가 다를 수도 있어 모두 계산한 것이지만, 사실 더하기나 곱하기는 순서를 바꿔도 결과가 같기 때문에 그냥 -와 /에 대해서만 순서를 바꿔 연산하면 되기 때문이다. 아직은 문제를 풀고 그걸 구현하는데 급급하지만 더 효율적으로 구현하는 것도 늘 고민해 봐야 하는 부분인 것 같다.
