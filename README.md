# Học CI/CD từ số 0

> **Mục tiêu:** xây dựng một dự án thực hành giúp người mới hiểu cách kiểm tra mã nguồn tự động, bảo vệ nhánh GitHub và triển khai ứng dụng an toàn. Ta sẽ học từng bước, giải thích vì sao mỗi cấu hình tồn tại, thay vì chỉ chép một workflow có sẵn.

## CI/CD là gì?

- **CI (Continuous Integration – tích hợp liên tục):** mỗi thay đổi được tự động kiểm tra, ví dụ cài dependencies, typecheck, lint và chạy test.
- **CD (Continuous Delivery/Deployment – phân phối/triển khai liên tục):** chuẩn bị hoặc tự động đưa phiên bản đã qua kiểm tra đến môi trường chạy.

> Luồng tổng quát: viết code → tạo Pull Request → CI kiểm tra → review và merge → build/release → deploy → theo dõi.

## Ta sẽ học những gì?

1. **Nền tảng Git và GitHub:** branch, commit, Pull Request, checks, review và protection.
2. **GitHub Rulesets:** quy tắc cho branch/tag; yêu cầu Pull Request, review, status checks thành công; hạn chế force-push/xóa nhánh; tìm hiểu quyền bypass và cách thử nghiệm an toàn.
3. **Kiểm tra dự án TypeScript:** cài dependency, typecheck, lint, format check, unit test và build. Phân biệt mục đích của từng lệnh và thời điểm nên chạy.
4. **Kiểm tra SQL:** kiểm tra cú pháp/lint, quản lý migration, kiểm thử truy vấn và schema trên database dùng riêng cho CI; không kết nối dữ liệu production từ test.
5. **GitHub Actions:** workflow, event, job, step, runner, cache, artifacts, matrix và cách đọc log khi lỗi.
6. **Build và deploy:** artifact có thể tái lập, environments, secrets, staging/production, approval, smoke test, rollback và theo dõi sau triển khai.
7. **Bảo mật và độ tin cậy:** quyền tối thiểu của `GITHUB_TOKEN`, pin action, không ghi secrets vào log, dependency updates và xử lý lỗi.

## Kế hoạch học chi tiết

Lộ trình từng bài nằm trong [docs/plan/](docs/plan/README.md), gồm mục tiêu, khái niệm, bài thực hành và tiêu chí hoàn thành cho từng bước.

## Lộ trình thực hành

### Giai đoạn 1 — Xác định dự án cần kiểm tra

Trước khi viết YAML, ghi lại stack, phiên bản runtime, cách cài dependencies, các lệnh chạy được trên máy cá nhân, và điều kiện để gọi một thay đổi là đạt. CI nên tự động hóa các lệnh đáng tin cậy này.

### Giai đoạn 2 — Viết và hiểu các script kiểm tra

Ví dụ với dự án Node.js/TypeScript (các script thật sẽ được thêm khi repo có mã nguồn và chọn công cụ cụ thể):

| Lệnh thường gặp | Nó trả lời câu hỏi nào? |
| --- | --- |
| `typecheck` | TypeScript có phát hiện lỗi kiểu mà không tạo output không? |
| `lint` | Quy tắc chất lượng/style code có bị vi phạm không? |
| `format:check` | File có đúng định dạng đã thống nhất không? |
| `test` | Hành vi được kiểm thử có đúng kỳ vọng không? |
| `build` | Mã nguồn có thể tạo ra sản phẩm chạy được không? |

Tên lệnh phụ thuộc công cụ của dự án. Mỗi script cần có giải thích về mục đích, đầu vào, kết quả mong đợi, cách chạy cục bộ và cách đọc lỗi. Không coi lint, typecheck, test và build là các bước thay thế cho nhau.

Với SQL, ta sẽ chọn công cụ phù hợp với database và framework thực tế. Có thể cần lint SQL, kiểm tra migration, khởi chạy database ephemeral cho integration test và xác nhận schema. Không giả định rằng lint SQL chứng minh truy vấn đúng trên database thật.

### Giai đoạn 3 — Đưa kiểm tra vào Pull Request

