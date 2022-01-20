---
layout: single
title: "[JAVA] List, Set, Map"
---

**key word** : List, Set, Map, 순환, 반복

<br><br>

## List

1. 특징
   - 저장되는 데이터의 순서를 유지함
   - (Object) 배열과 흡사한 구조이지만
     <br>1) 배열은 고정 사이즈인 반면 List는 가변적인 메모리가 적용고, 2) class로 기능이 제공된다는 점에서 차이가 있음.
   - index로 원소 관리
   - 동일한 내용을 갖는 객체의 **중복 저장**을 허용
   - 객체 타입만 저장 가능
     - 기본 타입의 변수들은 대응하는 객체(Wrapper Class)를 사용
       <br>
       ex) int -> Integer, double -> Double
     - list에 넣을 때 기본 타입을 사용할 경우 컴파일시 객체를 이용하는 문장으로 자동 변환 됨
       <br>
       ex) list.add(3); -> list.add(Integer(3));
2. API
   - ArrayList
     - new ArrayList()로 10개의 메모리 공간을 보유한 객체를 생성할 수 있음
     - 인자로 초기 메모리 사이즈 및 추가로 증가되는 메모리의 사이즈를 설정할 수 있음
     - [공식문서](https://docs.oracle.com/javase/8/docs/api/)를 참고하면 Object 객체를 매개변수나 리턴타입에서 사용하는 것을 알 수 있으므로 <객체타입>를 이용해 타입을 명시적으로 선언해주거나(Generic) or 형변환을 해서 사용할 수 있음
   - 원소 삭제 시 인덱스에 맞게 원소들을 재정렬하므로 배열에 비해 속도가 느림
     <br>
     -> 배열로 관리할 수 없는 다수의 데이터를 실시간으로 저장/삭제할 경우나, 삭제하는 데이터가 리스트의 끝쪽에 분포하는 경우에 사용하는 것이 좋음.

## Set

1. 특징
   - 저장되는 데이터의 순서를 유지하는 것이 불가능함
   - 동일한 내용을 갖는 객체의 **중복 저장이 불가능함**
   - 데이터를 하나씩 구분할 수 있는 고유한 index가 없어서 인덱싱이나 하나씩 값을 반환받을 수가 없음
   - [Iterator](https://docs.oracle.com/javase/8/docs/api/) API를 활용해 정보를 얻을 수 있음

## Map

1. 특징

- 저장되는 데이터의 순서를 유지하는 것이 불가능함
- key와 value의 쌍으로 저장이 됨
- indexing이 따로 안되므로 데이터를 모두 반환받고 싶을 경우에는 keySet()과 Iterator를 사용<a href="https://docs.oracle.com/javase/8/docs/api/#method.summary">이동</a>
