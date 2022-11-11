<p align="center"><img src="https://laravel.com/assets/img/components/logo-laravel.svg"></p>

# Laravel Docker
# Рабочий шаблон docker & Laravel Framework 7.27.0

Use:
Terminal => Linux

DevDependencies:
1. Install git
2. Install docker
3. Install docker-compose
4. Install make

Load docker images and create containers || start containers
```bash
make start
```

Stop containers
```bash
make stop
```

Show all started containers
```bash
make show
```

Add SSL certificate
```bash
sudo docker run -it --rm --name certbot \
            -v "/etc/letsencrypt:/etc/letsencrypt" \
            -v "/var/lib/letsencrypt:/var/lib/letsencrypt" \
            -p 80:80  certbot/certbot certonly
```
# File .env

DB_CONNECTION=mysql

DB_HOST=test-db

DB_PORT=3306

DB_DATABASE=test

DB_USERNAME=root

DB_PASSWORD=secret
