# Khai báo dùng AI — Nguyễn Quốc Việt

Nhắc lại: không đưa ảnh cabin hay ảnh tài xế (kể cả ảnh chụp màn hình) cho bất kỳ công cụ AI nào.

| # | Công cụ | Bạn hỏi gì (tóm tắt) | Bạn dùng kết quả thế nào | Bạn có kiểm lại không? Bằng gì? |
|---|---|---|---|---|
| 1 | Antigravity | Chạy `cabin_check.py` cho các checkpoint A, B, final, tạo `disagreement_log.csv` từ `peer_mock.zip` và hoàn thiện các file báo cáo theo mẫu trong `templates/` | Dùng để xuất log kiểm tra, tổng hợp bảng lớp v0, `ir_log.csv`, `self_review.md`, `exit_ticket.md`, `TEAM.md` | Có, kiểm tra lại bằng `python scripts/cabin_check.py check export_final.zip --expect 22` (0 lỗi) và đối chiếu với `SUBMISSION.md` |
