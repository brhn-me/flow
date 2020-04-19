# docker-compose with mysql and phpmyadmin
A sample docker compose for running both mysql and phpmyadmin atonce
```version: '2'
services:
  db-mysql:
    image: mysql:5.7
    container_name: db-mysql
    volumes:
      - ~/volumes/db/mysql/:/var/lib/mysql/
    environment:
      - MYSQL_ROOT_PASSWORD=test
      - MYSQL_DATABASE=test
    ports:
      - 3306:3306
    command: mysqld --lower_case_table_names=1 --skip-ssl --character_set_server=utf8mb4 --explicit_defaults_for_timestamp --default-authentication-plugin=mysql_native_password

  db-phpmyadmin:
    image: phpmyadmin/phpmyadmin:latest
    container_name: db-phpmyadmin
    restart: always
    links:
      - db-mysql
    ports:
      - '1234:80'
    environment:
      PMA_HOST: db-mysql
      PMA_PORT: 3306
      MYSQL_USER: root
      MYSQL_PASSWORD: test
      MYSQL_ROOT_PASSWORD: test
```
