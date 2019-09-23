PHONY: up down download_file bench

up:
	docker-compose up -d

down:
	docker-compose down

download_file:
	if [ ! -f 1.jpg ]; then \
		curl -L https://httpbin.org/image/jpeg -o 1.jpg ; \
	fi

upload_file:
	make upload_file1
	make upload_file2
	make upload_file3

upload_file1:
	docker cp 1.jpg $(shell docker-compose ps -q nginx1):/tmp/1.jpg

upload_file2:
	docker cp 1.jpg $(shell docker-compose ps -q nginx2):/tmp/2.jpg

upload_file3:
	docker cp 1.jpg $(shell docker-compose ps -q nginx3):/tmp/3.jpg

bench1:
	docker-compose run bench -n 1000000 http://nginx1/1.jpg

bench2:
	docker-compose run bench -n 1000000 http://nginx1/2.jpg

bench3:
	docker-compose run bench -n 1000000 http://nginx1/3.jpg

set_ips:
	docker-compose exec redis redis-cli SET /1.jpg $(shell  docker inspect -f '{{.NetworkSettings.Networks.redis_default.IPAddress}}' redis_nginx1_1)
	docker-compose exec redis redis-cli SET /2.jpg $(shell  docker inspect -f '{{.NetworkSettings.Networks.redis_default.IPAddress}}' redis_nginx2_1)
	docker-compose exec redis redis-cli SET /3.jpg $(shell  docker inspect -f '{{.NetworkSettings.Networks.redis_default.IPAddress}}' redis_nginx3_1)

setup:
	make up
	make download_file
	make upload_file
	make set_ips
