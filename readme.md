Welcome,

this is a personal template for laravel development with docker.

I will add/fix things as I need it. Use it at your own risk. :innocent:

## How it works

```
git clone git@github.com:mmanzano/docker-php-development.git
```

I think you should change your project code path: `./../../code/project` in `docker-compose.yml`. 

```
chmod +x dadmin
./dadmin [command]
```

## Available commands from dadmin

### ./dadmin build

```
docker-compose up --build -d
```

### ./dadmin cinstall

```
docker-compose exec --user $(id -u) phpproject composer install
```

### ./dadmin key

```
docker-compose exec --user $(id -u) phpproject php artisan key:generate
```

### ./dadmin tinker

```
docker-compose exec phpproject php artisan tinker
```

### ./dadmin migrate

```
docker-compose exec phpproject php artisan migrate
```

### ./dadmin rollback

```
docker-compose exec phpproject php artisan migrate:rollback
```

### ./dadmin seed

```
docker-compose exec phpproject php artisan db:seed
```

### ./dadmin phpunit

```
docker-compose exec --user $(id -u) phpproject ./vendor/bin/phpunit
```

### ./dadmin permissions

Please, execute `git stash -u` before this command. Execute `git stash pop` after. I am opening to suggestions to resolve this permissions issue.

```
docker-compose exec phpproject chmod +777 -R storage/framework
docker-compose exec phpproject chmod +777 -R storage/logs
```

### ./dadmin cc

```
docker-compose exec --user $(id -u) phpproject php artisan config:clear
docker-compose exec --user $(id -u) phpproject php artisan cache:clear
docker-compose exec --user $(id -u) phpproject php artisan view:clear
```

### ./dadmin up

```
docker-compose up -d
```

### ./dadmin stop

```
docker-compose stop
```

### ./dadmin down

```
sudo rm -rf docker-storage
docker-compose down
```

### ./dadmin destroy

This command ***delete all docker containers, images, volumes, networks*** in the current machine (be careful).

```
docker-compose down
docker rm -f $(docker ps -a -q)
docker rmi -f $(docker images -a -q)
docker volume rm $(docker volume ls -q)
docker network rm $(docker network ls | tail -n+2 | awk '{if($2 !~ /bridge|none|host/){ print $1 }}')
```
