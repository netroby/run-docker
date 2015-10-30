# run-docker
this is a example to tell how to run docker for production 
You should installed docker on your linux host, if not, you may want installed them by run 
```
curl -sS -L -1 get.docker.com | sh
```

```bash
#!/bin/bash
docker rm -vf web
docker rm -vf redis
docker rm -vf db
echo "Previous container been removed"
screen -dm docker run -t -i --name db -v /data/mysql-data:/mysql-data -p 127.0.0.1:3306:3306 netroby/fm-dev /bin/bash
sleep 1
screen -dm docker run --name redis -v /data/redis:/data  -d redis redis-server --appendonly yes
sleep 1
screen -dm docker run -t -i --name web -v /data/www/conf.d:/etc/nginx/conf.d -v /data/www:/www -p 443:443 -p 80:80 --link db:db --link redis:redis netroby/fn-dev /bin/bash
sleep 1
echo "Started all container"
docker stop web
docker stop redis
docker stop db
docker start db
docker start redis
docker start web
echo "All done"

```


## Donate me please

![Scan QRCode donate me via Alipay](https://www.netroby.com/assets/images/alipayme.jpg)

**Scan QRCode donate me via Alipay**
