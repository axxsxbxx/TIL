# MariaDB를 통한 정형 데이터 저장



## 1. R-RDBMS 연동

> R이라는 언어로 DB에 테이블 생성, 데이터 삽입/수정/삭제, 테이블 삭제, 데이터 추출 등의 작업을 프로그래밍(구현)하는 것

**1) 드라이버 프로그램 로딩**

> 드라이버 프로그램 : R, JAVA,Python 등의 언어로 DB를 연동할 때 여러가지 세부적인 작업을 대신 수행해주는 프로그램

- JDBC()

**2) MariaDB 데이터베이스에 접속(연결)**

- dbConnect()

**3) 수행하려는 CRUD에 알맞는 SQL 명령을 처리하거나 API에서 제공하는 함수를 이용해서 처리함**

- dbGetQuery()
- dbSendUpdate()
- dbWriteTable()
- dbReadTable()
- dbRemoveTable()

**4) MariaDB 데이터베이스에 접속 해제**

- dbDisconnect()



## 2. `MariaDB` 접속

```R
library(rJava)
library(RJDBC)
library(DBI)

drv <- JDBC(driverClass = 'org.mariadb.jdbc.Driver', 'mariadb-java-client-2.6.2.jar')
conn <- dbConnect(drv, 'jdbc:mariadb://127.0.0.1:3307/work', 'scott', 'tiger')
```



## 3. CRUD 명령 처리

```R
# 데이터 프레임 테이블에 저장
dbWriteTable(db연결객체, '테이블명', 데이터 프레임)
# 기존에 있던 테이블 내용에 추가해서 저장
dbWriteTable(db연결객체, '테이블명', 데이터 프레임, append=TRUE)
# 기존에 있던 테이블 내용 reset 후 새로 저장
dbWriteTable(db연결객체, '테이블명', 데이터 프레임, overwrite=TRUE)

# 테이블 읽기
dbReadTable(db연결객체, '테이블명')

# 쿼리 결과 가져오기
dbGetQuery(db연결객체, '쿼리')

# 데이터 수정
dbSendUpdate(db연결객체, "쿼리")

# 테이블 삭제
dbRemoveTable(db연결객체, '테이블명')

```



## 4. MariaDB 접속 해제

```R
dbDisconnect(conn)
```

