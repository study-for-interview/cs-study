# Statement vs PreparedStatement

Statement 와 PreparedStatement는 모두 SQL 쿼리를 실행 하는데 사용 할 수 있습니다. 

Statement – 문자열 기반 sql 쿼리 사용
PreparedStatement – 매개변수화된 SQL 쿼리를 실행하는 데 사용됩니다.

# Statement

## 1. Statement 인터페이스 는 문자열을 SQL 쿼리로 받아들입니다. 따라서 SQL 문자열 을 연결할 때 코드 가독성이 떨어집니다 .

```java
public void insert(PersonEntity personEntity) {
    String query = "INSERT INTO persons(id, name) VALUES(" + personEntity.getId() + ", '"
      + personEntity.getName() + "')";

    Statement statement = connection.createStatement();
    statement.executeUpdate(query);
}
```

## 2. SQL 인젝션에 취약하다 . 다음 예는 이러한 약점을 보여줍니다.

첫 번째 줄에서 업데이트는 모든 행의 " name " 열을 " hacker "로 설정합니다. "—" 이후의 모든 것은 SQL에서 주석으로 해석되고 업데이트 문의 조건은 무시됩니다. 두 번째 줄에서 " name " 열의 따옴표가 이스케이프 처리되지 않았기 때문에 삽입이 실패합니다 .
```java
dao.update(new PersonEntity(1, "hacker' --"));
dao.insert(new PersonEntity(1, "O'Brien"))
```

## 3. JDBC는 인라인 값이 있는 쿼리를 데이터베이스에 전달합니다 .

따라서 쿼리 최적화가 없으며 가장 중요한 것은 데이터베이스 엔진이 모든 검사를 보장해야 한다는 것 입니다. 또한 쿼리는 데이터베이스에 동일하게 표시되지 않으며 캐시 사용을 방지합니다 . 마찬가지로 batch updates는 별도로 실행해야 합니다.

```java
public void insert(List<PersonEntity> personEntities) {
    for (PersonEntity personEntity: personEntities) {
        insert(personEntity);
    }
}
```

## 4. Statement 인터페이스 는 CREATE , ALTER 및 DROP 과 같은 DDL 쿼리  에 적합합니다 .

```java
public void createTables() {
    String query = "create table if not exists PERSONS (ID INT, NAME VARCHAR(45))";
    connection.createStatement().executeUpdate(query);
}
```

## 마지막으로 파일 및 배열을 저장하고 검색 하는 데 Statement 인터페이스를 사용할 수 없습니다 .


--- 

# PreparedStatement

## 1. PreparedStatement 는 Statement 인터페이스를 확장합니다.
파일 및 배열을 포함하여 다양한 개체 유형을 바인딩하는 메서드가 있습니다. 따라서 코드 를 이해하기 쉬워 집니다.

```java
public void insert(PersonEntity personEntity) {
    String query = "INSERT INTO persons(id, name) VALUES( ?, ?)";

    PreparedStatement preparedStatement = connection.prepareStatement(query);
    preparedStatement.setInt(1, personEntity.getId());
    preparedStatement.setString(2, personEntity.getName());
    preparedStatement.executeUpdate();
}
```

## 2. 제공된 모든 매개변수 값에 대한 텍스트를 이스케이프 처리하여 SQL 주입으로부터 보호합니다 .

```java
@Test 
void whenInsertAPersonWithQuoteInText_thenItNeverThrowsAnException() {
    assertDoesNotThrow(() -> dao.insert(new PersonEntity(1, "O'Brien")));
}

@Test 
void whenAHackerUpdateAPerson_thenItUpdatesTheTargetedPerson() throws SQLException {

    dao.insert(Arrays.asList(new PersonEntity(1, "john"), new PersonEntity(2, "skeet")));
    dao.update(new PersonEntity(1, "hacker' --"));

    List<PersonEntity> result = dao.getAll();
    assertEquals(Arrays.asList(
      new PersonEntity(1, "hacker' --"), 
      new PersonEntity(2, "skeet")), result);
}
```

## 3. PreparedStatement 는 사전 컴파일을 사용 합니다. 

데이터베이스는 쿼리를 받자마자 쿼리를 미리 컴파일하기 전에 캐시를 확인합니다. 따라서 캐시되지 않은 경우 데이터베이스 엔진은 다음 사용을 위해 이를 저장합니다.

또한 이 기능 은 비 SQL 바이너리 프로토콜을 통해 데이터베이스와 JVM 간의 통신 속도를 높 입니다. 즉, 패킷에 데이터가 적어서 서버 간의 통신이 더 빨라집니다.

## 4.  PreparedStatement 는 단일 데이터베이스 연결 동안  batch execution을 제공합니다 .

```java
public void insert(List<PersonEntity> personEntities) throws SQLException {
    String query = "INSERT INTO persons(id, name) VALUES( ?, ?)";
    PreparedStatement preparedStatement = connection.prepareStatement(query);
    for (PersonEntity personEntity: personEntities) {
        preparedStatement.setInt(1, personEntity.getId());
        preparedStatement.setString(2, personEntity.getName());
        preparedStatement.addBatch();
    }
    preparedStatement.executeBatch();
}
```

## 5. PreparedStatement 는 BLOB 및  CLOB 데이터 유형 을 사용하여 파일을 저장하고 검색하는 쉬운 방법을 제공합니다 . 

같은 맥락에서 java.sql.Array 를 SQL Array로 변환하여 목록을 저장하는 데 도움이 됩니다.

## 마지막으로 PreparedStatement 는 반환된 결과에 대한 정보를 포함하는 getMetadata() 와 같은 메서드를 구현합니다 .


### 두 인터페이스 모두 SQL 쿼리를 실행하는 방법을 제공하지만 DDL 쿼리 에는 Statement 를 사용하고 DML 쿼리에는 PreparedStatement 를 사용하는 것이 더 적합 합니다.

--- 
참고 :

https://www.baeldung.com/java-statement-preparedstatement
