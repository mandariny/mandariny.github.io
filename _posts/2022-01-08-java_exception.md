---
layout: single
title: "[JAVA] 자바 예외처리"
---

**key word** : exception, 예외처리, try, catch, finally, throws

프로그램을 개발할 때에는 경미한 이슈가 일어나더라도 다른 기능들이 정상적으로 작동하게끔 만들어야 한다.
혹시나 일어날 수 있는 예외 상황에 대해 처리하는 로직을 따로 작성하는 것이 **예외 처리**이다.

## 예외(Exception)와 예외처리

1. 예외처리의 필요성
   <br>
   이슈가 생기더라도 프로그램 실행이 중단돼서는 안되는 경우에 다른 로직은 정상적으로 돌아갈 수 있도록 하기 위해 예외처리를 한다. <br>
   문제가 생긴 부분에 대해 유연하게 처리하기 위해 처리 가능한 경미한 에러는 사전에 예외처리 해둔다.

2. 예외 종류

   - 컴파일 예외
     <br>
     예외 처리 문장이 필수적이며, 처리하지 않으면 컴파일 자체가 불가능한 예외이다.
     <br>
     ex) ClassNotFoundException
     <br>
     에러도 예외도 컴파일시에 문제가 생기는게 낫다.. 예외가 생길 수 있는 부분을 찾아서 처리해주면 정상적으로 컴파일 가능
   - 실행 예외
     <br>
     컴파일은 잘 되지만 실행중에 문제가 생길 수 있는 예외이다.
     java.lang.RuntimeException을 상속한 Exception들이 여기에 해당된다.
     <br>
     이를 해결하기 위해서는 예외가 발생하지 않도록 값을 수정해주거나, try ~ catch문을 사용해 예외처리를 한다.
     <br>
     ex) ArrayIndexOutOfBoundsException

3. 예외 처리 문법
   - try ~ catch문
     ```
     try{
             // 예외가 발생할 수 있는 로직을 작성하는 부분
             // 실제로 프로그램에 필요한 기능 부분을 이 부분에 쓰면 된다.
         }catch (예외타입 변수명) {
             // 예외가 발행한 경우에 예외를 처리하는 블록
         }finally{
             // 예외 발생 여부와는 무관하게 실행이 보장되는 블록
             // 시스템 자원 반환 등에 주로 쓰인다고 한다.
         }
     ```
   - throws
     호출한 곳에서 예외를 처리할 수 있도록 [Exception 객체](https://docs.oracle.com/javase/8/docs/api/)를 만들어 던지는(throw) 방법이다.
     <br>
     호출한 곳에서 try ~ catch를 이용해 예외 처리를 해줘야 한다.
     여러 곳에서 생길 수 있는 예외를 한 곳에서 처리하면 나중에 뭘 위한 예외인지 알아보기가 어려워지니 호출한 곳으로 처리를 미루는 것이다.
     ```
     리턴타입 메소드명 () throws Exception{
         //예외로 처리해야 하는 상황이 생기는 경우
         // Exception 객체 생성
         throw new Exception();
     }
     ```
   - 사용자 정의 Exception 클래스 사용
     사용자가 직접 Exception 클래스를 만들어 사용하는 것이다. Spring framdwork에서도 다수로 제공하고 있다. Exception이나 Exception의 서브 클래스를 상속받아 만들면 된다.
     ```
     public class 예외객체명 extends Exception{
        // 생성자 추가
     }
     ```
