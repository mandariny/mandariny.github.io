---
layout: single
title: "[Algorithm / Java] 프로그래머스 신규 아이디 추천"
---

**key word** : 자바 정규 표현식, regex
<br><br>

## [문제](https://programmers.co.kr/learn/courses/30/lessons/72410)

---

2021년 카카오 코딩테스트 문제가 구현력을 키우는데 좋다고 해서 풀어봤다. 규칙에 맞게 문자열을 편집하면 되는 문제로 난이도 자체는 어렵지 않았다. 하지만 정규 표현식을 사용해야해서 검색이 많이 필요했다. 그동안 미뤄왔던 공부를 한다고 생각하며 문제를 풀었다.

<br><br>

## 아이디어

---

toLowerCase, replaceAll, replace, substring 등 String의 주요 메소드들을 사용해서 풀 수 있을 것 같았다. 또 유효 문자를 검사하는 데에는 정규 표현식을 사용할 수 있을 것 같아서 공부해 바로 적용해봤다.

<br><br>

## 구현

---

```
class Solution {
    public String solution(String new_id) {
        new_id = new_id.toLowerCase();
        new_id = new_id.replaceAll("[^-_.[a-z][0-9]]", "");

        while(true){
            if(new_id.contains("..")){
                new_id = new_id.replace("..",".");
            }else{
                break;
            }
        }

        if(new_id.startsWith(".", 0)){
            new_id = new_id.substring(1);
        }

        if(new_id.length() > 15){
            new_id = new_id.substring(0, 15);
        }

        if(new_id.equals("")){
            new_id = "a";
        }

        if(new_id.charAt(new_id.length() - 1) == '.'){
            new_id = new_id.substring(0, new_id.length() - 1);
        }

        if(new_id.length() <= 2){
            String s = String.valueOf(new_id.charAt(new_id.length() - 1));
            new_id = new_id.concat(s).concat(s);
            new_id = new_id.substring(0, 3);
        }
        return new_id;
    }
}
```

<br><br>

## 2차 구현

---

```
class Solution {
    public String solution(String new_id) {
        new_id = new_id.toLowerCase();
        new_id = new_id.replaceAll("[^a-z0-9-_.]", "");
        new_id = new_id.replaceAll("[.]{2,}", ".");
        new_id = new_id.replaceAll("^[.]|[.]$", "");
        if(new_id.equals("")) new_id = "a";
        if(new_id.length() > 15) new_id = new_id.substring(0, 15);
        new_id = new_id.replaceAll("^[.]|[.]$", "");
        while(new_id.length() < 3){
            char c = new_id.charAt(new_id.length() - 1);
            new_id += c;
        }

        return new_id;
    }
}
```

정규표현식을 더 공부하고 다시 풀어봤다. 확실히 코드가 더 깔끔했졌다.

<br><br>

## 후기

---

정규 표현식을 공부하고 막 적용한 상태라 코드가 지저분한 부분이 많다. 다른 분들의 풀이를 보니까 마침표 2개를 검사하는 표현식, 맨 앞 자리와 맨 뒷 자리의 마침표를 검사하는 표현식 등도 작성할 수 있는 것이었다.

마침표 두 개를 검사하는 표현식을 작성할 줄 몰라서 알게 된 것이기도 한데, String의 메소드 중 replace는 바꿀 문자로 char 타입을 인자로 받지만, replaceAll은 표현식을 인자로 받았다. 모르고 `replaceAll("..", ".")`라고 썼다가 문자열이 모두 마침표로 바뀌어서 당황했다.

미뤄왔던 정규 표현식 공부를 시작했다는 것에 의의를 두고 싶고, 종종 사용하면서 익숙해져야겠다. 다음에 다시 풀 때에는 따로 검색하지 않아도 정규 표현식을 자유자재로 사용할 수 있게끔 공부해야겠다. 또, 검사하는 부분을 각각 메소드로 만들어 사용하는 분들이 많았다. 나도 재사용성까지 고려하여 문제를 푸는 습관을 들여야겠다.
