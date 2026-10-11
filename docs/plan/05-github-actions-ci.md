# Bài 05 — CI với GitHub Actions

## Mục tiêu

Tự động chạy các script đã kiểm chứng trên Pull Request và hiểu workflow được kích hoạt, thực thi, cấp quyền và báo kết quả như thế nào.

## Khái niệm

- **Workflow:** file YAML mô tả quy trình tự động, thường lưu dưới `.github/workflows/`.
- **Event/trigger:** sự kiện khởi chạy workflow, ví dụ mở hoặc cập nhật PR.
- **Runner:** máy chạy workflow.
- **Job:** nhóm bước chạy trên runner; job có thể chạy song song nếu không phụ thuộc nhau.
- **Step:** một hành động hoặc lệnh trong job.
- **Status check:** kết quả hiển thị trên PR và có thể được Ruleset yêu cầu.

## Thực hành

1. Tạo workflow tối thiểu chạy khi mở/cập nhật PR và khi push lên nhánh chính.
2. Chọn runner và phiên bản runtime rõ ràng.
3. Checkout code, cài dependency từ lockfile, rồi gọi đúng các scripts đã chạy cục bộ.
4. Đặt tên workflow/job ổn định, dễ nhận diện và phù hợp tên check cần bảo vệ.
5. Mở PR thay đổi nhỏ, theo dõi trạng thái check và xem log.
6. Tạo lỗi có chủ ý để xác nhận PR báo thất bại; sửa lỗi và xác nhận check chạy lại thành công.

## Đọc một workflow theo thứ tự

Xác định event → permissions → runner → thiết lập runtime → cài dependencies → lệnh kiểm tra → điều kiện phụ thuộc. Mỗi job nên có mục tiêu rõ ràng; các lệnh không liên quan không cần bị gộp chỉ để file ngắn hơn.

## Lưu ý

- Workflow phải cài đúng dependencies; không dựa vào file đã có sẵn trên runner.
- Cache giúp giảm thời gian cài đặt nhưng không nên là điều kiện để build thành công.
- Tách deploy khỏi PR workflow nếu PR từ fork hoặc code chưa tin cậy có thể tiếp cận credentials.
- Không in environment variables hoặc secret ra log.
- Đặt quyền `GITHUB_TOKEN` tối thiểu cần thiết; workflow chỉ kiểm tra code thường không cần quyền ghi.

## Câu hỏi tự kiểm tra

- Workflow, job, step và runner khác nhau thế nào?
- Status check lấy tên từ đâu và vì sao tên ổn định quan trọng?
- Nếu workflow chạy trên máy cá nhân thành công nhưng CI lỗi, cần so sánh điều gì?

## Hoàn thành khi

PR mới tự chạy các kiểm tra đã chọn, lỗi có thể tái hiện qua log, và bạn giải thích được từng phần chính của workflow.
