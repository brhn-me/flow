# docker-compose with mysql and phpmyadmin
A sample docker compose for running both mysql and phpmyadmin atonce
```version: '2'
services:
  mysql:
    image: mysql:5.7
    container_name: mysql
    volumes:
      - ~/volumes/mysql/:/var/lib/mysql/
    environment:
      - MYSQL_USER=user
      - MYSQL_PASSWORD=user
      - MYSQL_ROOT_PASSWORD=root
      - MYSQL_ALLOW_EMPTY_PASSWORD=yes
      - MYSQL_DATABASE=db
    ports:
      - 3306:3306
    command: mysqld --lower_case_table_names=1 --skip-ssl --character_set_server=utf8mb4 --explicit_defaults_for_timestamp --default-authentication-plugin=mysql_native_password

  phpmyadmin:
    image: phpmyadmin/phpmyadmin:latest
    container_name: phpmyadmin
    restart: always
    depends_on:
      - mysql
    links:
      - mysql
    ports:
      - '1234:80'
```
