# Bài 06 — GitHub Rulesets

## Mục tiêu

Thiết lập chính sách bảo vệ nhánh phù hợp để thay đổi vào nhánh chính đi qua PR và các status checks bắt buộc.

## Ruleset là gì?

Ruleset là cấu hình trên GitHub để áp dụng quy tắc cho nhánh hoặc tag. Nó khác file workflow trong repository: workflow tạo ra checks; Ruleset quyết định checks nào phải đạt trước khi cho phép cập nhật nhánh.

Tên menu và lựa chọn có thể thay đổi theo GitHub, loại tài khoản, quyền truy cập và cấp repository/organization. Cần kiểm tra giao diện hiện tại khi thực hành.

## Các quy tắc thường gặp

- Áp dụng cho nhánh mặc định (ví dụ `main`) hoặc mẫu nhánh cụ thể.
- Yêu cầu Pull Request trước khi merge.
- Yêu cầu một hoặc nhiều approvals nếu quy trình review cần.
- Yêu cầu status checks thành công, chọn đúng checks đã xuất hiện từ workflow.
- Hạn chế force-push hoặc xóa nhánh được bảo vệ.
- Quy định ai/ứng dụng nào có thể bypass; giới hạn bypass thật cẩn thận.

## Thực hành

1. Xác nhận bạn có quyền quản lý Rulesets và xác định nhánh đích.
2. Kiểm tra workflow CI đã chạy thành công và status check đã xuất hiện trên PR.
3. Tạo Ruleset với phạm vi nhỏ, trước tiên chỉ áp dụng lên nhánh thử nghiệm nếu có thể.
4. Bật yêu cầu PR và chọn status checks tương ứng. Tránh chọn check chưa từng chạy hoặc tên không ổn định.
5. Thử merge PR khi check đang pending, thất bại và thành công để hiểu hành vi.
6. Xác nhận người quản trị vẫn có cách sửa cấu hình nếu tự khóa đường cập nhật.
7. Ghi lại các quy tắc đã bật, phạm vi áp dụng và bypass được cấp.

## Lưu ý

Ruleset không thay thế review có chất lượng. Yêu cầu review và status checks cần phản ánh mức độ rủi ro, quy mô nhóm và quyền tài khoản. Đừng cấp bypass rộng theo thói quen; quyền bypass làm thay đổi hiệu lực của quy tắc.

## Câu hỏi tự kiểm tra

- Workflow tạo ra điều gì mà Ruleset sử dụng?
- Vì sao nên chọn status check sau khi đã chạy workflow ít nhất một lần?
- Nếu check đổi tên, Ruleset có thể gặp vấn đề gì?

## Hoàn thành khi

PR vào nhánh được bảo vệ không thể merge nếu check bắt buộc chưa thành công, và bạn biết nơi xem phạm vi cùng bypass của Ruleset.
