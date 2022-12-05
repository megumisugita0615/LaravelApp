env:
	cp .env.example .env
	vi .env

install:
	docker run --rm \
	-u "$(id -u):$(id -g)" \
	-v "$(pwd):/var/www/html" \
	-w /var/www/html \
	laravelsail/php81-composer:latest \
	composer install --ignore-platform-reqs

build:
	./vendor/bin/sail up -d
	docker compose exec php chmod -R 777 ./storage/
	docker compose exec php php artisan key:generate
	composer dump-autoload
	${cache}
	${dbfresh}
	${dbseed}
	docker compose exec php npm install
	docker compose exec php npm run dev

cache:
	docker compose exec php php artisan config:cache

dbfresh:
	docker compose exec php php artisan migrate:fresh

dbseed:
	docker compose exec php php artisan db:seed

up:
	./vendor/bin/sail up -d
	docker compose exec php npm run dev

down:
	./vendor/bin/sail down

php:
	docker compose exec php sh

mysql:
	./vendor/bin/sail mysql
