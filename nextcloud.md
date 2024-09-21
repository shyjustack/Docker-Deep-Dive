version: '3.8'

services:
  db:
    image: mariadb:latest
    container_name: nextcloud-db
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: password
      MYSQL_DATABASE: nextcloud
      MYSQL_USER: nextcloud
      MYSQL_PASSWORD: password
    volumes:
      - db_data:/var/lib/mysql

  app:
    image: nextcloud:latest
    container_name: nextcloud-app
    restart: always
    ports:
      - 8080:80
    links:
      - db
    volumes:
      - nextcloud_data:/var/www/html
    environment:
      MYSQL_PASSWORD: password
      MYSQL_DATABASE: nextcloud
      MYSQL_USER: nextcloud
      MYSQL_HOST: db

volumes:
  db_data:
  nextcloud_data:
