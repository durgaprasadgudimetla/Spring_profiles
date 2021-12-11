https://www.baeldung.com/spring-profiles --> profile management


java -jar  -Dspring.profiles.active=dev  C:\Users\prasa\Documents\workspace-spring-tool-suite-4-4.12.0.RELEASE\flight-booking-service\target\flightbookingservice-0.0.1-SNAPSHOT.jar


mvn clean package -Pprod



DB:

Convenience class for building a DataSource. Provides a limited subset of theproperties
 supported by a typical DataSource as well as detection logic to pickthe most suitable pooling DataSource implementation. 
 
The following pooling DataSource implementations are supported by this builder.When no type has been explicitly set, the first available poolimplementation will be picked: 
•Hikari (com.zaxxer.hikari.HikariDataSource)
•Tomcat JDBC Pool (org.apache.tomcat.jdbc.pool.DataSource)
•Apache DBCP2 (org.apache.commons.dbcp2.BasicDataSource)
•Oracle UCP (oracle.ucp.jdbc.PoolDataSourceImpl)


server:
  port: 2023

spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/postgres
    username: postgres
    password: postgres
    hikari:
      connection-timeout: 20000
      maximum-pool-size: 5
  jpa:
    hibernate:
     ddl-auto: update
     properties:
      hibernate:
        dialect: org.hibernate.dialect.PostgreSQLDialect
        
        
        
        
        
 spring application.yml:
 -----------------------
 
 
 server:
  port: 2023
spring:
  profiles:
    active: 
    - local
---
spring:
 profiles: local
 flight.datasource:
   hibernate:
     properties:
       hibernate:
          dialect: org.hibernate.dialect.PostgreSQLDialect
     driver-class-name: org.postgresql.Driver
     url: jdbc:postgresql://localhost:5432/postgres
     username: postgres
     password: postgres
 jpa:
  hibernate:
    ddl-auto: update
   # hikari:
   #   connection-timeout: 20000
   #   maximum-pool-size: 5
 #jpa:
  #  hibernate:
   #  ddl-auto: update
    # properties:
     # hibernate:
     
      #  dialect: org.hibernate.dialect.PostgreSQLDialect
      
      
application.properties:
------------------------
spring.jpa.hibernate.ddl-auto=none
spring.jpa.hibernate.show-sql=true
spring.datasource.url=jdbc:postgresql://localhost:5432/postgres
spring.datasource.username=postgres
spring.datasource.password=postgres

--
spring.datasource.initialization-mode=always
spring.datasource.initialize=true
spring.datasource.schema=classpath:/schema.sql
spring.datasource.continue-on-error=true


https://www.callicoder.com/spring-boot-jpa-hibernate-postgresql-restful-crud-api-example/

https://dzone.com/articles/bounty-spring-boot-and-postgresql-database
   
