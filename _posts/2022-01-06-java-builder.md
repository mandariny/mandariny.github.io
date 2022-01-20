---
layout: single
title: "[JAVA] Builder 사용법"
---

**key word** : Builder, lombok, build

<br><br>

Builder는 lombok이라는 외부 라이브러리를 이용하면 사용할 수 있다.
객체를 생성할 때 생성자를 사용하지 않아도 멤버변수를 초기화할 수 있어서 가끔 필요한 상황이 있을 수 있을 듯 하다. 코드 유연성, 확장성을 위해 사용한다.

## Builder

[공식 문서](https://projectlombok.org/features/Builder)를 보면 @Builder는 클래스나 생성자, 메소드에 모두 사용할 수 있다. <br>

1. 구조

   @Builder를 사용하게 되면 builder라고 불리는 내부 static class인 FooBuilder를 생성하는데 대략 아래와 같은 구조인 것 같다.

   ```
       static FooBuilder(same type arg~~){
           private params (of target)
           ...

               private FooBuilder(){
                   Constructor
               }

               Builder setParams(){
                   setter와 같은 역할, 타겟의 모든 멤버변수에 대해 가지고 있음
               }

               public String toString(){

               }
           }
   ```

   @Builder는 위와같이 생성자나 setter, toString같은 역할을 하는 메소드를 가지고 있으며 이를 이용해 객체를 생성할 수 있다.
   <br>
   마지막으로 @Builder가 달린 타겟 클래스에는 builder를 생성할 수 있는 builder() 메소드가 생긴다.

2. 기능(클래스에 @Builder를 사용할 때)

   - 객체를 생성할 때 멤버변수를 초기화하는 코드를 자동으로 생성해줌
   - 일부 변수만 초기화할 때 사용 권장
   - 콜렉션 타입의 변수를 초기화 할 때도 전체 원소 리스트가 아닌 개별적인 원소로 추가 가능
   - setter와 같은 역할을 하는 메소드들은 Builder 객체를 반환하기 때문에 연속적으로 사용할 수 있음

3. 사용 방법
   - 클래스에 새롭게 생성된 builder()메소드를 사용한다.
   - builder() 내의 메소드를 이용해 원하는 기능을 사용한다.
   - build()를 통해 새로운 객체를 반환받는다.
     <br>
     ex) `Person.builder().name("아무개").build();`

<br>
<br>
사용자 정의 생성자를 사용할 경우엔 클래스가 아닌 생성자에 @Builder를 사용해야 한다던가 하는 몇 가지 주의 사항이나 기능들이 더 있지만 필요할 때 찾아보면 될 것 같다.
<br>
생성자에 파라미터로 줄 수 있는 조합의 경우의 수가 많을 경우에 유용하게 사용할 수 있을 것같다.
