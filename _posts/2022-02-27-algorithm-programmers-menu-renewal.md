---
layout: single
title: "[Algorithm / Java] 프로그래머스 신규 아이디 추천"
---

**key word** : 조합, 해시맵
<br><br>

## [문제](https://programmers.co.kr/learn/courses/30/lessons/72411)

---

여러 문자열과 조합의 개수가 주어지면, 가장 많이 나온 문자 조합을 리턴하는 문제이다. 지금까지 공부한 알고리즘이나 자료구조를 활용하면 그렇게 어렵지 않게 풀 수 있는 것 같다.

<br><br>

## 아이디어

---

가능한 메뉴 조합을 구하고 해시맵을 이용하여 가장 많이 나온 조합을 골랐다. 조합을 구할 때에는 스택을 사용했다.

<br><br>

## 구현

---

```
import java.util.HashMap;
import java.util.Stack;
import java.util.ArrayList;
import java.util.Arrays;

class Solution {
    public String[] solution(String[] orders, int[] course) {
        ArrayList<HashMap<String, Integer>> arr = new ArrayList<>();
        ArrayList<String> answers = new ArrayList<>();

        for(int c : course){
            HashMap<String, Integer> map = new HashMap<>();
            for(String s : orders){
                char[] chars = s.toCharArray();
                Arrays.sort(chars);
                dfs(0, 0, String.valueOf(chars), c, new Stack<String>(), map);
            }
            arr.add(map);
        }

        for(HashMap<String, Integer> map : arr){
            maxCource(map, answers);
        }

        String[] answer = new String[answers.size()];
        answers.toArray(answer);
        Arrays.sort(answer);

        return answer;
    }

    public void dfs(int k, int at, String order, int course, Stack<String> newCource, HashMap<String, Integer>map){
        if(k == course){
            makeHash(newCource, map);
            return;
        }

        int len = order.length();
        for(int i=at; i<len; i++){
            newCource.push(String.valueOf(order.charAt(i)));
            dfs(k + 1, i + 1, order, course, newCource, map);
            newCource.pop();
        }
    }

    public void makeHash(Stack<String> newCource, HashMap<String, Integer>map){
        String str = "";
        for(String s : newCource){
            str += s;
        }

        if(!map.containsKey(str)){
            map.put(str, 1);
        }else{
            map.put(str, map.get(str) + 1);
        }
    }

    public void maxCource(HashMap<String, Integer> map, ArrayList<String> answers){
        int max = getMaxValue(map);

        for(String s : map.keySet()){
            if(map.get(s) == max && max != 1){
                answers.add(s);
            }
        }
    }

    public int getMaxValue(HashMap<String, Integer> map){
        int max = 0;
        for(Integer i : map.values()){
            max = max < i ? i : max;
        }
        return max;
    }
}
```

<br><br>

## 후기

---

구현 문제를 자주 풀지 않았어서 괜히 긴장하며 풀이를 시작했다. 하지만 좀 보다보니 그리 어려운 문제는 아닌 것 같았다. 다만 일단 정답을 맞추자는 생각에 좀 무식하게 푼 면이 있다. 해시맵의 경우에도 리스트로 관리하지 않고 바로 처리해도 됐을 것 같은데, 이런 식으로 좀 불필요하게 사용된 자료구조들이 있는 것 같다. 다시 풀 때엔 좀 더 정리된 코드로 문제를 해결해봐야겠다.
