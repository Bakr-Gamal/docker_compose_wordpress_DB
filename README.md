# docker_compose_wordpress_DB

# Dockercompose.yml
services:
  
  mysql_db:
    image: mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: 1234
      MYSQL_DATABASE: wp_db
      MYSQL_USER: wp_user
      MYSQL_PASSWORD: 1234
    volumes:
      - db_data:/var/lib/mysql


  wordpress: 
    depends_on:
      - mysql_db
    image: wordpress:latest
    ports:
      - 8000:80
    restart: always
    environment:
      WORDPRESS_DB_HOST: mysql_db:3306
      WORDPRESS_DB_USER: wp_user
      WORDPRESS_DB_PASSWORD: 1234
      WORDPRESS_DB_NAME: wp_db
    volumes:
      ["./:/var/www/html"]
volumes:
  db_data: {}



# Check the containers is running
bakr@bakr-virtual-machine:~/myproject/ASP_APP$ docker ps
CONTAINER ID   IMAGE              COMMAND                  CREATED        STATUS        PORTS                                     NAMES
95312d3f5ea0   nginx              "/docker-entrypoint.…"   18 hours ago   Up 18 hours   0.0.0.0:8888->80/tcp, [::]:8888->80/tcp   priceless_ride
38e2989e655e   wordpress:latest   "docker-entrypoint.s…"   5 weeks ago    Up 40 hours   0.0.0.0:8000->80/tcp, [::]:8000->80/tcp   wordpress_wordpress_1
4de7058d9505   mysql              "docker-entrypoint.s…"   5 weeks ago    Up 40 hours   3306/tcp, 33060/tcp                       wordpress_mysql_db_1


