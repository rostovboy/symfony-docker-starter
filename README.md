cd docker

comment in /php-fpm/Dockerfile: #CMD composer install --no-interaction && php-fpm

docker-compose build --pull --no-cache

docker-compose up

docker ps (get container_name)

docker exec -it container_name /bin/sh

php -m -c

composer create-project symfony/skeleton:"6.3.*" temp

from temp move files to root

uncomment in /php-fpm/Dockerfile: CMD composer install --no-interaction && php-fpm

docker-compose down -v

docker-compose build --pull --no-cache

docker-compose up

++++++++++++++++++++++++++++++++++++++++++++++

install debug and profiling tools

docker exec -it symfony_docker-php-fpm /bin/sh

composer require debug

to run profiler go to url http://localhost:8000/_profiler