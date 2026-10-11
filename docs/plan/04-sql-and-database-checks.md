# Bài 04 — SQL, schema và migration

## Mục tiêu

Hiểu rằng kiểm tra SQL gồm nhiều lớp, chọn được chiến lược phù hợp database, và chạy kiểm tra tích hợp mà không đụng đến dữ liệu production.

## Khái niệm

- **Schema:** cấu trúc database như bảng, cột, kiểu dữ liệu, ràng buộc và index.
- **Migration:** thay đổi schema được ghi lại theo phiên bản để áp dụng có thứ tự.
- **SQL lint:** kiểm tra quy tắc/cú pháp theo khả năng công cụ; không nhất thiết chạy câu lệnh trên database thật.
- **Integration test:** kiểm tra nhiều thành phần cùng hoạt động, chẳng hạn ứng dụng truy vấn database.
- **Ephemeral database:** database tạm dành riêng cho một lần chạy test, sau đó bị hủy.

## Các lớp kiểm tra có thể cần

1. Lint/format SQL để phát hiện vấn đề trình bày và một số lỗi tĩnh.
2. Kiểm tra migration từ trạng thái schema sạch.
3. Kiểm tra nâng cấp từ phiên bản schema trước nếu sản phẩm cần hỗ trợ đường nâng cấp.
4. Chạy test truy vấn/integration trên database đúng loại và phiên bản phù hợp.
5. Kiểm tra seed/test data chỉ chứa dữ liệu giả.

## Thực hành

1. Chọn hệ quản trị database và ghi phiên bản mục tiêu.
2. Chọn cách quản lý schema/migration theo framework hoặc công cụ dự án.
3. Viết một migration nhỏ, áp dụng lên database thử nghiệm sạch và xác minh schema.
4. Viết test kiểm tra một hành vi truy vấn có ý nghĩa.
5. Xác nhận test có thể chạy lặp lại và dọn database sau khi hoàn tất.
6. Ghi rõ biến môi trường cần thiết và cung cấp giá trị giả an toàn cho hướng dẫn.

## Lưu ý

SQLite, PostgreSQL, MySQL và các hệ khác có khác biệt cú pháp, kiểu dữ liệu và hành vi transaction. Chỉ chạy SQLite để kiểm tra PostgreSQL có thể bỏ sót lỗi tương thích. Dùng database cùng họ/phiên bản với production khi cần kiểm chứng hành vi thật.

Migration có thể gây mất dữ liệu hoặc downtime. Trước khi áp dụng vào production cần biết cách backup, kiểm tra tương thích giữa phiên bản ứng dụng/schema và phương án khôi phục.

## Câu hỏi tự kiểm tra

- SQL lint chứng minh được điều gì và không chứng minh được điều gì?
- Vì sao test cần database riêng và dữ liệu giả?
- Tại sao migration production cần được xem xét như thay đổi ứng dụng?

## Hoàn thành khi

Bạn có thể chạy migration và test database trên môi trường cô lập, xác minh kết quả, và giải thích vì sao không dùng database production trong CI.
