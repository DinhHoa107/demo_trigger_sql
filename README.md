# demo_trigger_sql
bai tap ve nha so 5 mssv k225480106088 Ta Pham Dinh Hoa mon He Quan Tri Co So Du Lieu
# BÀI TẬP VỀ NHÀ 05, Môn Hệ quản trị csdl.

SUBJECT: Trigger on mssql

# A. Trình bày lại đầu bài của đồ án PT&TKHT:
1. Mô tả bài toán của đồ án PT&TKHT, 
   đưa ra yêu cầu của bài toán đó
2. Cơ sở dữ liệu của Đồ án PT&TKHT :
   Có database với các bảng dữ liệu cần thiết (3nf),
   Các bảng này đã có PK, FK, CK cần thiết
 
# B. Nội dung Bài tập 05:
1. Dựa trên cơ sở là csdl của Đồ án
2. Tìm cách bổ xung thêm 1 (hoặc vài) trường phi chuẩn
   (là trường tính toán đc, nhưng thêm vào thì ok hơn,
    ok hơn theo 1 logic nào đó, vd ok hơn về speed)
   => Nêu rõ logic này!
3. Viết trigger cho 1 bảng nào đó, 
   mà có sử dụng trường phi chuẩn này,
   nhằm đạt được 1 vài mục tiêu nào đó.
   => Nêu rõ các mục tiêu 
4. Nhập dữ liệu có kiểm soát, 
   nhằm để test sự hiệu quả của việc trigger auto run.
5. Kết luận về Trigger đã giúp gì cho đồ án của em.

bài làm: 
# A. Trình bày lại đầu bài của đồ án PT&TKHT:
Mô tả bài toán của đồ án PT&TKHT, đưa ra yêu cầu của bài toán đó
Mô tả bài toán
Hiện nay, nhiều tiệm cầm đồ đang quản lý hoạt động kinh doanh một cách thủ công bằng sổ sách hoặc các công cụ đơn giản như Excel, dẫn đến việc xử lý dữ liệu mất thời gian, dễ xảy ra sai sót và khó kiểm soát hiệu quả hoạt động.

Một hệ thống quản lý tiệm cầm đồ sẽ giúp tự động hóa quá trình ghi nhận thông tin khách hàng, tài sản cầm cố, hợp đồng, lãi suất, thanh lý và các khoản thanh toán. Điều này không chỉ giúp tiết kiệm thời gian, giảm thiểu sai sót mà còn nâng cao hiệu quả quản lý và dịch vụ khách hàng.

2. Yêu cầu của bài toán
2.1. Yêu cầu chức năng
Hệ thống cần đáp ứng các chức năng chính sau:

Quản lý khách hàng:

Thêm/sửa/xoá thông tin khách hàng.

Tra cứu thông tin khách hàng theo tên, CMND/CCCD, số điện thoại,…

Quản lý tài sản cầm cố:

Ghi nhận thông tin tài sản: loại tài sản, mô tả, tình trạng, hình ảnh…

Gắn tài sản với hợp đồng cầm cố cụ thể.

Quản lý hợp đồng cầm đồ:

Tạo hợp đồng mới: thông tin khách hàng, tài sản, số tiền cho vay, lãi suất, thời hạn, ngày bắt đầu.

Cập nhật tình trạng hợp đồng: còn hiệu lực, quá hạn, đã thanh lý, đã gia hạn…

Tính lãi theo thời gian thực.

Thanh toán & gia hạn hợp đồng:

Ghi nhận thông tin thanh toán (trả gốc, trả lãi).

Hỗ trợ gia hạn hợp đồng, cập nhật thời hạn và lãi suất.

Quản lý thanh lý tài sản:

Danh sách tài sản quá hạn, chưa chuộc.

Ghi nhận thông tin thanh lý: ngày bán, giá bán, người mua…

Thống kê - Báo cáo:

Báo cáo tổng hợp số lượng hợp đồng đang hoạt động, đã kết thúc, quá hạn.

Báo cáo doanh thu theo ngày/tháng/năm.

Thống kê tài sản theo loại, tình trạng.

# 2 cơ sở dữ liệu 
bảng khách hàng 
![image](https://github.com/user-attachments/assets/66b9c79e-16dd-485c-aa97-9ab8fce124e0)

bảng tài sản 
![image](https://github.com/user-attachments/assets/fe2ea885-12f9-487e-a57b-3f4493f9e7d3)

bảng thanh lý
![image](https://github.com/user-attachments/assets/3b2c9445-167b-486c-8106-dfa1e56f480f)

bảng thanh toán 
![image](https://github.com/user-attachments/assets/18ee4f58-fd38-4898-8b4e-a4fbd7637eb4)

bảng hợp đồng 
![image](https://github.com/user-attachments/assets/995f2b02-2fac-426b-8da5-75672659dad6)

bảng diagram 
![image](https://github.com/user-attachments/assets/78273a12-306a-440b-90b8-5d93a616c832)


# B. Nội dung Bài tập 05:
1. Dựa trên cơ sở là csdl của Đồ án
2. Tìm cách bổ xung thêm 1 (hoặc vài) trường phi chuẩn
   (là trường tính toán đc, nhưng thêm vào thì ok hơn,
    ok hơn theo 1 logic nào đó, vd ok hơn về speed)
   => Nêu rõ logic này!
3. Viết trigger cho 1 bảng nào đó, 
   mà có sử dụng trường phi chuẩn này,
   nhằm đạt được 1 vài mục tiêu nào đó.
   => Nêu rõ các mục tiêu 
4. Nhập dữ liệu có kiểm soát, 
   nhằm để test sự hiệu quả của việc trigger auto run.
5. Kết luận về Trigger đã giúp gì cho đồ án của em.
# 2 bổ sung trường phi cuẩn 
bổ sung trường phi chuẩn tiền lãi dự kiến
![image](https://github.com/user-attachments/assets/5b94b4fa-75fb-459c-9c69-f612dbd39b45)
thêm bảng log 
![image](https://github.com/user-attachments/assets/935054d7-19e0-450b-a2f9-8f2769bee554)

# 3 viết câu lệnh trigger cho bảng hợp đồng tính tiền lãi dự kiến
![image](https://github.com/user-attachments/assets/0cadd14a-7434-4986-8b5a-46e9f902907f)

# 4 nhập dữ liệu có kiểm soát
![image](https://github.com/user-attachments/assets/d882a747-cf99-4643-b8a5-d6382f334052)

# kết quả 
![image](https://github.com/user-attachments/assets/2731733c-6aba-485a-bd1e-e3e1a98fc7c9)

# 5 kết luận 
Giảm thiểu lỗi tính tay TienLaiDuKien

Tự động hoá quy trình nhập liệu

Giúp thống kê nhanh chóng và tối ưu hiệu năng

Có thể mở rộng cho tính năng khác (ghi Log, cảnh báo quá hạn...)













