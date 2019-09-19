PHONY: up down bench

up:
	docker-compose up -d

down:
	docker-compose down

bench:
	docker-compose run bench -c 1 -q 5 -n 100 http://nginx/rate_limit