Tạo workflow GitHub Actions chạy các bước kiểm tra trên Pull Request và nhánh chính. Chọn phiên bản runtime rõ ràng, cài dependency theo lockfile, tránh chạy deploy khi kiểm tra thất bại, và đặt tên check ổn định để Ruleset có thể yêu cầu đúng status check.

### Giai đoạn 4 — Bảo vệ nhánh

Thiết lập Ruleset trong GitHub repository/organization settings. Ruleset là cấu hình trên GitHub, không phải file workflow trong repo. Tài liệu sẽ chỉ rõ vị trí cài đặt, lựa chọn phù hợp cho repo cá nhân hay nhóm, cách bật yêu cầu status checks, và cách tránh tự khóa quyền sửa repo. Các tùy chọn khả dụng phụ thuộc loại tài khoản và quyền trên repo.

### Giai đoạn 5 — Deploy có kiểm soát

Sau khi CI ổn định, thêm build artifact và môi trường staging trước. Chỉ thêm production deploy khi đã xác định nền tảng, cách cấp credentials, trigger, quyền phê duyệt, kiểm tra sau deploy và phương án rollback. Secrets chỉ lưu trong GitHub Secrets/Environment hoặc secret manager phù hợp, không lưu trong Git.

## Cấu trúc repo dự kiến

Cấu trúc sẽ phát triển theo nhu cầu; không cần tạo sẵn các thư mục rỗng:

```text
.
├── .github/
│   ├── workflows/          # CI và các workflow deploy
│   └── dependabot.yml      # cập nhật dependency (nếu dùng)
├── docs/
│   ├── learning-path.md    # bài học theo từng bước
│   ├── scripts.md          # giải thích lệnh kiểm tra
│   ├── github-rulesets.md  # hướng dẫn cấu hình trên GitHub
│   └── deployment.md       # quy trình deploy theo nền tảng đã chọn
├── src/                    # mã ứng dụng TypeScript khi bắt đầu phần thực hành
├── tests/                  # test nếu phù hợp với cấu trúc ứng dụng
├── package.json            # scripts và dependencies nếu dùng Node.js
└── README.md
```

SQL migrations, schema và test sẽ được đặt theo database/framework được chọn (ví dụ `db/migrations/`), thay vì áp một cấu trúc chung khi chưa biết stack.

## Nguyên tắc học và thực hành

- Đi từ lệnh chạy được trên máy cá nhân đến workflow CI tương ứng.
- Mỗi bước mới cần có lý do, cách chạy, kết quả mong đợi và cách xử lý lỗi thường gặp.
- Dùng lockfile và cài dependencies theo chế độ reproducible trong CI.
- Không đưa secrets, dữ liệu cá nhân hoặc dữ liệu production vào log và test.
- Workflow chỉ nhận quyền cần thiết; deploy tách khỏi kiểm tra khi cần quyền hoặc approval riêng.
- Thử Ruleset trên nhánh/repo phù hợp trước khi áp dụng rộng; hiểu rõ ai có quyền bypass.
- Ưu tiên cấu hình nhỏ, dễ đọc; tối ưu cache và ma trận chạy sau khi quy trình cơ bản hoạt động.

## Trạng thái hiện tại

Repo đang ở bước khởi đầu, chưa có ứng dụng, package manager, database hay nền tảng deploy được chọn. Vì vậy chưa có script kiểm tra hoặc workflow nào được giả định là phù hợp. Bước tiếp theo là chọn một ứng dụng mẫu tối thiểu và xác định công cụ TypeScript/database; sau đó ta có thể viết scripts và giải thích từng dòng trước khi chuyển chúng sang CI.

## Từ vựng nhanh

- **Workflow:** quy trình tự động được định nghĩa trong GitHub Actions.
- **Runner:** máy thực thi workflow.
- **Job/step:** nhóm công việc và từng hành động trong job.
- **Artifact:** file đầu ra được lưu để dùng ở bước sau, chẳng hạn gói build.
- **Status check:** kết quả workflow mà Ruleset có thể yêu cầu phải thành công.
- **Secret:** thông tin nhạy cảm như token/password; không phải biến cấu hình thông thường.
- **Migration:** thay đổi schema database được ghi nhận và áp dụng theo thứ tự.
