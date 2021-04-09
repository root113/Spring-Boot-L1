# Spring-Boot-L1
## Setup
1. Download this repository as ```.zip``` or clone the repository by following command
```
git clone https://github.com/root113/Spring-Boot-L1.git
```

2. You need to have ```PostgreSQL``` and ```Docker``` installed on your system
   - To install PostgreSQL follow the instructions on these links below depending on your OS: 
      - For Windows, refer to [here](https://www.postgresqltutorial.com/install-postgresql/).
      - For MacOS, refer to [here](https://www.postgresqltutorial.com/install-postgresql-macos/).
      - For Linux, refer to [here](https://www.postgresql.org/download/linux/).
   - To install Docker follow the instructions on these links below depending on your OS:
      - For Windows, refer to [here](https://docs.docker.com/docker-for-windows/install/).
      - For MacOS, refer to [here](https://docs.docker.com/docker-for-mac/install/).
      - For Ubuntu, refer to [here](https://docs.docker.com/engine/install/ubuntu/).
      - For Debian, refer to [here](https://docs.docker.com/engine/install/debian/).
      - For Fedora, refer to [here](https://docs.docker.com/engine/install/fedora/).
      - For CentOS, refer to [here](https://docs.docker.com/engine/install/centos/).

3. Start a postgres instance and follow the insturctions. (You can name credentials at your will but remember that you have to change relevant parts inside source code according to it)
   1. Init:
      ```
      docker run --name postgres-spring -e POSTGRES_PASSWORD=1234 -d -p  5432:5432 postgres:alpine
      ```
   3. Check new container's id:
      ```
      docker ps
      ```
   3. Bash into the container:
      ```
      docker exec -it container_id bin/bash
      ```

4. Switch to user postgres
   ```
   psql -U postgres
   ```

5. Database setup
   1. Create database and connect:
      ```
      CREATE DATABASE demodb;
      ```
      ```
      \c demodb
      ```
   2. If you are not using IntelliJ Idea Ultimate Edition, the sql script that is writtien inside ```demo/src/main/resources/db/migration/v1__PersonTable.sql``` will not work. Thus, you have to create the table manually. If not, skip this step.
      ```
      CREATE TABLE person (id UUID NOT NULL PRIMARY KEY, name VARCHAR(100) NOT NULL);
      ```
   3. Create extension for UUID generator:
      ```
      CREATE EXTENSION "uuid-ossp";
      ```
   4. Insert your test datas:
      ```
      INSERT INTO person (id, name) VALUES (uuid_generate_v4(), 'Example Name');
      ```

### Usage
Postman is recommended but not necessary. You can use any browser with below command to list the test datas (Default port is set to 8080. If it is already in use, kill which process uses it or try changing the port to something different.)
```
localhost:8080/api/v1/person
```
