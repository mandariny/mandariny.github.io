---
layout: single
title: "[JAVA] 자바 프로그램 설계 실습"
---

**key word** : 실습, DTO, MVC, 설계

## 실습 / 설계해보기

고객 한 명의 데이터를 요청, 화면에 출력하기

1. 구현할 클래스
   1. Customer
      - 고객 데이터 표현용 클래스 (DTO)
      - 가장 먼저 구현하는 부분
   2. Controller
      - 요청을 받으면 핵심 로직을 실행, 결과를 반환 받아 화면처리 로직에 전달 및 실행
   3. StarView
      - 시작화면, 가장 먼저 실행되는 부분 (main()보유)
      - 클라이언트가 요청한 경우를 가정
      - Controller에게 고객 정보를 요청
   4. EndView
      - 결과값을 출력하는 부분
   5. Model
      - 고객 데이터를 Controller에게 반환하는 핵심 로직
      - DB로부터 고객 정보를 검색할 수 있음을 가정
      - 두 번째로 구현되는 부분
      - 고려사항
        - 데이터 제공을 위해 DTO 생성하는 부분 -> Customer 객체 생성 필수
        - Controller는 Model의 getCustomer()메소드만 호출 -> 객체 생성될 필요 없이 static으로 선언하는 것이 유리
        - 객체 생성시 발생하는 값의 유효성 검사 위치 고민
2. 개발 로직
   Client(가정) -> StartView -> Controller -> Model(DTO 생성/DB와의 통신 가정) -> Controller -> EndView -> Client(출력)
3. 개발 순서
   - Customer(데이터 객체) -> Model(핵심 로직) -> 그 외
