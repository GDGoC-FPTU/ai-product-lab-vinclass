# 01 — Problem Scan (Bài cá nhân)

> **Vin Smart Future — Lab 02: AI Product Scoping**
>
> Bài làm cá nhân: quét cơ hội (SCAN) và đánh giá nhanh (QUICK-ASSESS) trước khi thảo luận nhóm.

---

## 🏛️ Bối cảnh: Tôi là ai?

Tôi Nguyễn Thành Tài là **AI Product Engineer** tại **Vin Smart Future**. Trước buổi Lab, tôi đã lướt qua các kênh nội bộ (ticket Jira, nhóm Zalo vận hành, phản hồi từ đại lý/khách sạn) của một vài công ty thành viên để ghi nhận các tác vụ thủ công lặp lại hoặc gây phàn nàn từ người vận hành thực địa — không chỉ tập trung vào một mảng duy nhất.

---

# 🔍 Phase 1 — SCAN: Tìm kiếm cơ hội (Cá nhân)

Dùng **4 Lenses** quét qua vận hành của các công ty thành viên Vingroup.


| #   | Subsidiary     | Lens               | Mô tả ngắn bài toán                                                                                                                                                    |
| --- | -------------- | ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | **VinFast**    | Lặp lại            | Phân loại và gán ticket bảo hành từ email/form khách hàng (mô tả lỗi xe, ảnh đính kèm) — trung bình 200+ ticket/ngày, nhân viên CS phải đọc và chọn loại lỗi thủ công. |
| 2   | **Vinpearl**   | Tốn thời gian      | Lễ tân soạn email xác nhận + itinerary cá nhân hóa cho khách đoàn MICE (hội nghị, cưới) — khoảng 18–25 phút/nhóm khách.                                                |
| 3   | **Vinhomes**   | Lặp lại            | Ban quản lý nhập thủ công thông tin đăng ký thẻ xe từ form giấy/PDF cư dân gửi qua app hoặc quầy (biển số, chủ xe, căn hộ) vào hệ thống bãi xe.                        |
| 4   | **Vinmec**     | AI-upgrade         | Hotline/App đặt lịch hẹn chưa hiểu mô tả triệu chứng tự nhiên của bệnh nhân → gợi ý sai chuyên khoa, nhân viên tổng đài phải hỏi lại nhiều vòng.                       |
| 5   | **Xanh SM**    | Pain từ người khác | Tài xế phàn nàn thưởng cuối ca sai lệch do đối soát thủ công chuyến đi, phụ phí đường cao tốc và khuyến mãi với bảng tính Excel (mất 2–3 ngày chờ phản hồi).           |
| 6   | **VinWonders** | Tốn thời gian      | Nhân viên quầy vé xử lý thủ công đổi/trả vé combo khi khách đổi lịch tham quan do thời tiết (đọc điều khoản, tính chênh lệch giá) — 8–12 phút/lượt vào cuối tuần.      |


---

# 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards (Cá nhân)

Chọn top 3 từ danh sách SCAN: **#1 (VinFast Bảo hành), #2 (Vinpearl MICE), #4 (Vinmec Đặt lịch).**

---

## Quick Problem Card #1 — VinFast Phân loại ticket bảo hành

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán: Tự động phân loại và gán ticket bảo hành VinFast  │
│ từ mô tả lỗi + ảnh khách gửi qua email/form.                │
│ Công ty thành viên: [x] VinFast                             │
│                     [ ] Xanh SM  [ ] Vinhomes               │
│                     [ ] Vinmec   [ ] Khác                   │
│                                                             │
│ Ai đang đau (Actor)? Nhân viên CS bảo hành (quá tải),       │
│ khách hàng (chờ phản hồi lâu khi ticket gán sai bộ phận).   │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Khách gửi form/email mô tả lỗi + ảnh/video             │
│   → 2. CS đọc nội dung và mở ảnh đính kèm                   │
│   → 3. Chọn thủ công loại lỗi (điện/pin/nội thất/OTA...)    │
│   → 4. Gán bộ phận xử lý (đại lý / xưởng / hotline kỹ thuật)│
│   → 5. Gửi email xác nhận SLA cho khách                     │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2–3 (⏱ 6–8 phút/lượt)│
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2–3              │
│ (Trích xuất triệu chứng từ text/ảnh → đề xuất loại lỗi +    │
│ bộ phận; CS chỉ review trước khi gán chính thức)            │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm thời gian phân loại từ 7 phút ──> dưới 90 giây;        │
│ tỷ lệ gán sai bộ phận từ ~12% ──> dưới 3% (sau HITL).       │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

