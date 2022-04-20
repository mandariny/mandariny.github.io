---
layout: single
title: "[JAVA] DAO / DBUtil"
---

**key word** : DAO, DBUtil, JDBC, DB연동

<br><br>

## DAO (Data Access Object Pattern)

JDBC로 DB를 연동하게 되니 기존에 DTO 패턴으로 만들어뒀던 객체들을 DB에 CRUD하기 위한 기능들이 필요해졌다. 이 때, DB와 실질적으로 소통하는 기능을 전담하는 클래스를 DAO라고 부른다.

보통 table당 하나의 DAO 클래스를 설계하는 것을 권장한다고 하며, 구조가 복잡할 경우에는 그 이상 추가로 개발한다고 한다.

CRUD 기능을 가진 메소드들로 구성된다.

<br><br>

## DBUtil

여러 table을 사용하는 경우에는 DAO 클래스도 여러개 생성되므로 설정 정보 등이 중복된다. 이러한 중복된 코드를 분리해서 따로 관리하는 클래스가 DBUtil 클래스이다.

<br><br>

## DBUtil의 구성

1. properties
   - DB와 연동할 때 사용해야하는 정보 (url, id, pw) 등은 properties 파일에 따로 저장한 뒤 DBUtil 클래스에서는 파일을 읽어들여 사용하는 것이 좋다. DB 정보가 바뀌더라도 새로 빌드한 후 재배포하지 않아도 되기 때문.
2. getConnection
   - DB와 연결된 Connection 클래스를 반환해주는 메소드.
3. close
   - 작업이 끝난 이후 Connection, Statement, ResultSet 등의 객체를 닫아줘야 한다.
   - 반환해야할 객체의 종류에 따라 Overloading해서 여러 메소드를 만들 수 있다.
     <br>
     -> executeQuery의 경우 ResultSet을 반환하므로 ResultSet도 해제할 수 있는 close(Connection, Statement, ResultSet) 메소드를 사용해야 하고, executeUpdate의 경우 정수만 반환하기 때문에 close(Connection, Statement)메소드를 이용해야 한다.
     <br>
     PreparedStatement의 경우 Statement의 자식 클래스라 자동 형변환되어 정상적으로 처리됨
