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


DB Script:

CREATE TABLE REGION(
    REGIONID INT 				PRIMARY KEY      NOT NULL,
    REGIONNAME          		    CHAR(50) NOT NULL,
);

CREATE TABLE COUNTRY(
   COUNTRYID INT PRIMARY KEY      NOT NULL,
   COUNTRYNAME           CHAR(50) NOT NULL,
   REGIONID         INT     references  REGION(REGIONID)
);

CREATE TABLE LOCATION(
    LOCATIONID INT PRIMARY KEY      NOT NULL,
    LOCATIONNAME          		    CHAR(50) NOT NULL,
	STREETADDRESS                   CHAR(50) NOT NULL,
	CITY           			        CHAR(50) NOT NULL,
	STATEPROVIDENCE                 INT NOT NULL,
	COUNTRY           		        CHAR(50) NOT NULL,
    COUNTRYID                       INT     references COUNTRY(COUNTRYID)
);


insert into region values(1,'Asia');

CREATE TABLE DEPARTMENT(
    DEPTID INT PRIMARY KEY      NOT NULL,
    DEPTNAME          		    CHAR(50) NOT NULL,
	LOCATIONID                   INT     references LOCATION(LOCATIONID)
);



CREATE TABLE MANAGER(
    MANGERID INT PRIMARY KEY      NOT NULL,
    MANAGERNAME          		   CHAR(50) NOT NULL,
	DEPTID                   INT     references DEPARTMENT(DEPTID)
);

CREATE TABLE JOB(
    JOBID INT PRIMARY KEY      NOT NULL,
    JOBTITLE          		   CHAR(50) NOT NULL,
	MINSALARY                   INT  ,
	MAXSALARY					INT
);

CREATE TABLE EMPLOYEE(
    EMPLOYEEID INT PRIMARY KEY      NOT NULL,
    EMPLOYEENAME          		    CHAR(50) NOT NULL,
	MANAGERID                   INT     references MANAGER(MANGERID),
	DEPTID                   INT     references DEPARTMENT(DEPTID),
	JOBID                   INT     references JOB(JOBID)
);

CREATE TABLE EMPLOYEEDETAILS(
    DID INT 				PRIMARY KEY      NOT NULL,
    FNAME          		    CHAR(50) NOT NULL,
	LNAME          		    CHAR(50) NOT NULL,
	EMAIL          		    CHAR(50) NOT NULL,
	ADDRESS1          	    CHAR(100) NOT NULL,
	ADDRESS2          		CHAR(100) NOT NULL,
	PHONENUMBER             BIGINT NOT NULL,
	EMPLOYEEID              INT     references EMPLOYEE(EMPLOYEEID)
);


insert into region values(1,'Asia');
insert into region values(2,'africa');

insert into country values(91,'India',1);

insert into location values(2,'kondapur','whitefield','Hyderabad',500000,'India',91);
insert into location values(1,'Tust','whitefield','Banglore',600000,'India',91);

insert into department values(101,'IT',1);
insert into department values(102,'HR',1);
insert into department values(103,'Travel',1);
insert into department values(104,'Insurance',1);

insert into job values(11,'Java fullstack',15000, 80000);
insert into job values(12,'HR',15000, 50000);
insert into job values(13,'Front End',18000, 90000);


insert into employee values(123,'Durga prasad',1, 101,11);
insert into employee values(124,'Rambabu',1, 102,12);
insert into employee values(125,'Durga prasad',1, 101,13);

ALTER TABLE EMPLOYEE ALTER COLUMN EMPLOYEENAME TYPE VARCHAR(50);


   
