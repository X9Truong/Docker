## Namespaces , Cgroup
<img src="/img/9.png">

### 1. Namespaces

* Namespaces: Là feature trong Kernel Linux, hỗ trợ cho công nghệ container cung cấp isolated secure environment. Docker sử dụng công nghệ Linux namespaces cho isolation, process namespaces ... Đối với network docker sử dụng công nghệ Linux network namespaces,mỗi containers có một network namespace ( địa chỉ IP, bảng định tuyến ...).các process chạy trong một container không thể nhìn thấy và thậm chí ít ảnh hưởng hơn đến các process đang chạy trong một container khác hoặc trong hệ thống máy chủ.

- Mỗi containers có một network stack: Có nghĩa là containers không có quyền truy cập vào sockets hoặc interfaces của container khác. Tuy nhiên, nếu hệ thống máy chủ được thiết lập phù hợp các container có thể tương tác với nhau thông qua network interfaces tương ứng giống như chúng có thể tương tác với server bên ngoài.

* Từ Linux kernel 2.6.24 Linux hỗ trợ có 6 namespace:
<ul>

- Process ID : Cung cấp sự isolated  để phân bổ các process identifiers  (PID), danh sách các process và chi tiết của chúng. Mặc dù các namespaces mới được isolated với các namespace khác, các process trong namespaces mới vẫn thấy tất cả các process mặc dù các PID khác nhau.

- IPC (Inter process communication): Namespace cô lập các System V inter-process với các namespace khác.

- User (currently experimental support for): Namespace cô lập user IDs với các namespace khác.

- UTS: Namespace chấp nhận thay đổi tên hostname

- Network : Cho phép cô lập môi trường mạng network trong một host. Namespace phân chia việc sử dụng các khác niệm liên quan tới network như devices, địa chỉ addresses, ports, định tuyến và các quy tắc tường lửa vào trong một hộp (box) riêng biệt, chủ yếu là ảo hóa mạng trong một máy chạy một kernel duy nhất.

- Mount: Namespace cho phép tạo file system layout khác nhau, hoặc tạo các điểm truy cập read-only.
</ul>

``` sh

       Namespace   Constant          Isolates
       Cgroup      CLONE_NEWCGROUP   Cgroup root directory
       IPC         CLONE_NEWIPC      System V IPC, POSIX message queues
       Network     CLONE_NEWNET      Network devices, stacks, ports, etc.
       Mount       CLONE_NEWNS       Mount points
       PID         CLONE_NEWPID      Process IDs
       User        CLONE_NEWUSER     User and group IDs
       UTS         CLONE_NEWUTS      Hostname and NIS domain name
```

- Các process chạy inside namespaces chỉ tương tác được với các process bên trong namespace đó và không thể tương tác outside cũng như namespace khác (container khác).

### 2.Cgroup (Control groups)

+ Common control groups

<ul>

* CPU

* Memory

* Network Bandwidth

* Disk

* Priority

</ul>

- Cgroup là 1 thành phần quan trọng trong Linux Containers,cgroup thực hiện tính toán tài nguyên và giới hạn sử dụng. Cgroup cung cấp nhiều số liệu metric hữu ích, đảm bảo mỗi containers đều được chia sẻ RAM,CPU,diskI/O và quan trọng hơn một container không thể làm giảm hiệu suất của hệ thống bằng cách sử dụng hết tài nguyên.

- Vì vậy, trong khi chúng không đóng vai trò ngăn chặn một container truy cập hoặc ảnh hưởng đến dữ liệu và quy trình của một container khác, thì chúng rất cần thiết để chống lại một số cuộc tấn công từ chối dịch vụ. Chúng đặc biệt quan trọng trên các nền tảng nhiều người thuê, như PaaS công cộng và riêng tư, để đảm bảo thời gian hoạt động (và hiệu suất) nhất quán ngay cả khi một số ứng dụng bắt đầu hoạt động sai.



