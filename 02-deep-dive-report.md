# 02 — Deep-Dive Report (Bài nhóm)

> **Tên nhóm:** (Điền tên nhóm tại đây)  
> **Thành viên:**  
> - Họ tên — MSSV: (điền)  
> - Họ tên — MSSV: (điền)  
> - Họ tên — MSSV: (điền)  

---

## 0) Quyết định lựa chọn bài toán

Nhóm thống nhất chọn bài toán:

**VinFast — Tự động phân loại & gán ticket bảo hành từ mô tả lỗi + ảnh đính kèm**  

Lý do chọn: volume cao, quy trình lặp lại, có thể đặt **HITL** rõ ràng để kiểm soát rủi ro, và metric cải thiện thời gian phản hồi dễ đo.

---

## 3.1) Current-State Workflow Mapping (mô tả bằng chữ)

Quy trình hiện tại (CS bảo hành xử lý thủ công):

1. **Nhận ticket** từ email/form (mô tả lỗi + ảnh/video).  
2. **Đọc nội dung** và mở ảnh/video để hiểu triệu chứng.  
3. **Chọn loại lỗi** (điện/pin/OTA/nội thất/ngoại thất/khác) và **độ ưu tiên**.  
4. **Gán bộ phận xử lý** (đại lý/xưởng/hotline kỹ thuật) + cập nhật hệ thống ticketing.  
5. **Soạn phản hồi xác nhận** (SLA, hướng dẫn bước tiếp theo) gửi khách.

- 🔴 **Bottleneck**: Bước (2)–(3) (đọc + hiểu + phân loại) vì mô tả không chuẩn, ảnh mờ/nhiều góc.  
- 🔄 **Handoff**: (4) chuyển từ CS sang bộ phận kỹ thuật/đại lý; nếu gán sai sẽ phải chuyển vòng, kéo dài SLA.

---

## 3.2) Problem Statement (6-field) & Metrics

| Field | Nội dung |
|---|---|
| **1. Actor / Operator** | Nhân viên CS bảo hành VinFast; bộ phận kỹ thuật/đại lý nhận xử lý; khách hàng chờ phản hồi |
| **2. Current Workflow** | Nhận ticket → đọc mô tả & xem ảnh → phân loại lỗi & ưu tiên → gán đội xử lý → phản hồi xác nhận SLA |
| **3. Bottleneck** | Hiểu mô tả tự nhiên + ảnh/video để phân loại đúng; dễ sai khi khách mô tả thiếu/không chuẩn |
| **4. Business Impact** | Gán sai làm tăng vòng chuyển ticket, kéo dài SLA; CS quá tải giờ cao điểm; khách không hài lòng vì chờ lâu |
| **5. Success Metric** | (a) Thời gian phân loại/gán: từ ~7 phút → **< 90 giây** (bản nháp) ; (b) Tỷ lệ gán sai giảm xuống **< 3%** sau bước duyệt người (HITL) |
| **6. Operational Boundary** | AI **chỉ đề xuất** phân loại + đội xử lý + draft phản hồi; **không tự gửi** cho khách; mọi gán chính thức phải **được CS duyệt**; AI không được đưa kết luận bảo hành/đổ lỗi khách hàng |

---

## 3.3) Future-State Flow & AI Fit

### AI Fit
- **LLM Feature + HITL** (không cần agentic loop ở bản đầu): mục tiêu là “tạo nháp nhanh + gợi ý tuyến xử lý”.

### Future-State Flow (mô tả bước)

1. **Ingest** ticket (text + attachments metadata).  
2. 🔵 **AI Step**: trích xuất triệu chứng (symptom summary), đề xuất:
   - `issue_category` (loại lỗi)
   - `priority`
   - `routing_team` (đại lý/xưởng/hotline)
   - draft phản hồi xác nhận + câu hỏi bổ sung (nếu thiếu dữ liệu)
3. 🟢 **Human-in-the-loop (CS Review)**:
   - chỉnh/đổi đề xuất nếu cần
   - xác nhận routing + gửi phản hồi cho khách
4. 🔄 **Handoff**: ticket chuyển sang đội kỹ thuật/đại lý xử lý theo tuyến đã duyệt.

### Fallback (khi AI lỗi/không tự tin)
- Nếu thiếu ảnh/video hoặc confidence thấp → **route mặc định** sang CS manual queue + template hỏi bổ sung.
- Nếu mô tả liên quan an toàn (cháy, chập, tai nạn) → **đánh priority cao** và bắt buộc CS/đội kỹ thuật xem ngay (không auto-route).

---

## 5) Evaluate — AI Readiness Checklist & Decision

### AI Readiness Checklist
1. Dữ liệu mẫu/logs sạch để test?  
   - Có thể trích ticket lịch sử (text + nhãn tuyến xử lý) để làm baseline; cần xử lý ẩn danh PII trước.
2. Rủi ro khi AI sai có kiểm soát được?  
   - Có: dùng **HITL** bắt buộc, AI chỉ tạo nháp và đề xuất.
3. Stakeholders sẵn sàng thay đổi quy trình cũ?  
   - Khả thi: CS thường thích công cụ “gợi ý nhanh” nếu giúp giảm tải.

### Quyết định
**GO** (Prototype scope hẹp)

### Justification (luận điểm kỹ thuật + chi phí)
- Scope hẹp: chỉ làm **draft phân loại + routing** cho một số nhóm lỗi phổ biến.
- Chi phí chính: chuẩn hóa dữ liệu ticket lịch sử + xây UI review cho CS.
- Rủi ro: gán sai tuyến → xử lý bằng HITL và fallback queue.

