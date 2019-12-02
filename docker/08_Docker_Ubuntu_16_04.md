### Cài đặt Docker

* Cài đặt các gói để cho phép apt sử dụng repository qua HTTPS:

```
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common -y
```

* Thêm key chính thức của Docker:

`curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -`

* Thêm Repositories stable:

```
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```
* Update

`sudo apt-get update`

* Cài đặt Docker CE phiên bản mới nhất:

`sudo apt-get install docker-ce -y`

* Để test thử thành công hay khồng chúng ta chạy lệnh :

` docker run hello-world`

<img src="/img/Capture.JPG">

Terminal của bạn hiển thị như thế này là thành công rồi

Lệnh docker run là để chạy một image và sẽ tạo ra một container chính là instance của image hello-world, nếu image đó chưa được pull về thì lệnh docker run sẽ tìm và tự động pull về image có phiên bản mới nhất. Để tìm kiếm một image chúng ta có thể dùng lệnh:

`sudo docker search {image_name}`

```
root@docker:~# docker search mysqld
NAME                              DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
prom/mysqld-exporter                                                              17                                      [OK]
schnitzler/mysqldump              A small container for running mysqldump (dir…   3                                       [OK]
ianneub/mysqldump-to-s3                                                           2                                       [OK]
camil/mysqldump                   Backup and restore MySQL databases using Kub…   2                                       [OK]
youdowell/k8s-mysqldump           Docker image to store mysql dumps to AWS S3     1                                       [OK]
bigtruedata/mysqldump             The bigtruedata/mysqldump image                 1                                       [OK]
bluemeric/mysqld                                                                  0
koollman/mysqldump                Backup and restore MySQL databases using Kub…   0
torvitas/mysqldump                mysqldump                                       0                                       [OK]
istio/examples-bookinfo-mysqldb                                                   0
smcguinness/mysqldump-s3cmd       An image which sends a mysqldump to S3 using…   0
iamtopcat/mysqldump                                                               0
orvice/docker-mysqldump           docker-mysqldump                                0                                       [OK]
simonswine/mysqldumper                                                            0
ackstorm/debian-mysqldump                                                         0
jbrissier/mysqldump               Mysldump Docker utility                         0
anchorfree/mysqld-exporter                                                        0
netquest/mysqldump                                                                0
monachus/rancher-mysqldump        Dump MySQL via Kubernetes CronJob               0                                       [OK]
wondershake/mysqldump             mysqldump and backup to cloud storage           0                                       [OK]
lojzik/mysqldump                  dump all to separate files in docker            0                                       [OK]
jfusterm/mysqld-exporter          Alpine image with mysqld_exporter               0
perfectweb/mysqldump-to-s3        dump mysql db to s3 bucket                      0                                       [OK]
instantlinux/mysqldump            Perform a daily dump of MySQL databases in a…   0                                       [OK]
andromedarabbit/mysqldump-async   A simple wrapper to execute `mysqldump` asyn…   0                                       [OK]
```


