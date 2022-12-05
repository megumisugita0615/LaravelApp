env:
	cp .env.example .env
	vi .env

install:
	docker compose up -d
	docker compose exec php composer require laravel/sail --dev

build:
	docker compose up -d --build
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
