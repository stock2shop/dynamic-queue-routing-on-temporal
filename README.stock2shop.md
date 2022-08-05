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
```

Push data to a named queue group, see `app/src/Activity/RouteActivity.php`
```bash
cd /app
# Uses custom queue
php app.php push bob "hello bob" -s 110
php app.php push mario "hello mario" -s 110
# Default priority
php app.php push luigi "hello luigi" -s 11
```

View RR stats
```bash
./rr workers -i
```

Query DB counters
```bash
mycli -h temporal-mysql -u root -p asdf -D s2sworker -e \
    "select * from channels;"
```