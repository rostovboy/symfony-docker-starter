cd docker

comment in /php-fpm/Dockerfile: CMD composer install --no-interaction && php-fpm

docker-compose build --pull --no-cache

docker-compose up

docker ps (get container_name)

docker exec -it container_name /bin/sh

php -m -c

composer create-project symfony/skeleton:"6.3.*" temp

from temp move files to root

docker-compose down -v

docker-compose build --pull --no-cache

docker-compose up