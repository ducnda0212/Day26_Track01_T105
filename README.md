# Day26_Track01_T105 — AI Adoption Change Management

## 1. Thành viên

| Họ tên | MSSV | Phần phụ trách | Góp ý đã đưa cho nhóm bạn |
|---|---|---|---|
| Nguyễn Đình Anh Đức | 2A202602856 | Phạm vi, chẩn đoán, workflow mới, lộ trình 30–60–90, dashboard, memo | |

## 2. Phạm vi

- **Sản phẩm AI:** Campus 24/7 - Hệ thống quản lý và điều phối vận hành ký túc xá thông minh
- **Nhóm người dùng chính:** Cán bộ ký túc xá
- **Quy trình:** Sinh viên báo sự cố → AI gợi ý ticket → Cán bộ duyệt và điều phối cho handler → Handler xác nhận hoàn thành

## 3. Nguyên nhân gốc

**Nguyên nhân 1:** Cán bộ chưa có căn cứ thực tế để tin AI vì chưa có track record trên dữ liệu thật; mọi số đo hiện chỉ từ golden set tự soạn.

- Framework: Gartner-Lite (Readiness) + ADKAR (nghẽn ở Desire)
- Bằng chứng: `eval/README.md` ghi golden set 93 case "do nhóm tự viết", tự điều phối chưa có trong eval; phân loại đúng 89%, nhóm hard 78%; P1 chỉ 7/10 với câu ngoài dataset

## 4. Cách làm mới

Ba thay đổi bắt buộc trong TO-BE:

1. **Nguồn kiểm chứng:** hiển thị căn cứ (`*_basis`) và nguồn gợi ý (luật hay LLM) cho cán bộ trên hàng chờ; hiện backend đã lưu nhưng chưa hiển thị
2. **Người chịu trách nhiệm:** cán bộ quyết định cuối và bắt buộc ghi lý do khi đổi gợi ý của AI; nhóm dự án (người phụ trách eval) review log override mỗi tuần, quyết định chỉnh luật/ngưỡng
3. **Xử lý khi AI không chắc:** ca không chắc và ca LLM dự phòng bắt buộc duyệt tay → ghi nhãn cuối → ẩn danh thêm vào golden set → chạy lại eval trước khi đổi luật

## 5. Chỉ số

Chi tiết 8 chỉ số trong `dashboard/` và `v1/`.

- **Product:** tỷ lệ phân loại đúng loại sự cố · baseline 89% · target ≥80% · nguồn `eval/results/latest.md` · owner nhóm dự án (người phụ trách eval)
- **Product:** P1 recall (bắt được ca nguy hiểm) · baseline 100% golden set, 7/10 ngoài dataset · target 100% · nguồn `latest.md` và `JOURNAL.md` · owner nhóm dự án (người phụ trách eval)
- **Workflow:** tỷ lệ ca không chắc chuyển đúng cho cán bộ · baseline 92% · target ≥80% · nguồn `latest.md` · owner nhóm dự án (người phụ trách eval)

## 6. Quyết định

**Tiếp tục**, theo hướng pilot 30 ngày với một nhóm cán bộ trên ticket thật ẩn danh. Lý do: chất lượng trên dữ liệu tự soạn đã đạt mục tiêu, nhưng còn thiếu track record thật và vòng phản hồi. Hai thay đổi so với v1: 
- (1) thêm chỉ số tỷ lệ sửa gợi ý có ghi lý do để đo thay đổi TO-BE số 2
- (2) đặt target tương đối so với baseline 30 ngày đầu cho các chỉ số vận hành, kèm cổng 30–60–90 dựa trên bằng chứng