---

## Quick Problem Card #2 — Vinpearl Itinerary khách đoàn MICE

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán: Tự động soạn email xác nhận + lịch trình (itinerary)│
│ cá nhân hóa cho khách đoàn MICE tại Vinpearl.               │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [x] Khác: Vinpearl         │
│                                                             │
│ Ai đang đau (Actor)? Lễ tân / Sales coordinator (soạn thủ công),│
│ khách đoàn (nhận thông tin chậm, sai giờ check-in/phòng họp).│
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                          │
│   1. Sales xuất booking summary từ PMS (phòng, F&B, AV)     │
│   → 2. Lễ tân mở template Word và điền từng mục thủ công      │
│   → 3. Kiểm tra chính sách hủy, deposit, dress code từng sự kiện│
│   → 4. Gửi email + follow-up Zalo/phone nếu khách hỏi thêm    │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2–3 (⏱ 20 phút/lượt)  │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2–3              │
│ (Draft itinerary + điều khoản từ structured booking data;   │
│ nhân viên chỉnh tone thương hiệu và duyệt trước khi gửi)     │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm thời gian soạn từ 22 phút ──> dưới 5 phút (draft);    │
│ 95% email gửi trong vòng 2 giờ sau khi Sales chốt booking.  │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

---

## Quick Problem Card #3 — Vinmec Gợi ý chuyên khoa khi đặt lịch

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán: Hiểu mô tả triệu chứng tự nhiên của bệnh nhân     │
│ để gợi ý chuyên khoa/bác sĩ phù hợp khi đặt lịch qua App/  │
│ hotline Vinmec (giảm vòng hỏi lại của tổng đài).            │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [x] Vinmec   [ ] Khác                   │
│                                                             │
│ Ai đang đau (Actor)? Nhân viên tổng đài (quá tải giờ cao điểm),│
│ bệnh nhân (đặt nhầm khoa, phải đổi lịch, chờ lâu).          │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Bệnh nhân gọi App/hotline, mô tả triệu chứng tự do      │
│   → 2. Tổng đài hỏi thêm 3–5 câu để thu hẹp                  │
│   → 3. Tra cứu bảng mapping triệu chứng → chuyên khoa (PDF)  │
│   → 4. Kiểm tra lịch trống bác sĩ trên HIS thủ công         │
│   → 5. Xác nhận lịch và gửi SMS nhắc                        │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2–3 (⏱ 5–7 phút/cuộc) │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2–3              │
│ (Tóm tắt triệu chứng + gợi ý top-2 chuyên khoa có confidence;│
│ tổng đài hoặc bệnh nhân chọn; KHÔNG tự chẩn đoán bệnh)       │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm thời gian tư vấn từ 6 phút ──> dưới 2 phút;            │
│ tỷ lệ đặt nhầm chuyên khoa từ ~18% ──> dưới 8%.             │
│                                                             │
│ Quick Architecture: [ ] No AI  [x] Rule  [x] LLM  [ ] Agent   │
│ (Rule: từ khóa cấp cứu → chuyển ngay tổng đài người;        │
│  LLM: diễn giải triệu chứng tự nhiên → gợi ý khoa)          │
└─────────────────────────────────────────────────────────────┘
```

---

## Ghi chú lựa chọn cho nhóm (tham khảo)


| Thẻ             | Điểm mạnh                                      | Rủi ro cần lưu ý                                                   |
| --------------- | ---------------------------------------------- | ------------------------------------------------------------------ |
| **#1 VinFast**  | Volume cao, metric rõ, dữ liệu text/ảnh sẵn có | Ảnh lỗi kỹ thuật cần HITL; không được AI tự từ chối bảo hành       |
| **#2 Vinpearl** | ROI thời gian nhân sự rõ, ít rủi ro y tế       | Sai giờ sự kiện gây khiếu nại — bắt buộc duyệt người trước gửi     |
| **#3 Vinmec**   | Impact trải nghiệm bệnh nhân lớn               | Ranh giới y khoa nghiêm; cấp cứu phải Rule-based chuyển người ngay |


*Nhóm có thể chọn một trong ba thẻ trên cho Phase 3 (Deep-Dive) tùy dữ liệu và stakeholder sẵn có trong lớp.*