# 01 — Problem Scan & Quick-Assess — Vin Smart Future (VinFast Use Case)

> **Bài nộp Phase 1–2 của nhóm VinClass, định vị theo Rubric lab và bối cảnh vận hành Vin Smart Future.**
>
> * **Mục tiêu của file này:** Ghi lại kết quả SCAN & Quick-Assess — nền tảng để nhóm chọn 1 bài toán Deep-Dive và đối chiếu với [02-deliverable-example.md](02-deliverable-example.md).
> * **Mảng kinh doanh lựa chọn:** **VinFast — Dịch vụ sau bán, đặt lịch xưởng & hỗ trợ chủ xe.**

---

## 🏛️ Bối cảnh: Tôi là ai?

Tôi là **Nguyễn Trọng Nguyên**, học viên nhóm **VinClass** trong chương trình Vin Smart Future. Nhóm mình được yêu cầu ngồi cùng team **CS đặt lịch xưởng VinFast** — những người xử lý ticket từ App và chat — để xem chỗ nào có thể nhờ AI đỡ việc.

Buổi shadow đó tôi thấy rõ một kiểu ticket lặp đi lặp lại: khách không nói “lỗi P0420” mà nói *“xe kêu cụp cụp qua ổ gà”*. Agent phải đọc hết thread, lật tài liệu kỹ thuật, rồi đoán hạng mục xưởng cho đúng — mất khoảng vài phút, giờ cao điểm thì queue dồn. Có lần chọn nhầm hạng mục, khách đến xưởng phải chờ đổi lịch. Bài toán hôm nay của nhóm xuất phát từ đúng chỗ đó.

---

# 🔍 Phase 1 — SCAN: Tìm kiếm cơ hội (Cá nhân)

Dùng **4 Lenses** quét vận hành **VinFast** (cùng tập trung công ty thành viên, các góc lens khác nhau).

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|------------|------|---------------------|
| 1 | **VinFast** | Lặp lại | Hàng tuần team tài chính/vận hành trạm sạc **đối chiếu log sạc** từ trụ liên kết với hóa đơn đối tác — nhiều dòng lệch, xử lý thủ công trên Excel. |
| 2 | **VinFast** | Tốn thời gian | **Hotline pin yếu (1900 23 23 89):** tra trạm sạc + soạn chỉ dẫn; nếu pin < ngưỡng thì hỏi cứu hộ — agent gọi RSA/MBC thủ công — **~12–15 phút/cuộc** (ước lượng). |
| 3 | **VinFast** | AI-upgrade | Khách mô tả tiếng Việt tự nhiên trên App/chat; agent phải **map sang mã lỗi / hạng mục bảo dưỡng** trước khi đặt lịch xưởng. |
| 4 | **VinFast** | Pain từ người khác | Chủ xe phàn nàn **chờ tổng đài** giờ cao điểm dù đã có **Trợ lý ảo ViVi** — case phức tạp (cứu hộ, đổi lịch) vẫn rơi về người. |
| 5 | **VinFast** | Tốn thời gian | Agent **đặt lịch dịch vụ** đọc lại lịch sử chat/app + kiểm tra bảo hành trước khi chốt slot — **~8 phút/lượt** (ước lượng). |

**Nguồn neo (không bịa %):**

