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
