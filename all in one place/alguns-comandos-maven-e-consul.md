mvn clean install
mvn clean package
mvn dependency:tree
mvn dependency:tree -Dverbose | grep commons-logging
mvn dependency:tree | grep commons-logging
consul agent -dev &
mvn spring-boot:run

