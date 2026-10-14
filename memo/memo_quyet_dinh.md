# Memo quyết định — Nhóm T105 (Campus 24/7)

## 1. Vấn đề và nguyên nhân gốc

- **Phạm vi:** Campus 24/7, cán bộ ký túc xá, chuỗi phân loại → điều phối → theo dõi SLA → xác nhận hoàn tất.
- **Vấn đề:** AI chưa có track record trên dữ liệu thật, cán bộ chưa có căn cứ outcome để tin gợi ý.
- **Nguyên nhân gốc:** (1) chưa có dữ liệu thật để kiểm chứng; (2) vòng phản hồi chưa khép kín: override không kèm lý do, chưa có người chỉnh luật và ngưỡng.

## 2. Framework đã dùng và bằng chứng

- **Framework:** Gartner-Lite (Readiness), Mollick, ADKAR (Desire, Reinforcement).
- **Bằng chứng:** `eval/README.md` (golden set tự soạn, tự điều phối chưa nằm trong eval); `eval/results/latest.md` (phân loại 89%, hard 78%, typo 25%, abbrev 50%); `JOURNAL.md` tuần 5 (P1 7/10 ngoài dataset); `ticket_action_service.py` (override không bắt buộc lý do); `auto_dispatch.py` (ngưỡng 8/9 nằm trong mã).

## 3. Ít nhất 2 thay đổi sau phản biện

Chưa có nhóm phản biện nên các thay đổi dưới đây đến từ **tự rà soát v1 theo 4 trục** (Phạm vi / Framework / Chỉ số / Hành động):

1. **Chỉ số** — v1 có thay đổi TO-BE "bắt buộc ghi lý do khi sửa gợi ý" nhưng không có chỉ số nào đo nó. v2 thêm chỉ số "tỷ lệ lần sửa gợi ý có ghi lý do", baseline chưa đo, target 100% sau khi bật bắt buộc.
2. **Chỉ số** — 5 chỉ số vận hành ở v1 để target "đặt sau khi có baseline", nên chưa ra quyết định được. v2 đặt target tương đối: override ưu tiên và thời gian xử lý giảm ≥20% so với baseline sau 60 ngày; đúng hạn SLA không thấp hơn baseline. Đây là đề xuất, hiệu chỉnh khi có dữ liệu thật.
3. **Hành động** — v1 chưa có tiêu chí chuyển giai đoạn rõ. v2 thêm sheet "Cổng 30-60-90" với dấu hiệu hoàn thành dựa trên bằng chứng cho từng giai đoạn.

## 4. Quyết định

**Tiếp tục**, theo hướng pilot 30 ngày.

## 5. Lý do, bước tiếp theo và owner

- **Lý do:** chất lượng AI trên dữ liệu tự soạn đã đạt mục tiêu (phân loại 89%, P1 recall 100%, ca không chắc 92%), nhưng còn thiếu track record thật và vòng phản hồi.
- **Bước tiếp theo:** pilot một nhóm cán bộ trên ticket thật đã ẩn danh; ghi baseline; bật hiển thị căn cứ và bắt buộc ghi lý do khi sửa. Owner: cán bộ KTX và nhóm dự án (người phụ trách eval).

### Phụ lục: AS-IS / TO-BE

| TRƯỚC (AS-IS) | SAU (TO-BE) |
|---|---|
| Backend có căn cứ và độ tin cậy theo nguồn, chưa hiển thị cho cán bộ | Hiển thị căn cứ và nguồn (luật hay LLM) trên hàng chờ |
| Cán bộ đổi ưu tiên, người xử lý, hạn: chỉ ghi `cũ → mới` | Bắt buộc ghi lý do; nhóm dự án review log override hàng tuần |
| Eval chạy tay, dữ liệu tự soạn; luật và ngưỡng sửa trong mã | Ca không chắc duyệt tay → gán nhãn → thêm vào golden set → chạy lại eval trước khi đổi luật |

### Phụ lục: Lộ trình 30–60–90 ngày

| 0–30 ngày: Chứng minh vấn đề | 31–60 ngày: Chứng minh chất lượng | 61–90 ngày: Quyết định mở rộng |
|---|---|---|
| Pilot một nhóm cán bộ; nhập ticket thật đã ẩn danh; ghi baseline. Owner: cán bộ KTX. Hoàn thành khi: có baseline ≥4 chỉ số vận hành và ≥30 ticket thật đã gán nhãn tay | Hiển thị căn cứ, bắt buộc lý do, review log hàng tuần, thêm ticket thật vào golden set và chạy eval. Owner: nhóm dự án (người phụ trách eval). Hoàn thành khi: ≥1 vòng chỉnh luật từ override log, P1 recall vẫn 100%, tỷ lệ sửa có lý do = 100% | So với mốc đầu, xác định ai sở hữu luật và ngưỡng, quyết định tiếp tục / sửa / dừng. Owner: nhóm dự án |