PHONY: up down bench dryrun

up:
	docker-compose up -d

down:
	docker-compose down

bench:
	docker-compose run bench -c 1 -q 5 -n 100 http://nginx/rate_limit

dryrun:
	docker-compose run bench -c 1 -q 20 -n 100 http://nginx/rate_limit_dryrun