- Trợ lý ảo ViVi: [VinBigdata case study](https://vinbigdata.com/en/case-studies/the-comprehensive-vietnamese-virtual-assistant-on-vinfasts-electric-car.html)
- Hotline CSKH / xưởng: [VinFast hotline tổng hợp](https://vinfast.vn/tong-hop-hotline-he-thong-xuong-dich-vu-ho-tro-tren-duong-danh-cho-khach-hang-vinfast/)

---

# 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards (Cá nhân)

Chọn top 3 từ SCAN: **#2 (pin/cứu hộ), #3 (triệu chứng), #5 (đặt lịch xưởng).**

## Thẻ bài toán tiêu biểu: Card #2 — VinFast Phân loại triệu chứng tiếng Việt (Deep-dive · SCAN #3)

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán: Khách mô tả triệu chứng xe bằng tiếng Việt tự     │
│ nhiên cần map sang mã lỗi / hạng mục xưởng trước đặt lịch.  │
│ Công ty thành viên: [x] VinFast                             │
│                                                             │
│ Ai đang đau? Agent CS đặt lịch, Kỹ thuật viên (ticket mơ hồ) │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Khách gửi mô tả triệu chứng qua App/chat VinFast       │
│   → 2. Agent CS đọc toàn bộ thread và ghi chú thủ công      │
│   → 3. Tra cứu tài liệu kỹ thuật / mã lỗi trên hệ thống nội bộ│
│   → 4. Chọn hạng mục bảo dưỡng / sửa chữa phù hợp           │
│   → 5. Chốt slot lịch hẹn xưởng dịch vụ cho khách            │
│                                                             │
│ Bước nào tốn nhất? Bước 2-3 (⏱ 6 phút/lượt)                 │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2-3              │
│ (Phân loại intent -> gợi ý mã lỗi -> draft ghi chú cho agent)│
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│ Giảm thời gian xử lý từ 6 phút ──> dưới 2 phút; tỉ lệ đặt   │
│ nhầm hạng mục không tăng quá 2%.                            │
│                                                             │
│ Quick Architecture: [x] LLM Feature (Phân loại + draft ghi chú)│
└─────────────────────────────────────────────────────────────┘
```

---

### QUICK PROBLEM CARD #1 — Sự cố pin yếu / cứu hộ (SCAN #2)

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán: Chủ xe VinFast báo pin yếu giữa đường cần hướng   │
│ dẫn trạm sạc; nếu pin < ngưỡng thì hỏi cứu hộ và (khi đồng │
│ ý) kết nối RSA/MBC. Công ty thành viên: [x] VinFast         │
│                                                             │
│ Ai đang đau? Chủ xe (chờ đợi), Agent CS (quá tải)           │
│                                                             │
│ Workflow thủ công hiện tại (6 bước):                        │
│   1. Khách gọi 1900 23 23 89                                │
│   → 2. Agent ghi pin %, GPS, model xe                       │
│   → 3. Tra trạm sạc + loại cổng (CCS2/GBT)                  │
│   → 4. Soạn SMS/App chỉ đường                               │
│   → 5. Pin < ngưỡng: hỏi có cần cứu hộ                      │
│   → 6. Khách đồng ý: agent gọi RSA/MBC thủ công             │
│                                                             │
│ Bước nào tốn nhất? Bước 3-4 và 6 (⏱ 10-12 phút/lượt)        │
│ AI có thể nhảy vào? Bước 3-4 (draft tin); 5-6 (consent)     │
│                                                             │
│ Metric: 15 phút ──> dưới 3 phút; ≥98% đúng cổng sạc.        │
│ Quick Architecture: [x] LLM Feature + [x] Agent (guardrail) │
└─────────────────────────────────────────────────────────────┘
```

---

### QUICK PROBLEM CARD #3 — Đặt lịch dịch vụ xưởng (SCAN #5)

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán: Agent đặt lịch phải đọc lại lịch sử chat/app và   │
│ kiểm tra bảo hành trước khi chốt slot.                       │
│ Công ty thành viên: [x] VinFast                             │
│                                                             │
│ Ai đang đau? Agent CS đặt lịch, Khách hàng (chờ xác nhận)   │
│                                                             │
│ Workflow (4 bước):                                          │
│   1. Khách yêu cầu đặt lịch qua App/chat/tổng đài            │
│   → 2. Agent đọc thread + ticket cũ                         │
│   → 3. Kiểm tra bảo hành trên CRM                           │
│   → 4. Chốt slot trên DMS xưởng VinFast                      │
│                                                             │
│ Bước nào tốn nhất? Bước 2-3 (⏱ 8 phút/lượt)                 │
│ AI có thể nhảy vào? Bước 2-3 (tóm tắt + gợi ý slot, HITL)   │
│                                                             │
│ Metric: 8 phút ──> dưới 3 phút; không tăng đặt nhầm slot.    │
│ Quick Architecture: [x] LLM Feature                         │
└─────────────────────────────────────────────────────────────┘
```

---

# 🗳️ Quyết định lựa chọn của nhóm

Nhóm quyết định chọn bài toán **"Card #2 — VinFast Phân loại triệu chứng tiếng Việt → hạng mục xưởng"** (SCAN #3) để thực hiện Deep-Dive.

## Lý do lựa chọn và loại bỏ các thẻ khác

* **Card #1 (Sự cố pin yếu / cứu hộ):** Workflow gần song song ví dụ minh họa Xanh SM (hotline → tra cứu → chỉ đường → cứu hộ) trong [02-deliverable-example.md](02-deliverable-example.md). Nhóm chọn bài **khác domain** để thể hiện scoping độc lập.
* **Card #3 (Đặt lịch dịch vụ xưởng):** Chủ yếu tóm tắt thread + gợi ý slot — overlap Bước 2–3 của Card #2; khó tách metric *phân loại hạng mục* riêng.

**Vì sao chọn Card #2:** **App/chat + NLP tiếng Việt + catalog kỹ thuật**, khác hẳn điều phối cứu hộ; phù hợp **LLM Feature + HITL**; metric rõ (6 phút → 2 phút, ≤2% nhầm hạng mục). Chi tiết Deep-Dive: [02-deep-dive-report.md](02-deep-dive-report.md).
