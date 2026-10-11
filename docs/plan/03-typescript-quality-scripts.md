# Bài 03 — Scripts kiểm tra cho TypeScript

## Mục tiêu

Phân biệt các loại kiểm tra và tạo những lệnh có thể chạy cục bộ, có mã thoát thành công/thất bại rõ ràng để CI gọi lại.

## Các kiểm tra

| Kiểm tra | Phát hiện loại vấn đề nào? | Không thay thế cho |
| --- | --- | --- |
| Typecheck | Lỗi kiểu theo cấu hình TypeScript | Test hành vi hoặc lỗi runtime |
| Lint | Vi phạm quy tắc code và một số lỗi phổ biến | Đánh giá logic nghiệp vụ |
| Format check | File chưa theo định dạng thống nhất | Lint hay test |
| Test | Hành vi không đúng với kỳ vọng đã viết | Bao phủ mọi trường hợp |
| Build | Không tạo được đầu ra chạy/phát hành | Kiểm thử chất lượng đầu ra trên production |

## Thực hành

1. Chọn công cụ dựa trên ứng dụng và tạo cấu hình tối thiểu có chủ đích.
2. Định nghĩa scripts dễ hiểu trong manifest dự án (thường là `package.json` cho Node.js).
3. Bảo đảm lệnh kiểm tra trả exit code khác 0 khi có lỗi; CI dựa vào điều này để đánh dấu job thất bại.
4. Chạy từng script riêng, sửa lỗi và ghi lại một ví dụ lỗi điển hình.
5. Tạo một lỗi có chủ ý cho từng loại kiểm tra để chắc rằng script phát hiện được nó.
6. Thêm hướng dẫn cục bộ: lệnh chạy, điều kiện cần và cách sửa lỗi thường gặp.

## Thứ tự thực hành gợi ý

Chạy các kiểm tra nhanh trước (format check, lint, typecheck), sau đó test và build. Thứ tự trong pipeline còn tùy dependency giữa các lệnh; cần ưu tiên tốc độ phản hồi mà vẫn giữ kết quả đáng tin cậy.

## Lưu ý

- Không đặt tên script khiến người đọc hiểu nhầm: ví dụ lint không đồng nghĩa với format.
- Tránh lệnh chỉ chạy được trên máy của một người do phụ thuộc file chưa commit hoặc trạng thái cũ.
- Không bỏ qua test thất bại bằng `|| true` hay cấu hình tương tự.
- Có thể thêm một lệnh tổng hợp sau khi các lệnh thành phần đã hiểu rõ; vẫn nên giữ khả năng chạy riêng từng bước.

## Câu hỏi tự kiểm tra

- Typecheck có chạy ứng dụng không?
- Build thành công có chứng minh tính năng đúng không?
- Exit code có vai trò gì trong CI?

## Hoàn thành khi

Bạn chạy riêng được từng script, chứng minh được một lỗi phù hợp bị phát hiện, và giải thích được phạm vi cũng như giới hạn của từng kiểm tra.
