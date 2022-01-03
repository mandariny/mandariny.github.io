---
layout: single
title: "자바 개발 환경"
---

## 프로그램 실행 환경

---

1. C/C++
   - 컴파일 후 링크
   - 각 운영체제에서 실행할 수 있는 실행 파일 생성
2. Java
   - 컴파일로 bytecode 생성
     - `javac` 명령어를 이용해 <mark>\*.java</mark>파일을 bytecode 로 컴파일-> <mark>\*.class</mark>파일로 저장
   - 자바가상머신(JVM)을 통해 바이트코드를 각 운영체제에 맞는 기계어로 변환후 실행
     - `java` 명령어를 이용해 '\*.class' 파일을 실행

<br>
프로그래밍 언어로 컴퓨터에게 명령을 내릴 경우 고급 언어를 기계어로 바꿔주는 컴파일러가 필요하다. 자바는 컴파일러가 바로 기계어로된 실행파일을 만들어주지 않고 일단 바이트코드로 변환한 후 자바가상머신을 이용해 최종적으로 운영체제에 맞는 실행파일을 만들게 된다.
  
-> 운영체제에 종속적이지 않음 (JVM은 종속적, 각 운영체제에 맞는 JVM을 설치해야 함)
<br><br>

## JRE, JDK

---

1. JRE (Java Runtime Environment)
   - JVM(Java Virtual Machine) + API(Application Programming Interface, liabrary) 등 자바를 실행하는 데 필요한 패키지
   - 자바가상머신(JVM) : 운영체제에 적합하게 컴파일된 바이트코드를 실행하는 실 주체의 기능을 함
2. JDK (Java Development Toolkit)
   - 자바용 SDK(Software Development Kit)
   - JRE를 포함하며 컴파일러(javac)와 jdb 등과 같은 도구를 포함
   - 컴파일러를 비롯한 프로그램 개발에 필요한 도구

Java 프로그램을 실행만 하는 것이라면 JRE만 있으면 되지만 하지만 Java를 이용해 프로그래밍을 해야 한다면 JDK가 필요하다.
<br><br>

## 개발환경 구축

---

1. JDK
   - 설치 후 Path에 jdk 하위의 bin 폴더(binary code로 바뀌는 부분 저장) 경로 추가
   - JAVA_HOME이라는 새로운 환경변수 생성 후 jdk 경로 추가 <br>-> jdk 경로가 필요한 경우 사용 가능
2. IDE(Intergrated Development Environment)
   - 프로그램 개발을 위한 통합 개발 환경을 제공
   - 자바는 주로 eclipse를 사용
   - 업데이트가 잦은 경우 최신버전은 지양하는 것이 좋고, 설치 경로와 실행 경로를 구별해 별도로 관리하는 것이 좋음
