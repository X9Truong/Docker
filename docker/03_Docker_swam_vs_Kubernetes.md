## Docker Swarm vs Kubernetes

- Khi số lượng container tăng lên, việc quản lý, triển khai, scale trở nên phức tạp, không thể hì hục chạy bằng tay được thì chúng ta nhắc đến Docker Swarm hay Kubernetes, thực sự thì so sánh hai khái niệm này chưa hẳn chính xác bởi chúng không "ngồi chung một mâm" nhưng cơ bản thì như sau.

<img src="/img/2.png">

* Tổng quan về Kubernetes

Dựa theo website của Kubernetes thì chúng được định nghĩ như sau: 

*“Kubernetes is an open-source system for automating deployment, scaling, and management of containerized applications.”*

*Kubernetes là một hệ thống mã nguồn mở để tự động triển khai, scaling, quản lý các container. Kubernetes được xây dựng bởi Google dựa trên kinh nghiệm quản lý sử dụng các container trong khi triển khai một hệ thống quản lý gọi là Borg ( nhiều lúc gọi là Omega)*

<img src="/img/3.png">

* Như bạn thấy từ hình trên, có một số thành phần liên kết cluster Kubernetes. Các node đặt khối lượng công việc vào user pod. Các thành phần khác bao gồm:

* Etcd: Khối này lưu trữ dữ liệu cấu hình có thể được truy cập bởi Máy chủ API Kubernetes Master bằng API đơn giản hoặc HTTP JSON.

* API Server: Khối này là trung tâm quản lý các node chính Kubernetes. Nó tạo điều kiện giao tiếp giữa các khối khác nhau, từ đó duy trì hoạt động cluster.

* Controller Manager: Khối này đảm bảo trạng thái mong muốn của cluster "matches" với trạng thái hiện tại bằng cách scaling khối lượng công việc.

* Scheduler: Khối này đưa khối lượng công việc vào trong các node thích hợp - trong trường hợp tất cả công việc đặt trên host của bạn.

Danh sách dưới đây là những thuật ngữ liên quan khác với Kubernetes:

* Pod: Kubernetes triển khai và lên kế hoạch các container trong nhóm gọi là Pod. Các container trong pod chạy trong cùng node và chia sẻ tài nguyên như filesystems, kernel, và địa chỉ IP.

* Deployments: Các khối xây dựng này có thể được sử dụng để tạo và quản lý một nhóm của pod. Deployments có thể được sử dụng với tầng dịch vụ để scaling hoặc đảm bảo tính khả dụng.

* Services: Services là các điểm cuối có thể được xử lý theo tên và có thể được kết nối tới pod sử dụng label selectors. Sevice này sẽ yêu cầu round-robin tự động giữa các pods. Kubernetes sẽ thiết lập một máy chủ DNS cho cluter được coi như service mới và cho phép chúng xử lý thông qua tên.

* Labels: Labels là cặp khóa-giá trị gắn liền với đối tượng và có thể được sử dụng để tìm kiếm và cập nhật nhiều đối tượng như một bộ duy nhất.


