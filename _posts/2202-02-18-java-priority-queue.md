---
layout: single
title: "[JAVA] 우선순위 큐"
---

**key word** : Queue, Priority Queue, 우선순위 큐

<br><br>

## Priority Queue

---

큐라는 자료구조는 FIFO(First In First Out) 방식으로 자료를 저장한다. 먼저 저장된 데이터가 먼저 나가는 구조인데, 이때 무조건 먼저 들어온 순서대로 내보내는 것이 아니라, 우선순위가 높은 원소를 먼저 내보낼 수도 있다. 그게 바로 우선순위 큐(Priority Queue)이다. 우선순위 큐는 우선순위에 따라 들어오는 순서와 다르게 나갈 수 있기 때문에 일반적으로 힙을 이용해 구현하기때문에 O(nlogn)의 시간복잡도를 갖는다.

<br><br>

## 자바 PriorityQueu 클래스

---

util 패키지 내에 PriorityQueue 클래스가 존재하며 비교 가능한
