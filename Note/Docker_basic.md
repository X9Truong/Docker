### Note

- Download image: `docker pull ubuntu:16.04`

- Đặt tên và hostname cho container

`docker run -it --name "abc" -host centos1 centos:latest`

- Quay lại container `docker attach ID`

- Chạy lệnh bên ngoài container `docker exec ID cmd` , `docker exec -it ID bash`

* Lưu container thành image `docker commit centos1 cent:v1`

`docker save --output /path/myimage.tar ID`

- Khôi phục lại image đã lưu: `docker load -i myimage.tar`

- Đặt tên lại cho image `docker tag ID name:tag` # name/tag

```
FROM — chỉ định image gốc: python, unbutu, alpine…
LABEL — cung cấp metadata cho image. Có thể sử dụng để add thông tin maintainer. Để xem các label của images, dùng lệnh docker inspect.
ENV — thiết lập một biến môi trường.
RUN — Có thể tạo một lệnh khi build image. Được sử dụng để cài đặt các package vào container.
COPY — Sao chép các file và thư mục vào container.
ADD — Sao chép các file và thư mục vào container.
CMD — Cung cấp một lệnh và đối số cho container thực thi. Các tham số có thể được ghi đè và chỉ có một CMD.
WORKDIR — Thiết lập thư mục đang làm việc cho các chỉ thị khác như: RUN, CMD, ENTRYPOINT, COPY, ADD,…
ARG — Định nghĩa giá trị biến được dùng trong lúc build image.
ENTRYPOINT — cung cấp lệnh và đối số cho một container thực thi.
EXPOSE — khai báo port lắng nghe của image.
VOLUME — tạo một điểm gắn thư mục để truy cập và lưu trữ data.
```

* Chia sẻ dữ liệu giữa host và container:

`docker run -it /folder_share/data:/root/data ID_images`

* Chia sẻ dữ liệu giữa container và container:

- Trên container1:

`docker run -it -v /folder_share/data:/root/data --name C1 ID_images`

- Trên container2:

`docker run -it --name C2 --volume-from C1 ubuntu:latest`

* Docker volume-from

`docker volume ls` # check volume

- Tạo volume :

`docker volume create D1`

`docker inspect D1` # Kiểm tra thông tin volume D1

`docker volume rm D` # Xóa volume D1

- Gán volume vào container:

`docker run -it --name C1 --mount source=D2,target=/root/DISK2 ID_image`

- Xóa container rồi mount lại volume để kiểm tra.

* Tạo volume ánh xạ thư mục trong container

`docker volume create --opt device=/root/data --opt type=none --opt o=bind DISK1`

```
[root@docker ~]# docker volume create --opt device=/root/data --opt type=none --opt o=bind DISK1
DISK1
[root@docker ~]# docker volume ls
DRIVER              VOLUME NAME
local               D1
local               D2
local               DISK1
[root@docker ~]# docker inspect DISK1
[
    {
        "CreatedAt": "2019-12-04T00:14:15+07:00",
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/volumes/DISK1/_data",
        "Name": "DISK1",
        "Options": {
            "device": "/root/data",
            "o": "bind",
            "type": "none"
        },
        "Scope": "local"
    }
]
[root@docker ~]#
```
- Đối với loại disk này chúng ta sử dụng -v không sử dụng dạng --mount

`docker run -it -v DISK1:/root/data centos`

* Network 

`docker pull busybox` # Download image busybox

`docker run -it --rm busybox` # Tham số rm sau khi kết thúc tự xóa container

`ls /bin/` # Kiểm tra command support của busybox

```
[root@docker ~]# docker network ls
NETWORK ID          NAME                DRIVER              SCOPE
3ed9a31b6d17        bridge              bridge              local
180a68f65711        host                host                local
627b125c3fa7        none                null                local
[root@docker ~]#
```
`docker run it --name C1 busybox`

```
/ # cd /var/
/var # ls
spool  www
/var # cd www/
/var/www # httpd
/var/www #echo "Hello world" > index.html
```

- Ánh xạ port: `docker run -it --name C2 -p 8888:80 busybox`


`wget -O - 172.17.0.2` # Kiem tra

* Tạo network

`docker network create --driver bridge mynetwokr`

* Chỉ định network

`docker run -it --name C3 --network network1 ID_image`

```
[root@docker ~]# docker network inspect network1
[
    {
        "Name": "network1",
        "Id": "aa35b33c8d7b958206cde7ab995dd7fd169aabf723a8761e067a6c68e10f7651",
        "Created": "2019-12-04T00:41:23.388053353+07:00",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "172.19.0.0/16",
                    "Gateway": "172.19.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {
            "d3b1291f572fcc83eb640db599a8871ed96fa9109b61c37579b12bdcb39de4b7": {
                "Name": "C3",
                "EndpointID": "73f504ef5cdcf408d86c091ca8121f1c40639f34b02579f5543bbe5003a9d266",
                "MacAddress": "02:42:ac:13:00:02",
                "IPv4Address": "172.19.0.2/16",
                "IPv6Address": ""
            }
        },
        "Options": {},
        "Labels": {}
    }
]
[root@docker ~]#
```

`docker -it --name C4 --network network1 -p 9999:80 busybox`

* Attach network cho container

`docker network connect name_network name_container`





