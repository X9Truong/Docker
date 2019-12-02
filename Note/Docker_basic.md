### Note

- Đặt tên và hostname cho container

`docker run -it --name "abc" -host centos1 centos:latest`

- Quay lại container `docker attach ID`

- Chạy lệnh bên ngoài container `docker exec ID cmd` , `docker exec -it ID bash`

* Lưu container thành image `docker commit centos1 cent:v1`

`docker save --output /path/myimage.tar ID`

- Khôi phục lại image đã lưu: `docker load -i myimage.tar`

- Đặt tên lại cho image `docker tag ID name:tag` # name/tag







