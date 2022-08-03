## Quick start

Clone repo
```bash
cd ${S2S_PATH}
git clone https://github.com/stock2shop/queue-orchestration.git
```

Run temporal and s2s-worker in docker
```bash
cd queue-orchestration

# Vendor PHP deps
composer update
./vendor/bin/rr get

# Config
cp .env.sample .env

# Start containers
# docker-compose up -d --build
docker-compose up -d
```

View logs
```bash
docker logs -f temporal
docker logs -f s2s-worker
```


## Demo

As per [README](https://github.com/stock2shop/queue-orchestration)

Start a bash session on `s2s-worker`
```bash
docker exec -it s2s-worker bash
cd /app
```

Push data to a named queue group
```bash
php app.php push bob "hello bob" -s 1000
php app.php push mario "hello mario" -s 1000
php app.php push luigi "hello luigi" -s 10
```

Query DB
```bash
mycli -h temporal-mysql -u root -p asdf -D s2sworker -e "show tables;"
mycli -h temporal-mysql -u root -p asdf -D s2sworker -e \
    "select * from channels;"
```