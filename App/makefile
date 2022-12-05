env:
	cp .env.example .env
	vi .env

install:
	docker run --rm \
    	-u "$(id -u):$(id -g)" \
    	-v $(pwd):/var/www/html \
    	-w /var/www/html \
    	laravelsail/php81-composer:latest \
    	composer install --ignore-platform-reqs \

build:
	docker compose up -d
	${cache}
	docker compose exec php chmod -R 777 ./storage/
	docker compose exec php php artisan key:generate
	${dbfresh}
	${dbseed}
	docker compose exec php npm install
	docker compose exec php npm run dev

dbfresh:
	docker compose exec php php artisan migrate:fresh

dbseed:
	docker compose exec php php artisan db:seed

cache:
	docker compose exec php php artisan cache:clear
	docker compose exec php php artisan config:cache

up:
	docker compose up -d
	docker compose exec php npm run dev

down:
	docker compose down

php:
	docker compose exec php sh

mysql:
	docker compose exec mysql sh
