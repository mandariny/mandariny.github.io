---
layout: single
title: "[JAVA] 자바 API 및 외부 라이브러리 사용"
---

**key word** : API, java.lang, 외부 라이브러리, Maven, m2, pom, dependency, lombok, log4j, junit, log, test

<br><br>

자바에서는 사용이 편리한 API를 제공해주고 있다. 그리고 다른 외부 라이브러리들도 잘 돼 있는게 많아서 사용하면 생산성을 향상시키기 좋아보인다. 자바 API와 외부 라이브러리를 사용하는 방법을 알아보려고 한다.

## API(Application Programming Interface)

1. API?
   - 이미 구현돼 사용 가능하게 제공해주는 코드들
   - 자바에서 직접 제공해주는 API도 존재 -> [자바 API 공식 문서](https://docs.oracle.com/javase/8/docs/api/)로 확인 가능
2. API 활용
   - import문을 이용해 외부 패키지 사용
   - 객체 생성 후에 호출하며, static 변수와 static 메소드는 객체 생성 없이도 호출 가능
     <br>
     ex)Math
   - java.lang package만 유일하게 import 생략 가능

## Maven

1. Maven(메이븐)이란?
   - 인터넷이 연결된 상태에서 외부 저장소에서 제공해주는 library들을 로컬 시스템으로 다움로드 받을 수 있는 툴
   - eclipse에 m2로 내장돼있음
   - 라이브러리들은 [maven 홈페이지](https://mvnrepository.com/)에서 확인 가능
2. 효용성
   - 라이브러리들 간의 의존 관계 확인 가능
   - 라이브러리를 자동으로 설치 할 수 있음
3. 사용 방법
   1. 새로운 프로젝트 생성
   2. 프로젝트 우클릭 -> Configure -> Convert to Maven Project
   3. pom.xml 파일에 dependency 추가
      - Global repositories 다운 후 검색하여 추가
        - Window - showView - other - maven - maven repository 창 열고 확인 가능
      - [웹](https://mvnrepository.com/)에서 검색 후 수동 추가
        - <dependencies> 태그를 추가한 후 라이브러리별 <dependency> 태그 삽입

## 많이 사용하는 Library

1. lombok

   - 특징
     - 코드량 감소를 위한 라이브러리, 특히 데이터 저장을 위한 클래스들에 주로 사용
     - 일일이 타이핑하지 않아도 getter/setter/생성자 등 필요한 메소드들을 생성해줌
     - 멤버 변수 추가, 삭제, 수정 후에도 따로 메소드를 수정해줄 필요가 없음
     - 개발 시간 단축, 유지보수 용이, 비용 절감(기업 관점) 등의 장점이 있음
   - 설치 방법
     1. lombok.jar [다운로드](https://projectlombok.org/all-versions) 후 설치
        - eclipse.exe 실행 파일의 위치 정보 필요
        - 명령어를 이용할 경우 `java -jar lombok.jar`
     2. eclipse.exe와 같은 폴더 내에 lombok.jar이 생성되었는지 확인
   - 설치시 발생한 오류
     - 설치 이후 기존 프로젝트의 클래스들이 제대로 표시되지 않고 <mark>Unable to make protected final java.lang.Class ~ </mark>과 같은 오류가 발생
     - java lang 클래스를 잡지 못하는 것 같아 새 프로젝트를 만들거나 이클립스를 껐다 켜도 해결되지 않음
     - 찾아보니 eclipse.ini 파일만 수정해주면 간단하게 해결이 되길래 [블로그](https://shanepark.tistory.com/205)를 참조해 해결함
     - 주요 기능
       - @(에노테이션)을 이용해 추가하고자 하는 기능을 표시
         <br>
         ex) @Getter, @Setter
       - 에노테이션을 사용해도 사용자 정의로 커스텀 가능

2. log4j (log for java)
   - end user들의 서비스 사용(로그)을 쉽게 기록할 수 있는 라이브러리
   - 유저들의 액션에 대한 추척 가능
3. junit
   - 특징
     - 개발하는 기능을 실시간으로 확인하기 위한 test용 framework
     - main 메소드가 불필요해짐
       - 서버 없이 실행시켜야하는 자바 소스에 대해 test용으로 주로 활용
       - junit을 활용함으로써 test 용도로의 활용성이 낮아짐
   - 사용시 발생한 오류
     - <mark>the import org.junit.Test conflicts with a type defined in the same file</mark> 오류
       - Test라는 클래스명이 겹쳐서 생긴 오류. 클래스명만 바꿔주면 해결 된다.
     - static메소드나 parameter를 쓰면 동작하지 않음
     - junit이 import되지 않는 경우
       - eclipse가 기본으로 잡는 junit 버전과 설치한 버전이 일치하지 않을 경우 사용이 안 됨
       - 프로젝트 우클릭 -> Build Path -> Configure Build Paht -> Add Library에서 수동으로 버전을 바꿔줘 해결

<br>
직접 타이핑해야한다는 강박이 약간 있었는데 이미 유용한 툴들이 많이 있으니 최대한 활용하는 것이 중요하다는 생각이 든다.

그만큼 생산성을 높이고 코드 한 줄 더 칠 시간에 프로그램 구조와 설계에 대해 더 생각해보면 좋을듯.

그 외 여러 개발 편의를 높여주는 라이브러리 이것저것 찾아서 써봐야지.
