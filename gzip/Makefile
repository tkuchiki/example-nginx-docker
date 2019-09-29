PHONY: up down

up:
	docker-compose up -d

down:
	docker-compose down

curl:
	curl -I 127.0.0.1:$(shell docker inspect -f '{{ (index (index .NetworkSettings.Ports "80/tcp") 0).HostPort }}' gzip_nginx1_1)/test.json

curl_gzipped:
	curl -H "Accept-Encoding: gzip" -I 127.0.0.1:$(shell docker inspect -f '{{ (index (index .NetworkSettings.Ports "80/tcp") 0).HostPort }}' gzip_nginx1_1)/test.json
