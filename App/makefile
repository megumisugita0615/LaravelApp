env:
	cp .env.example .env
	vi .env

build:
	docker compose up -d
	docker compose exec php composer require laravel/sail --dev
	./vendor/bin/sail up -d --build
	docker compose exec php php artisan migrate:fresh
	docker compose exec php php artisan db:seed
	docker compose exec php php artisan key:generate
	docker compose exec php npm install
	docker compose exec php npm run dev

up:
	./vendor/bin/sail up -d
	docker compose exec php npm run dev

down:
	./vendor/bin/sail down

php:
	docker compose exec php sh

mysql:
	docker compose exec mysql sh

dbfresh:
	docker compose exec php php artisan migrate:fresh

dbseed:
	docker compose exec php php artisan db:seed
