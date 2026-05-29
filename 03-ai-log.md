# 03 — AI Log (Cá nhân)

> Mục tiêu của log này là ghi lại **tôi đã dùng AI ở chỗ nào**, AI **hay sai ở chỗ nào**, và tôi **đã sửa lại** ra sao để bài nộp hợp rubric.

## AI giúp gì

- Tôi dùng AI để **brainstorm nhanh** các ý tưởng trong Phase 1 (SCAN) theo nhiều góc nhìn, sau đó tôi tự chọn và tự viết lại cho khớp với VinFast.
- Tôi dùng AI như “editor” để **chỉnh format** theo đúng mẫu `02-deliverable-example.md` (tiêu đề Phase, cách trình bày card, cách diễn đạt gọn hơn).
- Tôi dùng AI để **soát lỗi nhất quán** giữa các file (Card nào deep-dive, metric có bị mâu thuẫn giữa `01-problem-scan.md` và `02-deep-dive-report.md` không).
- Tôi dùng AI để **gợi ý boundary** cho prototype: bắt buộc `[DRAFT_ONLY]`, không auto-book, không chẩn đoán chắc chắn; và gợi ý 2–3 prompt tấn công để thử.

## AI sai gì

- AI đôi khi viết **nghe rất “tròn trịa”** nhưng lại chung chung, dễ thành “văn AI”. Nếu copy nguyên xi sẽ thiếu cảm giác “người làm thật”.
- AI có lúc **đề xuất số liệu/volume/ROI** khá tự tin trong khi mình không có log thật. Nếu không kiểm soát sẽ thành bịa số.
- AI có xu hướng “đẩy” lên Agent sớm, trong khi bài này thực tế chỉ cần **LLM Feature + HITL** là đủ an toàn.

## Sửa đổi ra sao

- Với phần nội dung, tôi **viết lại bằng lời của mình**, giữ câu ngắn, bỏ bớt thuật ngữ không cần thiết, và thêm 1–2 chi tiết cụ thể để tự nhiên hơn.
- Với phần số liệu, tôi chỉ giữ những metric **đo được trong pilot** (ví dụ thời gian xử lý p50; accuracy top-3 qua audit), còn chỗ nào chưa có baseline thì ghi rõ “cần log”.
- Với phần kiến trúc, tôi chốt **LLM Feature + HITL** (agent duyệt trước khi chốt lịch), tránh mô tả Agent tự trị gây rủi ro vận hành.
- Với prototype, tôi chạy autograder và sửa cho qua được các kiểm tra ranh giới (boundary) thay vì chỉ “viết prompt cho hay”.
