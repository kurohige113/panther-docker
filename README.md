# panther-docker
panther-docker is php container with laravel + mysql8.0

https://wikiwiki.jp/wotanks/Pz.Kpfw.%20V%20Panther

# Overall view
```
.
├── panther   <- https://github.com/kurohige113/panther.git
│   └── ...
└── panther-docker   <- here
    ├── README.md
    ├── docker-compose.yml
    ├── web
    │   ├── Dockerfile
    │   └── php.ini
    └── db
        ├── Dockerfile
        └── my.cnf
```

# How to start

1. start container
```
docker-compose up -d
```

2. make html
```
docker exec -it web bash
touch /var/www/panther/public/index.html
```
or clone (https://github.com/kurohige113/panther.git)

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
# create laravel ver.6
composer create-project "laravel/laravel=6.0.*" panther

# /var/www/panther/panther -> /var/www/panther
# because document root is /var/www/panther/public
cd panther
mv * .[^\.]* ../
cd ..
rm -rf panther
```

# db connection
```
# connection
$ mysql -u root -p

# create user 
create user 'hoge'@'localhost' identified by 'password'; // Unnecessary

# change grant
grant all privileges on panther_db.* to 'hoge'@'localhost'; // Unnecessary

# change user password authentication method
ALTER USER 'admin'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password'; // Unnecessary
ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY 'root';

# check user
SELECT user, host, plugin FROM mysql.user;

```

# laravel .env
```
DB_CONNECTION=mysql
DB_HOST=db             // <- here
DB_PORT=3306
DB_DATABASE=panther_db // <- here
DB_USERNAME=root       // <- here
DB_PASSWORD=root       // <- here
```

```
$ docker exec -it web bash
$ php artisan migrate 
```

OK
