# Bài 00 — Bắt đầu và xác định mục tiêu

## Mục tiêu

Sau bài này, bạn giải thích được CI và CD ở mức cơ bản, mô tả đường đi từ thay đổi code đến deploy, và biết repo đang cần quyết định gì trước khi viết cấu hình.

## Khái niệm

- **CI (Continuous Integration):** tự động chạy các kiểm tra trên thay đổi code để phát hiện vấn đề sớm.
- **Continuous Delivery:** luôn giữ phần mềm ở trạng thái có thể phát hành; việc phát hành production thường cần một hành động hoặc phê duyệt.
- **Continuous Deployment:** thay đổi vượt qua các điều kiện đã định sẽ tự động được đưa lên production.
- **Pipeline:** chuỗi bước tự động, chẳng hạn cài dependency → lint → test → build.

CI không đảm bảo ứng dụng không có lỗi. Nó chỉ tự động hóa những điều kiện kiểm tra đã thiết kế.

## Luồng cần nắm

`thay đổi code → commit/branch → Pull Request → checks → review → merge → build/release → deploy → kiểm tra sau deploy`

Mỗi bước có thể thất bại. Pipeline tốt báo lỗi ở bước gần với nguyên nhân và cung cấp log đủ để điều tra.

## Việc cần làm

1. Đọc README ở thư mục gốc và xác nhận repo hiện chưa có ứng dụng hay công nghệ đã chọn.
2. Chọn một ứng dụng mẫu để thực hành. Có thể bắt đầu bằng ứng dụng Node.js/TypeScript nhỏ, không cần dịch vụ bên ngoài.
3. Ghi lại mục tiêu ứng dụng, runtime, package manager, cách chạy, và điều kiện tối thiểu để chấp nhận một thay đổi.
4. Nếu muốn học SQL, ghi rõ sẽ dùng loại database nào. Cú pháp, migration và cách chạy database phụ thuộc hệ quản trị.
5. Vẽ luồng hiện tại trên giấy, kể cả khi mọi bước đều đang làm thủ công.

## Câu hỏi tự kiểm tra

- CI chạy khi nào và chạy ở đâu?
- Khác nhau giữa Continuous Delivery và Continuous Deployment là gì?
- Kiểm tra nào nên chạy trước khi cho phép merge?
- Vì sao chưa nên viết workflow trước khi biết lệnh kiểm tra của ứng dụng?

## Hoàn thành khi

Bạn có thể mô tả mục tiêu ứng dụng mẫu và liệt kê các quyết định còn thiếu: stack, database (nếu có), nơi chạy ứng dụng và cách xác định một bản deploy thành công.
