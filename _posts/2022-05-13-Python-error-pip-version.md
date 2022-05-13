---
layout: single
title: "[Python / Error] pip version error"
---

**key word** : pip

AWS EC2에 centos를 깔았더니 python3.6이 깔려있었다. 삭제하고 python3.8을 새로 깔고 alternatives를 이용해 버전도 바꿔줬다.

하지만 문제는 언제나 pipㅠ

기껏 python3.8로 바꿔놨는데 pip는 `-bash: /usr/local/bin/pip3: /usr/bin/python3.6: bad interpreter: No such file or directory` 이렇게만 뜬다..

1. pip 새로 설치하기
   <br>
   [블로그](https://40holic.tistory.com/71)를 참고한 방법.
   wget을 이용해 새로 받을 수도 있다고하는데,, 문제는 wget을 설치할 수 없다는 것이었다. 메모리를 할당할 수 없어서 다운로드를 할 수 없단다,,

2. `python -m pip install 패키지명 ` 이용
   <br>
   [StackOverflow](https://stackoverflow.com/questions/2812520/dealing-with-multiple-python-versions-and-pip)를 참고한 방법.
   다행히 이 방법이 통했다. 패키지 설치 성공!

임시방편인 것 같아서 찝찝함이 없지 않지만 일단 이렇게라도 사용해야겠다.
