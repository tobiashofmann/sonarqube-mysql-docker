# sonarqube-mysql-docker
A docker compose file to have a Docker image for SonarQube using MySQL as DB, and not the embedded database. SonarQube won't allow to upgrade itself on embedded db. Using MySQL allows to easily upgrade the SQ server, eg. from 7.0 to 7.1

# Create docker container

You need to have Docker installed. 

```sh
git clone https://github.com/tobiashofmann/sonarqube-mysql-docker.git
cd sonarqube-mysql-docker
docker-compose up
```

This will create a Docker container for the MySQL DB and one for the SonarQube server. 

# Note

## TLS

MySQL uses TLS connection by default, meaning that SonarQube cannot connect to MySQL without having first installed the db certificate. This behaviour is deactivated in the connection String by setting useSSL=false

```yml
- SONARQUBE_JDBC_URL=jdbc:mysql://db:3306/sonar?useUnicode=true&characterEncoding=utf8&rewriteBatchedStatements=true&useConfigs=maxPerformance&useSSL=false
```

## SHA

MySQL 8 uses a new password algorithm based on sha-2. The MySQL driver shipped with the SonarQube 7.x image cannot authenticate the user because of this. The workaround is to use MySQL 5.7 and not 8.x.
