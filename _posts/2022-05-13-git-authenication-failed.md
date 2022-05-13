---
layout: single
title: "[Git] Authentication failed"
---

**key word** : git, Authentication failed, 인증

AWS EC2에 centos로 서버를 구성하고 로컬에서만 돌리던 웹페이지를 배포하려다 만난 에러다. 깃에 소스를 올려둬서 깃 클론으로 받으면 쉬울 것 같았는데 예상치못한 Authentication failed...

https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/

친절하게도 토큰 인증에 대해 안내하는 페이지를 알려준다. 작년 8월부터 시작했다고하는데 들었던 기억이 난다. 한동안 git을 다른 환경에서 사용할 일이 없어서 까먹고 있었지만ㅋㅋㅋ

간단히 말하자면 깃에 접근하거나 깃헙 리포지토리에 접근하기 위해서 기존에 사용하던 비밀번호 대신 인증 토큰을 이용하면 된다는 내용이다.

토근을 발급받는 방법도 자세히 안내해준다. 아래는 [링크](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) 내용을 요약한 것이다.

1. 프로필 내 Settings로 들어간다.
2. 좌측 하단의 <> Developer settings로 들어간다.
3. 좌측 하단의 Personal access tokens로 들어간다.
4. Generate new token으로 들어가 이름, 유효 기간, 허용 범위 등을 체크하고 토큰을 발급 받는다.
5. 발급받은 토큰을 password에 입력하고 로그인을 한다.
