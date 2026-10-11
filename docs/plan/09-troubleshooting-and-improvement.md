# Bài 09 — Đọc lỗi và cải tiến pipeline

## Mục tiêu

Điều tra lỗi từ bằng chứng trong log, phân biệt lỗi code với lỗi môi trường/workflow, và cải tiến pipeline mà vẫn giữ độ tin cậy.

## Quy trình điều tra

1. Xác định workflow, job và step thất bại; đọc phần log đầu tiên có lỗi gốc, không chỉ dòng kết thúc.
2. Ghi commit, branch, event, phiên bản runtime và cấu hình liên quan.
3. So sánh lệnh CI với lệnh chạy cục bộ; tái hiện trong môi trường sạch nếu có thể.
4. Phân loại: lỗi code/test, dependency, cấu hình, quyền/secret, dịch vụ ngoài, timeout hay runner.
5. Sửa nguyên nhân, chạy lại bước liên quan cục bộ và tạo PR để kiểm tra toàn pipeline.
6. Nếu lỗi tạm thời, xác nhận bằng chứng trước khi retry; ghi nhận nếu cần cải thiện khả năng phục hồi.

## Đo lường và tối ưu

- Theo dõi thời gian pipeline, tần suất lỗi và thời gian chờ runner.
- Chỉ thêm cache khi đo được bottleneck; cache sai key có thể gây kết quả khó tái hiện.
- Chạy job độc lập song song khi tài nguyên và thứ tự cho phép.
- Dùng matrix khi cần kiểm tra nhiều phiên bản/hệ điều hành có liên quan, tránh tăng ma trận không cần thiết.
- Tách smoke/integration test dài khỏi kiểm tra nhanh nếu điều đó cải thiện phản hồi mà không làm giảm bảo vệ cần thiết.

## Thực hành

1. Tạo PR làm một check thất bại có chủ ý.
2. Tìm nguyên nhân trong log và sửa lỗi.
3. Ghi lại thời gian của pipeline và bước chậm nhất.
4. Đề xuất một tối ưu có thể đo được, thực hiện rồi so sánh trước/sau.
5. Kiểm tra rằng tối ưu không bỏ qua hoặc làm yếu check.

## Câu hỏi tự kiểm tra

- Lỗi xuất hiện ở đâu trong log và điều gì chứng minh nguyên nhân?
- Vì sao retry không phải cách sửa cho mọi lỗi?
- Cần đo gì trước khi thêm cache hoặc chạy song song?

## Hoàn thành khi

Bạn có thể điều tra một CI failure từ log đến nguyên nhân, tái hiện/sửa lỗi, và đánh giá một thay đổi hiệu năng bằng số đo.
