# Bài 08 — Build, artifact và deploy

## Mục tiêu

Thiết kế đường từ code đã kiểm tra đến môi trường chạy, bắt đầu ở staging và có thể xác minh kết quả cũng như quay lui khi cần.

## Khái niệm

- **Build artifact:** đầu ra được tạo từ một phiên bản code, có thể lưu và chuyển sang bước triển khai.
- **Environment:** môi trường như development, staging hoặc production, thường có cấu hình và quyền riêng.
- **Smoke test:** kiểm tra nhanh sau deploy để xác nhận dịch vụ cơ bản hoạt động.
- **Rollback:** quay về phiên bản đã biết là tốt hoặc khôi phục trạng thái dịch vụ.

## Những quyết định cần có trước khi viết deploy

- Ứng dụng chạy ở đâu và deployment mechanism là gì?
- Bản build được tạo khi nào, lưu bao lâu và deploy có dùng đúng artifact đó không?
- Deploy kích hoạt khi nào: merge, tag/release hay hành động thủ công?
- Credentials được cấp ở đâu và job nào có thể đọc?
- Ai phê duyệt production và làm sao xác nhận deploy thành công?
- Cách quay lui ứng dụng và database migration là gì?

## Thực hành

1. Chọn hosting/runtime và đọc quy trình deploy chính thức của nền tảng.
2. Đóng gói ứng dụng thành artifact/container theo yêu cầu thực tế.
3. Triển khai vào staging bằng credentials riêng, hạn chế quyền và dữ liệu giả.
4. Chạy smoke test sau deploy và lưu log đủ để điều tra.
5. Thực hành quay về phiên bản trước trên staging.
6. Chỉ sau đó mới thiết kế production với phê duyệt và secret/environment tách biệt.
7. Với migration, cân nhắc thứ tự tương thích: schema mới có thể cùng tồn tại tạm thời với phiên bản ứng dụng trước không?

## Lưu ý

Không có quy trình deploy chung phù hợp mọi nền tảng. Tránh đặt secret production ở cấp repository nếu chỉ một environment cần dùng. Thay đổi database có thể không thể rollback bằng cách đơn giản; cần kế hoạch backup/forward-fix và kiểm tra tương thích.

## Câu hỏi tự kiểm tra

- Vì sao staging hữu ích trước production?
- Artifact giúp bảo đảm điều gì giữa build và deploy?
- Smoke test xác nhận được gì và không xác nhận được gì?

## Hoàn thành khi

Bạn có thể deploy phiên bản xác định lên staging, xác nhận dịch vụ sau deploy, và thực hiện một phương án khôi phục đã thử.
