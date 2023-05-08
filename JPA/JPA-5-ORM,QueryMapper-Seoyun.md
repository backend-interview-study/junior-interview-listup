# Q. ORM Framework와 Query Mapping Framework의 차이에 대해서 설명해주세요. (JPA vs Mybatis)

## 면접 한 줄 정리
: Persistence Framwork는 SQL Mapper와 ORM으로 나눌 수 있습니다.<br> 
ORM과 Query Mapping Framwork 즉 SQL Mapper의 큰 차이로는 쿼리 지원 여부와 매핑의 방법, DBMS의 종속 여부입니다.

- SQL Mapper 
  - SQL문과 객체(obejct)의 필드를 매핑하여 데이터를 객체화
  - RDB에 따라 SQL 문법이 다르기 때문에 DBMS에 종속적인 문제
  - SQL문을 직접 작성하고 쿼리 수행 결과를 어떠한 객체에 매핑할지 바인딩 해줘야 한다. 
  - 객체와 쿼리문을 모두 관리해야하며 CRUD 메소드를 직접 다 구현해야한다
  - 대표적인 프레임워크 MyBatis
- ORM
  - 객체와 관계형 데이터베이스를 매핑하여 RDB 테이블을 객체지향적으로 사용
  - DBMS에 종속적이지 않다
  - 객체간의 관계를 바탕으로 SQL문을 자동으로 생성하고 직관적인 코드(메서드)로 데이터 조작이 가능함으로 비지니스 로직에 집중할 수 있다. (CRUD 제공과 페이징 처리 등)
  - 대표적인 예 JPA

JPA와 Mybatis 차이의 예로
Mybatis는 DBMS에 종속적이기 때문에 데이터베이스 정보가 변경되면 연관된 코드도 함께 수정해주어야 하는 반면 JPA는 객체만 변경하면되며
Mybatis의 경우 쿼리를 직접 작성하여 복잡한 쿼리도 해결가능한 반면 JPA는 복잡한 쿼리는 해결이 어렵습니다. 

---
자세한 내용은 [블로그 링크](https://velog.io/@may_yun/JPA-ORM%EA%B3%BC-SQL-Mapper%EC%9D%98-%EC%B0%A8%EC%9D%B4)를 참고해 주세요. 
