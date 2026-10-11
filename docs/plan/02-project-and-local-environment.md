# Bài 02 — Chuẩn bị ứng dụng và môi trường cục bộ

## Mục tiêu

Tạo một ứng dụng nhỏ có thể cài, chạy và kiểm tra theo hướng dẫn nhất quán. Trước khi tự động hóa, bạn cần biết chính xác các lệnh thủ công đang làm gì.

## Khái niệm

- **Runtime:** môi trường thực thi ứng dụng, ví dụ phiên bản Node.js.
- **Package manager:** công cụ cài và quản lý dependency, ví dụ npm, pnpm hoặc Yarn.
- **Dependency:** thư viện mà dự án cần để phát triển hoặc chạy.
- **Lockfile:** ghi lại phiên bản dependency đã phân giải để các lần cài có kết quả nhất quán.
- **Environment:** cấu hình và dịch vụ mà ứng dụng cần khi chạy.

## Thực hành

1. Chọn runtime và package manager, ghi phiên bản vào tài liệu hoặc cấu hình dự án.
2. Tạo ứng dụng mẫu tối thiểu và thêm một hướng dẫn cài/chạy.
3. Commit manifest và lockfile phù hợp với package manager đã chọn.
4. Cài dependency từ trạng thái sạch theo hướng dẫn chính thức của package manager.
5. Chạy ứng dụng và ghi lại kết quả mong đợi.
6. Tách cấu hình nhạy cảm khỏi code; cung cấp file mẫu như `.env.example` chỉ chứa tên biến và giá trị giả an toàn nếu cần.

## Lưu ý

Không trộn nhiều package manager/lockfile nếu không có lý do. CI nên dùng lệnh cài đặt dựa trên lockfile ở chế độ CI/frozen tương ứng, thay vì tự cập nhật phiên bản trong lúc build.

Hạn chế thêm dịch vụ bên ngoài ở giai đoạn đầu. Mục tiêu là tạo nền tảng có thể tái hiện trên máy khác trước khi thêm database hoặc hosting.

## Câu hỏi tự kiểm tra

- Lockfile giải quyết vấn đề gì?
- Vì sao CI cần cài dependency giống cách nhóm phát triển cài?
- File `.env.example` có nên chứa secret thật không?

## Hoàn thành khi

Một người khác có thể làm theo hướng dẫn để cài và chạy ứng dụng mẫu, và bạn biết phiên bản runtime/package manager nào đang được dùng.
