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

++++++++++++++++++++++++++++++++++++++++++++++

https://symfony.com/bundles/SymfonyMakerBundle/current/index.html

install maker-bundle

docker exec -it symfony_docker-php-fpm /bin/sh

composer require --dev symfony/maker-bundle

php bin/console list make

+++++++++++++++++++++++++++++++++++++++++++++

create .editorconfig

paste from https://github.com/symfony/symfony/blob/v6.3.8/.editorconfig

install linters:

docker exec -it symfony_docker-php-fpm /bin/sh

composer require --dev friendsofphp/php-cs-fixer

run fix: ./vendor/bin/php-cs-fixer fix


composer require --dev phpstan/phpstan

So, for example if you have your classes in directories src and tests, you can run PHPStan like this:

vendor/bin/phpstan analyse src tests

++++++++++++++++++++++++++++++++++++++++++++

install ORM

docker exec -it symfony_docker-php-fpm /bin/sh

composer require orm (install recipes - press No)

comment in .env:

#DATABASE_URL="postgresql://app:!ChangeMe!@127.0.0.1:5432/app?serverVersion=15&charset=utf8"

add: DATABASE_URL="mysql://database:password@db:3306/database?serverVersion=5.7.43&charset=utf8mb4"

where DATABASE_URL="mysql://user:password@db:3306/database_name?serverVersion=5.7.43&charset=utf8mb4"

get database credentials from /docker/.env

++++++++++++++++++++++++++++++++++++++++++++

create first entity

docker exec -it symfony_docker-php-fpm /bin/sh

php bin/console list make

php bin/console make:entity

Article

- title - string - 255 - no
- introtext - string - 255 - no
- content - text - no
- published - boolean - no
- slug - string - 150 - no

https://www.doctrine-project.org/projects/doctrine-dbal/en/3.7/reference/types.html

When you're ready, create a migration with:

php bin/console make:migration

this command will make migration file in /migrations directory

Review the new migration then run it with:

php bin/console doctrine:migrations:migrate

this creates two tables in our database: articles and doctrine_migration_versions


