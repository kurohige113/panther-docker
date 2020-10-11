# leopard-docker
leopard-docker is php container.

https://ja.wikipedia.org/wiki/VK_1602_レオパルト

# Overall view
```
.
├── leopard   <- https://github.com/kurohige113/leopard.git
│   └── ...
└── leopard-docker   <- here
    ├── README.md
    ├── docker-compose.yml
    └── web
        ├── Dockerfile
        └── php.ini
```

# How to start

1. start container
```
docker-compose up -d
```

2. make html
```
docker exec -it web bash
touch /var/www/leopard/public/index.html
```
or clone (https://github.com/kurohige113/leopard.git)

3. browse localhost

you can see the website.

4. close container

```
docker-compose down
```

# laravel start
```
docker exec -it web bash

# make laravel project
laravel new leopard 

# /var/www/leopard/leopard -> /var/www/leopard
# because document root is /var/www/leopard/public
cd leopard
mv * .[^\.]* ../
cd ..
rm -rf leopard
```
