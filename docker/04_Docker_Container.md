## Container

Các phần mềm, chương trình sẽ được Container Engine ( là một công cụ ảo hóa tinh gọn được cài đặt trên host OS) đóng gói thành các container.

Thế Container là gì, nó là một giải pháp để chuyển giao phần mềm một cách đáng tin cậy giữa các môi trường máy tính khác nhau bằng cách:

* Tạo ra một môi trường chứa mọi thứ mà phần mềm cần để có thể chạy được.

* Không bị các yếu tố liên quan đến môi trường hệ thống làm ảnh hưởng tới.

* Cũng như không làm ảnh hưởng tới các phần còn lại của hệ thống.

Bạn có thể hiểu là ruby, rails, mysql ... kia được bỏ gọn vào một hoặc nhiều cái thùng (container), ứng dụng của bạn chạy trong những chiếc thùng đó, đã có sẵn mọi thứ cần thiết để hoạt động, không bị ảnh hưởng từ bên ngoài và cũng không gây ảnh hưởng ra ngoài.

Các tiến trình (process) trong một container bị cô lập với các tiến trình của các container khác trong cùng hệ thống tuy nhiên tất cả các container này đều chia sẻ kernel của host OS (dùng chung host OS).

Đây một nền tảng mở dành cho các lập trình viên, quản trị hệ thống dùng để xây dựng, chuyển giao và chạy các ứng dụng dễ dàng hơn. Ví dụ, bạn có một app java, bạn sẽ không cần cài đặt JDK vào máy thật để chạy app đó, chỉ cần kiếm container đã được setting tương ứng cho app về, bật nó lên, cho app chạy bên trong môi trường container đó, vậy là ok. Khi không sài nữa thì tắt hoặc xóa bỏ container đó đi, không ảnh hưởng gì tới máy thật của bạn.


**Ưu điểm:**

* Linh động: Triển khai ở bất kỳ nơi đâu do sự phụ thuộc của ứng dụng vào tầng OS cũng như cơ sở hạ tầng được loại bỏ.

* Nhanh: Do chia sẻ host OS nên container có thể được tạo gần như một cách tức thì. Điều này khác với vagrant - tạo môi trường ảo ở level phần cứng, nên khi khởi động mất nhiều thời gian hơn.

* Nhẹ: Container cũng sử dụng chung các images nên cũng không tốn nhiều disks.

* Đồng nhất :Khi nhiều người cùng phát triển trong cùng một dự án sẽ không bị sự sai khác về mặt môi trường.

* Đóng gói: Có thể ẩn môi trường bao gồm cả app vào trong một gói được gọi là container. Có thể test được các container. Việc bỏ hay tạo lại container rất dễ dàng.

**Nhược điểm:**

Xét về tính an toàn:

* Do dùng chung OS nên nếu có lỗ hổng nào đấy ở kernel của host OS thì nó sẽ ảnh hưởng tới toàn bộ container có trong host OS đấy.

* Ngoài ra hãy thử tưởng tượng với host OS là Linux, nếu trong trường hợp ai đấy hoặc một ứng dụng nào đấy có trong container chiếm được quyền superuser, điều gì sẽ xảy ra? Về lý thuyết thì tầng OS sẽ bị crack và ảnh hưởng trực tiếp tới máy host bị hack cũng như các container khác trong máy đó (hacker sử dụng quyền chiếm được để lấy dữ liệu từ máy host cũng như từ các container khác trong cùng máy host bị hack chẳng hạn).

Docker có hai khái niệm chính cần hiểu, đó là image và container:

Container: Tương tự như một máy ảo, xuất hiện khi mình khởi chạy image.

Tốc độ khởi chạy container nhanh hơn tốc độ khởi chạy máy ảo rất nhiều và bạn có thể thoải mái chạy 4,5 container mà không sợ treo máy.

Các files và settings được sử dụng trong container được lưu, sử dụng lại, gọi chung là images của docker.

`Image`: Tương tự như file .gho để ghost win mà mấy ông cài win dạo hay dùng.

Image này không phải là một file vật lý mà nó chỉ được chứa trong Docker.

Một image bao gồm hệ điều hành (Windows, CentOS, Ubuntu, …) và các môi trường lập trình được cài sẵn (httpd, mysqld, nginx, python, git, …).

Docker hub là nơi lưu giữ và chia sẻ các file images này (hiện có khoảng 300.000 images)

Bạn có thể tìm tải các image mọi người chia sẻ sẵn trên mạng hoặc có thể tự tạo cho mình một cái image như ý.

## Các câu lệnh trong Docker

Pull một image từ Docker Hub

`sudo docker pull image_name`

Tạo mới container bằng cách chạy image, kèm theo các tùy chọn:

`sudo docker run -v <forder_in_computer>:<forder_in_container> -p <port_in_computer>:<port_in_container> -it <image_name> /bin/bash`

Ví dụ:

`sudo docker pull ubuntu:16.04`

`sudo docker run -it ubuntu:16.04 /bin/bash`

Bây giờ bạn đã dựng thành công một môi trường ubuntu ảo rồi đó.

`docker images`: Liệt kê các images hiện có

`docker rmi {image_id/name}`: Xóa một image

`docker ps`: Liệt kê các container đang chạy

`docker ps -a`: Liệt kê các container đã tắt

`docker rm -f {container_id/name}`: Xóa một container

`docker start {new_container_name}`: Khởi động một container

`docker exec -it {new_container_name} /bin/bash`: Truy cập vào container đang chạy



