# Lộ trình học CI/CD

Lộ trình này đi từ kiểm tra thủ công trên máy cá nhân đến quy trình CI, bảo vệ Pull Request và deploy có kiểm soát. Học lần lượt; mỗi bài tạo nền cho bài tiếp theo. Thời lượng chỉ là ước lượng, có thể học theo tốc độ riêng.

## Cách học

1. Đọc mục tiêu và khái niệm của bài.
2. Thực hành trên nhánh riêng, chạy lệnh được nêu trong bài.
3. Tạo một thay đổi có chủ ý gây lỗi để quan sát công cụ phát hiện lỗi ra sao.
4. Hoàn thành tiêu chí cuối bài trước khi chuyển tiếp.
5. Ghi lại điều chưa hiểu hoặc log lỗi để làm đầu vào cho bài sau.

Các lệnh và cấu hình cụ thể sẽ được chốt theo ứng dụng mẫu, package manager, database và hosting đã chọn. Repo hiện chưa chứa ứng dụng, vì vậy các bài sau đây là kế hoạch học, không giả định rằng công cụ minh họa đã được cài đặt.

## Bản đồ bài học

| Bước | Bài học | Kết quả |
| --- | --- | --- |
| 00 | [Bắt đầu và xác định mục tiêu](./00-start-here.md) | Biết CI/CD giải quyết vấn đề nào và chọn phạm vi ứng dụng mẫu |
| 01 | [Git, branch và Pull Request](./01-git-and-pull-requests.md) | Thực hiện được luồng thay đổi qua Pull Request |
| 02 | [Chuẩn bị ứng dụng và môi trường](./02-project-and-local-environment.md) | Ứng dụng chạy nhất quán trên máy cá nhân |
| 03 | [Scripts kiểm tra cho TypeScript](./03-typescript-quality-scripts.md) | Có scripts rõ nghĩa cho typecheck, lint, format, test và build |
| 04 | [SQL, schema và migration](./04-sql-and-database-checks.md) | Biết cách kiểm tra SQL và database trong môi trường cô lập |
| 05 | [CI với GitHub Actions](./05-github-actions-ci.md) | Pull Request tự chạy các kiểm tra đã có |
| 06 | [GitHub Rulesets](./06-github-rulesets.md) | Nhánh chính được bảo vệ bằng PR và status checks |
| 07 | [Bảo mật và độ tin cậy](./07-security-and-reliability.md) | Workflow có quyền tối thiểu và dependency được quản lý |
| 08 | [Build, artifact và deploy](./08-build-and-deploy.md) | Có đường deploy staging/production và phương án khôi phục |
| 09 | [Đọc lỗi và cải tiến pipeline](./09-troubleshooting-and-improvement.md) | Có thể điều tra lỗi CI và cải thiện pipeline có căn cứ |

## Mốc hoàn thành

- **Nền tảng:** hoàn tất bài 00–02; biết tạo PR và chạy ứng dụng cục bộ.
- **Kiểm tra:** hoàn tất bài 03–04; các lệnh kiểm tra có thể chạy độc lập.
- **CI và bảo vệ:** hoàn tất bài 05–07; PR có checks và nhánh được bảo vệ phù hợp.
- **Phân phối:** hoàn tất bài 08–09; hiểu điều gì xảy ra từ lúc merge đến sau deploy.

## Quy tắc an toàn khi thực hành

- Không dùng credentials hoặc dữ liệu production trong bài tập.
- Không commit secret vào repository; nếu lỡ commit, thu hồi/thay secret ngay cả khi đã xóa khỏi file.
- Thử Ruleset trên repository thử nghiệm hoặc với phạm vi hẹp trước khi áp dụng cho dự án quan trọng.
- Chỉ bật deploy sau khi biết trigger, quyền truy cập, người phê duyệt và cách rollback.
