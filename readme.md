# up

docker-compose up --build -d

# composer install

docker-compose exec --user $(id -u) phpproject composer install

# migrate

docker-compose exec phpproject php artisan migrate

# tests

docker-compose exec --user $(id -u) phpproject ./vendor/bin/phpunit

# destroy

docker-compose down

docker rm -f $(docker ps -a -q)

docker rmi -f $(docker images -a -q)

docker volume rm $(docker volume ls -q)

docker network rm $(docker network ls | tail -n+2 | awk '{if($2 !~ /bridge|none|host/){ print $1 }}')