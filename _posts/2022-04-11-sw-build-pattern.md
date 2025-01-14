---
layout: single
title: "[SW / Design Pattern] Build Pattern"
---

**key word** : design pattern, build pattern, 생성 패턴

<br><br>

프로젝트를 진행하면서 프론트 단에 넘길 데이터를 DTO에 담아 보냈는데, 필요한 데이터만 넘기기 위해 생성자를 새로 만들다보니 코드도 지저분해지고, 같은 타입으로 이루어진 생성자의 경우 구분이 안된다는 단점도 있었다. 기본 생성자로 생성하고 setter로 지정해주거나, 안쓰는 값에 null을 넣어 전달하는 방법도 있긴 하지만 lombok의 @Builder를 이용하면 더 깔끔하게 객체를 생성할 수 있다고해서 Builder pattern에 대해 알아보고 프로젝트에 적용해보려고 한다.

<br><br>

## 객체를 생성하는 방법

객체를 만들 때 생성자(Constructor)를 이용하고, 파라미터를 받지 않는 기본 생성자와 사용자가 필요한 값만을 초기화하여 객체를 생성하는 사용자 정의 생성자를 정의해 사용한다. 필드 값이 2개 이하인 경우나, 필드 값에 변경이 없는 상황에서는 필요한 생성자를 직접 만들어 사용하는 것이 가능하다. 하지만 필드 값이 많고, 항상 모든 필드 값을 사용하지 않는다면 어떻게 해야할까? 혹은 필드가 계속해서 추가되는 경우엔 어떻게 해야할까?

1. 기본 생성자를 이용해 객체를 생성한 뒤 Setter로 값을 바꾼다.
2. 사용하지 않는 필드 값에는 null을 넣어준다.
3. 각 상황에 맞는 생성자를 여러개 오버로딩하여 사용한다.

물론 규모가 작고 프로그램을 확장하거나 수정할 가능성이 적은 경우에는 위와 같이 사용해도 특별한 문제는 없다. 하지만 2번 상황의 경우 코드를 작성할 때 가독성이 매우 떨어지게 되고 필드 값이 하나라도 늘어나게 되면 객체를 생성한 모든 지점의 코드를 바꿔야 하는 불상사가 생긴다. 3번 상황의 경우에는 필드 변수의 타입이 겹치게 되면 잘못 오버로딩이 될 가능성이 높다. 그 예로 다음과 같은 필드변수를 가진 클래스가 있다고 가정하자.

```
class Person(){
    String name;
    String nickName;
    int age;
    int weight;
    int height;
}
```

이름, 나이, 키를 초기화하는 생성자를 만들려고 한다면 `Person(String name, int age, int height){}`와같은 코드를 작성하게 될 것이다. 여기에서 이름과 몸무게, 키를 초기화하는 생성자를 만든다면 `Person(String name, int weight, int height){}`와 같은 코드를 작성하게 된다. 컴파일러가 보기엔 `Person(String, int, int)`인 생성자이므로 이 둘을 구분해 사용할 수 없다.

Setter를 이용하는 방식이 Builder를 사용하지 않는 경우 최선인 것 같다. 하지만 이또한 한 번 생성된 객체가 변경될 수도 있기 때문에 가급적 Setter를 이용하기보다는 애초에 원하는 값으로 초기화할 수 있는 Builder를 사용하는 편이 좋다고 한다.

<br><br>

## Builder

Builder Pattern은 쉽게 말하면 필드에 값을 세팅하고 자기 자신의 객체를 반환하는 함수를 이용해 더 가독성이 좋고, 유연하게 생성할 수 있게 해주는 Builder클래스를 만들어 사용하는 디자인 패턴이다. 자세한 예제는 참고한 [블로그](https://jdm.kr/blog/217)에서 볼 수 있다. 물론 우리가 일일이 만들지 않아도 lombok의 @Builder를 이용해 쉽게 사용할 수 있기때문에 난 lombok의 @Builder를 사용하는 방식에 대해서만 간단하게 알아보고 넘어가려고 한다.

1. Builder 패턴을 적용할 클래스에 @Builder를 명시한다.
2. .builder()를 이용해 builder 객체를 만든다.
3. 원하는 값을 필드명과 함께 초기화한다.
4. .build()를 통해 builder객체에서 해당 클래스 객체로 변환한다.

위에서 든 예시로 작성해본다면 다음과 같이 사용할 수 있다.

```
Person me = Person.builder()
            .name("Me")
            .nickName("mandariny")
            .age(999)
            .build();
```

<br><br>

## 결론

Builder Pattern을 이용하면 객체의 불변성을 확보할 수 있고, 객체 생성의 가독성과 유연성을 높일 수 있다. 물론 필드가 충분히 적은 경우나, 변경이 없는 경우에는 오히려 불필요한 작업이될 수 있지만 유지보수 및 확장을 생각하는 프로그램이라면 Builder Pattern을 적용하는 것이 좋을 것 같다.

<br><br>

## 참고

https://ko.wikipedia.org/wiki/%EB%B9%8C%EB%8D%94_%ED%8C%A8%ED%84%B4 <br>
https://mangkyu.tistory.com/163 <br>
https://jdm.kr/blog/217
