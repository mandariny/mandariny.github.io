---
layout: single
title: "[JAVA] 자바 프로그램 설계 구조"
---

**key word** : DTO, VO, MVC, Model, View, Controller

## 프로그램 개발시 권장되는 정형화된 구조(= Pattern)

1. Data Transfer Object (DTO) Pattern
   - 여러 클래스간에 주고 받는 데이터용 객체
   - Value Object(VO) Pattern, java bean 이라고 부르기도 함
2. MVC Pattern
   - MVC 패턴이 더욱 강화된 것이 framework
   - 구성 요소
     - Model
       - 핵심 로직
       - business logic(=biz), core logic
     - View
       - 화면 담당 기능
       - 클라이언트에게 보여지는 부분
     - Controller
       - 요청을 받고 요청별로 해당하는 실제 비즈니스 로직을 실행, 결과를 반환 받아 출력할 view에 전달
       - 중간에서 전달 및 조절하는 역할

## 프로그램 개발시 고려해야 할 사항

1. 최대한 각각의 기능을 세분화하고, 명확히하기
   - 협업 및 유지보수에 유리
2. 기능 및 역할에 따라 package, directory 등으로 구분해서 관리하기
3. 인자와 반환값 등이 전체 흐름/로직과 맞는지 체크하기
4. 객체 생성 여부
   - 기능(메소드)만을 위한 클래스의 경우 static으로 선언하면 불필요한 리소스 낭비를 줄일 수 있음
5. 값의 유효성 검사
   - 데이터 타입이 맞더라도 논리적으로 사용할 수 있는 값이 맞는지 확인
   - 값의 유효성을 판별하는 위치에 대해서도 고민할 것
     <br>
     ex) 객체를 생성하는 클래스에서 거를 것인지, 객체 내 메소드에서 거를 것인지 등
   - 예외 처리 필수
