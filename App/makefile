env:
	cp .env.example .env
	vi .env

install:
	docker compose up -d
	docker compose exec php composer require laravel/sail --dev

build:
	./vendor/bin/sail up -d --build
	${cache}
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
	./vendor/bin/sail up -d
	docker compose exec php npm run dev

down:
	./vendor/bin/sail down

php:
	docker compose exec php sh

mysql:
	docker compose exec mysql sh
