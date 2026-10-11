# Bài 07 — Bảo mật và độ tin cậy

## Mục tiêu

Nhận diện các đường rò rỉ credentials và giảm quyền của workflow, đồng thời hiểu cách cập nhật dependencies mà không làm pipeline mất tính lặp lại.

## Nội dung

### Secrets và quyền

- Lưu secret trong GitHub Secrets/Environment hoặc secret manager được chọn, không trong source, workflow literal, log hay artifact công khai.
- Cấp quyền `GITHUB_TOKEN` theo nguyên tắc tối thiểu; tách job cần quyền ghi khỏi job chỉ chạy test.
- Dùng environment protection/approval cho thao tác nhạy cảm nếu nền tảng và loại tài khoản hỗ trợ.
- Không cấp secret production cho workflow chạy code từ fork hoặc nguồn chưa tin cậy.

### Actions và dependency

- Ưu tiên action đáng tin cậy, kiểm tra nguồn và quyền mà action yêu cầu.
- Cân nhắc pin action theo commit SHA để cố định nội dung thực thi; cần có quy trình cập nhật SHA để nhận bản vá.
- Dùng lockfile và cập nhật dependency có review.
- Bật cảnh báo/công cụ cập nhật tự động khi phù hợp, nhưng vẫn review thay đổi và chạy kiểm tra.

### Độ tin cậy

- Giữ CI có kết quả xác định: đầu vào, phiên bản và môi trường phải rõ.
- Giới hạn thời gian job và dọn tài nguyên tạm khi có database/service.
- Không cache dữ liệu nhạy cảm; xử lý cache như dữ liệu có thể bị lỗi thời.
- Với retry, chỉ retry lỗi tạm thời có lý do; retry mù có thể che lỗi thật.

## Thực hành

1. Kiểm tra quyền hiện tại trong từng workflow và giảm quyền không cần thiết.
2. Tìm credentials/endpoint nhạy cảm trong code, lịch sử hướng dẫn và output log mẫu.
3. Xác định những job nào nhận secret và vì sao.
4. Ghi quy trình xoay vòng secret khi nghi bị lộ.
5. Kiểm tra dependency update trong PR và xác nhận CI chạy lại.

## Câu hỏi tự kiểm tra

- Vì sao secrets của production không nên có mặt trong PR workflow?
- Pin action theo SHA giúp gì và tạo thêm trách nhiệm gì?
- Cache có được phép là điều kiện duy nhất để workflow thành công không?

## Hoàn thành khi

Bạn mô tả được quyền và secrets mỗi workflow/job cần, biết cách giảm quyền thừa, và có quy trình review cập nhật dependency.
