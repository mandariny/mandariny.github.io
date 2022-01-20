---
layout: single
title: "[JAVA] 자바 입출력 API"
---

**key word** :

<br><br>

자바를 배울 떄 제일 먼저 배우는 Scanner나 System.out부터 알고리즘 공부를 하면서 알게 된 BufferedReader 등 자바에는 여러 입출력 API들이 존재한다. 하지만 오히려 너무 익숙해져서인지 쓰려고하면 자동으로 손이 타이핑을 할 뿐 정작 어떤 클래스들인지는 잘 몰랐다. 이참에 한 번 정리하면서 몰랐던 부분들을 공부해보려고 한다.

<br><br>

## 표준 입출력 클래스

---

<br>

### **System.in**

1. 기능
   - 값을 입력받을 때 쓰는 클래스이다.
   - 출력할때와 달리 값을 입력받을 때에는 어떤 값이 들어올 지 모르므로 예외처리를 필수적으로 해줘야 한다. (IOException)
   - System이라는 클래스 내에 InputStream타입의 in 멤버변수가 존재한다. 따라서 `System.in.read()`와 같이 InputStream의 메소드를 사용할 수 있다.
2. 주요 메소드

   - read()
     - input stream으로부터 바이트단위로 읽어올 수 있는 메소드.
     - byte 배열과 int 타입의 길이 정보 인자로 넘겨줄 수 있고, 받아온 데이터를 배열에 저장할 수 있다.
       <br>-> 한글 철자를 저장하기 위해서는 16bit(2byte)를 사용해야하므로 read()로는 읽어들일 수 없다.

3. System.out
