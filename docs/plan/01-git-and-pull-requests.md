# Bài 01 — Git, branch và Pull Request

## Mục tiêu

Thực hiện được một thay đổi nhỏ trên branch riêng, mở Pull Request (PR), đọc diff và hiểu vì sao PR là điểm phù hợp để chạy CI.

## Khái niệm

- **Commit:** bản ghi một nhóm thay đổi trong lịch sử Git.
- **Branch:** dòng phát triển tách biệt để làm việc mà không sửa trực tiếp nhánh chính.
- **Pull Request:** đề xuất đưa thay đổi từ branch vào nhánh khác; nơi review và kiểm tra tự động được tập trung.
- **Diff:** phần thể hiện những dòng được thêm, sửa hoặc xóa.
- **Merge:** đưa lịch sử/thay đổi của PR vào nhánh đích.

## Thực hành

1. Tạo branch với tên mô tả thay đổi.
2. Thực hiện thay đổi nhỏ, kiểm tra `git status` và xem diff trước khi commit.
3. Commit với thông điệp nêu rõ mục đích.
4. Đẩy branch lên GitHub và mở PR vào nhánh chính.
5. Đọc diff trên GitHub, thêm mô tả và xử lý nhận xét.
6. Merge PR thử nghiệm sau khi đã review.

## Lưu ý

PR giúp chạy cùng bộ kiểm tra trước khi thay đổi vào nhánh chính. Branch protection/Ruleset mới là chính sách ngăn merge khi điều kiện chưa đạt; chỉ mở PR không tự đảm bảo chất lượng.

Không đưa file chứa token, mật khẩu, private key hay dữ liệu cá nhân vào commit. `.gitignore` ngăn một số file mới bị theo dõi nhưng không xóa secret đã commit khỏi lịch sử.

## Câu hỏi tự kiểm tra

- Vì sao làm việc trên branch riêng hữu ích?
- Diff giúp reviewer kiểm tra điều gì?
- Nếu commit nhầm secret, xóa file trong commit tiếp theo đã đủ chưa?

## Hoàn thành khi

Bạn mở và merge được một PR nhỏ, biết tìm diff và checks của PR, và giải thích được vì sao CI sẽ chạy trên PR.
