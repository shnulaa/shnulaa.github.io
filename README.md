#一点点说明

这是[BeiYuu.com](http://beiyuu.com)的示例代码，如果你看了[使用Github Pages建独立博客](http://beiyuu.com/github-pages/)，希望看下去哦：

* 马上动手，很赞
* 感谢认可
* 推荐阅读：[我为什么写博客？](http://beiyuu.com/why-blog/)
* 想复用我的设计，没问题，标个出处就好啦
* 转载也没问题，标个出处呗少年
* 恩，认真的童鞋最可爱啦~


[[挂载ntfs]]
* rc.local

```
 mount -t nfs4  192.168.50.53:/volume2/nas-share /mnt/nfs
 mount.nfs  192.168.50.53:/volume1/video/movie /mnt/nfs/gateway/docker/data/emby/share2
 mount.nfs  192.168.50.53:/volumeUSB1/usbshare1-2/movie /mnt/nfs/gateway/docker/data/emby/share3
 autossh -M 20002 -fN -o &quot;PubkeyAuthentication=yes&quot; -o &quot;StrictHostKeyChecking=false&quot; -o &quot;ServerAliveInterval 60&quot; -o &quot;ServerAliveCountMax 3&quot; -R a_a_a_a:80:localhost:80 -p 22 root@119.28.78.137
```


* wiki

```
 docker run -d --name wiki -p 81:80 --restart=always -v /mnt/nfs/gateway/docker/data/wiki/html:/var/www/html seti/php52
 chmod -R 777 /var/www/html
```


* traefik
<pre> docker run --restart=always -d -p 8080:8080 -p 80:80 -v  /mnt/nfs/gateway/docker/data/traefik/traefik.toml:/etc/traefik/traefik.toml -v /var/run/docker.sock:/var/run/docker.sock traefik:v1.7</pre>

* git

```
 docker run --detach \
 --publish 22443:443 --publish 2280:80  --publish 2222:22 \
 --name git \
 --memory 2g \
 --restart always \
 --volume /mnt/nfs/gateway/docker/data/git/config:/etc/gitlab \
 --volume /mnt/nfs/gateway/docker/data/git/logs:/var/log/gitlab \
 --volume /mnt/nfs/gateway/docker/data/git/data:/var/opt/gitlab \
 gitlab/gitlab-ce:latest
```


* portainer
<pre> docker run -d --restart=always --name docker -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock -v /mnt/nfs/gateway/docker/data/portainer/data:/data -v /mnt/nfs/gateway/docker/data/portainer/public:/public portainer/portainer</pre>

* file

```
 docker run \
 -v /mnt/nfs/gateway/docker/data/file/srv:/srv \
 -v /mnt/nfs/gateway/docker/data/file/database.db:/database.db \
 -p 10080:80 \
 --name file \
 --restart=always \
 filebrowser/filebrowser
```


* bt

```
 docker run -d  \
    --name=bt1  \
    -e WEBUIPORT=8080  \
    -e PUID=1026 \
    -e PGID=100 \
    -e TZ=Asia/Shanghai \
    -p 16881:16881  \
    -p 16881:16881/udp  \
    -p 8082:8080  \
    -v /mnt/nfs/gateway/docker/data/bt1/config:/config  \
    -v /mnt/nfs/gateway/docker/data/bt1/downloads:/downloads  \
    --restart unless-stopped  \
    superng6/qbittorrent:latest
```


* emby

```
 docker run -d \
   --restart=always \
    --name emby2 \
    -e PUID=1000 \
    -e PGID=1000 \
    -p 8096:8096 \
    -v /mnt/nfs/gateway/docker/data/emby/config:/config \
    -v /mnt/nfs/gateway/docker/data/emby/share1:/mnt/share1 \
    -v /mnt/nfs/gateway/docker/data/emby/share2:/mnt/share2 \
    -v /mnt/nfs/gateway/docker/data/emby/share3:/mnt/share3 \
    nvllsvm/emby-unlocked
 
 docker run -d \
  --restart=always \
   --name emby3 \
   -p 8096:8096 \
   -v /mnt/nfs/gateway/docker/data/emby/config2:/config \
   -v /mnt/nfs/gateway/docker/data/emby/share1:/mnt/share1 \
   -v /mnt/nfs/gateway/docker/data/emby/share2:/mnt/share2 \
   -v /mnt/nfs/gateway/docker/data/emby/share3:/mnt/share3 \
   -v /mnt/nfs/gateway/docker/data/emby/share2:/data/media \
   yukinococo/emby_crack:unix-x64
```



