## Tổng quan về Docker Swarm

Docker Engine v1.12.0 và mới hơn cho phép lập trình viên triển khai container trong chế độ Swarm. Một Swarm cluster bao gồm Docker Engine được triển khai trên nhiều node. Node "Manager" thực hiện sắp xếp và quản lý cluster. Các node "Worker" nhận và thi hành nhiệm vụ từ node "manager". Mỗi service, có thể được khai báo, bao gồm nhiệm vụ có thể chạy trong Swarm node. Services có thể được sao chép để chạy trên nhiều node. Trong mô hình sao chép service, cân bằng tải nội bộ và DNS nội bộ có thể được sử dụng để cung cấp sẵn sàng các endpoint dịch vụ.

<img src="/img/4.png">

Kiến trúc Docker Swarm bao gồm các "manager" và các "worker". Người dùng có thể khai báo trạng thái mong muốn của nhiều service để chạy trong Swarm cluster sử dụng YAML files. Đây là vài thuật ngữ thông dụng liên quan đến Docker Swarm:

* Node: Một node là một thực thể của Swarm, các node có thể được phân phối tại chỗ hoặc trên cloud.

* Swarm: một cluster của các node. Trong chế độ Swarm, bạn sắp đặt các service, thay vì chạy các container bằng câu lệnh.

* Manager node: Là node nhận các định nghĩa service từ người dùng, và gửi công việc đến các node Worker. Node Manager có thể cũng thực hiện công việc của các node Worker.

* Worker node: là node nhận và chạy các nhiệm vụ từ node Manager.

* Service: Một service xác định images của container mà số lượng các bản lặp lại. Đây là một câu lệnh ví dụ sẽ được đặt trên 2 node có sẵn:

`docker service create --replicas 2 --name mynginx nginx`

* Task: một task là một nhiệm vụ của service trong một node worker.

## Kubernetes vs. Docker Swarm: Technical Capabilities


| <img src="/img/5.png"> | <img src="/img/6.png"> |
|:------------------------:|:------------------------:|
|Application Definition| |
|Ứng dụng có thể được triển khai sử dụng kết hợp các pods, deployments, and services. Một pod là một nhóm các container đồng nhất cùng vị trí và là đơn vị nhỏ nhất để triển khai. Deploysment có thể có nhiều bản sao trên nhiều node. Một service đại diện cho công việc container và tích hợp tới các DNS để round-robin yêu cầu gửi đến.|Ứng dụng có thể được triển khai dưới dạng services trong một Swarm cluster. Nhiều container sẽ được chỉ định bằng file YAML. Docker Compose có thể triển khai chúng. Task được phân phối qua các trung tâm dữ liệu qua việc sử dụng nhãn. Bạn có thể sử dụng nhiều tùy chọn vị trí để phân phối các task.|
|Application Scalability Constructs | |
|Mỗi tầng ứng dụng được định nghĩa như một pod, có thể được scaled khi quản lý bằng deployment, được chỉ định trong file YAML. Việc mở rộng có thể thực hiện thủ công hoặc tự động. Pod được sử dụng để tích hợp các ứng dụng như LAMP (Apache, MySQL, PHP) or ELK/Elastic (Elasticsearch, Logstash, Kibana)cùng vị trí và cùng quản lý ứng dụng như hệ thống quản lý nội dung và ứng dụng cho sao lưu, kiểm soát, …|Các services được scales bằng cách sử dụng Docker Composer với file YAML. Services có thể là toàn cục và sao chép. Services toàn cục chạy trên tất cả các node, các service sao chép chạy bản sao của service khác thông qua các nodes. Ví dụ, một node MySQL với 3 bản sao có thể chạy tối đa trên 3 node. Tasks có thể được scaled up hoặc scaled down, triển khai song song hoặc theo trình tự.|
|High Availability | |
|Deployments cho phép các pods được phân phối qua các node cung cấp tính khả dụng cao, do đó hạn chế các lỗi ứng dụng. Các dịch vụ cân bằng tải phát hiện các pod không khả dụng và xóa chúng. Tính khả dụng cao của Kubernetes được hỗ trợ. Nhiều node chính và node worker sẽ cân bằng tải cho các yêu cầu từ kubeclt và client, Etcd có thể được nhóm lại và các máy chủ API có thể được sao chép.|Các service có thể được nhân rộng trong các Swarm node, swarm manager chịu trách nhiệm toàn bộ các cluster và quản lý tài nguyên các node worker. Sử dụng cân bằng tải bên trong để đưa ra các service bên ngoài. Các nhà quản lý Swarm sử dụng thuật toán Raft Consensus để đảm bảo rằng họ có thông tin thích hợp.|
|Cân bằng tải | |
|Pod được giao tiếp thông qua một service, có thể được sử dụng như một cân bằng tải trong cluster. Thông thường, một Ingress (một đối tượng API quản lý việc truy cập bên ngoài vào dịch vụ bên trong Cluster, điển hình là HTTP) được sử dụng để cân bằng tải.| Trong chế độ Swarm có một thành phần DNS được sử dụng để phân phối các yêu cầu đến tên dịch vụ. Service có thể chạy trên các cổng do người dùng chỉ định hoặc có thể được chỉ định tự động.|
|Auto-scaling| |
|Auto-scaling bằng cách sử dụng một số pod đã định nghĩa khai báo bằng cách sử dụng Deployments.|Không trực tiếp, với mỗi dịch vụ, bạn có thể khai báo số tác vụ bạn muốn chạy. Khi bạn tự tăng hoặc giảm, Swarm manager tự động điều chỉnh bằng cách thêm hoặc xóa tác vụ.|
|Networking| |
|Mô hình mạng là một mạng lưới phẳng, cho phép tất cả các pod giao tiếp với nhau, các quy định mạng xác định cách mà các pod kết nối.	| Node tham gia vào một cụm Docker Swarm tạo ra một mạng che phủ cho các dịch vụ trải rộng tất cả các máy trong Swarm và một Docker bridge network cho container.|



	








