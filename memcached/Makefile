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
	docker cp 1.jpg $(shell docker-compose ps -q memcached1):/tmp/1.jpg
	docker cp 1.jpg $(shell docker-compose ps -q memcached2):/tmp/1.jpg
	docker cp 1.jpg $(shell docker-compose ps -q memcached3):/tmp/1.jpg
	docker cp 1.jpg $(shell docker-compose ps -q nginx1):/tmp/2.jpg

bench1:
	docker-compose run bench -n 1000000 http://nginx1/1.jpg

bench2:
	docker-compose run bench -n 1000000 http://nginx1/2.jpg

bench3:
	docker-compose run bench -n 1000000 http://nginx1/3.jpg

bench_multi1:
	docker-compose run bench -n 1000000 http://nginx1/multi/1.jpg

bench_multi2:
	docker-compose run bench -n 1000000 http://nginx1/multi/2.jpg

bench_multi3:
	docker-compose run bench -n 1000000 http://nginx1/multi/3.jpg

set_images:
	if [ ! -f memcli ]; then \
		curl -LO https://github.com/tkuchiki/memcli/releases/download/v0.1.0/memcli_linux_amd64.zip; \
		unzip memcli_linux_amd64.zip; \
		\
	fi
	docker cp memcli $(shell docker-compose ps -q memcached1):/tmp/memcli
	docker cp memcli $(shell docker-compose ps -q memcached2):/tmp/memcli
	docker cp memcli $(shell docker-compose ps -q memcached3):/tmp/memcli
	docker-compose exec memcached1 bash -c "cat /tmp/1.jpg | /tmp/memcli set --key '/1.jpg'"
	docker-compose exec memcached2 bash -c "cat /tmp/1.jpg | /tmp/memcli set --key '/2.jpg'"
	docker-compose exec memcached3 bash -c "cat /tmp/1.jpg | /tmp/memcli set --key '/3.jpg'"
	docker-compose exec memcached1 bash -c "cat /tmp/1.jpg | /tmp/memcli set --key '/multi/1.jpg'"
	docker-compose exec memcached2 bash -c "cat /tmp/1.jpg | /tmp/memcli set --key '/multi/2.jpg'"
	docker-compose exec memcached3 bash -c "cat /tmp/1.jpg | /tmp/memcli set --key '/multi/3.jpg'"

setup:
	make up
	make download_file
	make upload_file
	make set_images
