# 04 · Comparison Table — Bảng so sánh đầy đủ

> **Mục tiêu**: Tổng hợp tất cả số liệu thành 1 bảng so sánh duy nhất — artifact chính để present.

---

## Bảng so sánh

| | Budget Bot | Premium Concierge | Smart Mix |
|---|---|---|---|
| **① Model** | Gemini 2.5 Flash-Lite (all) | Claude Sonnet 4.6 (all) | Haiku 4.5 (Visa) + Flash-Lite (Guide/Weather) |
| **② Web search** | OFF | ON selective (Visa, Weather, Guide) | ON selective (Visa, Weather) |
| **③ History** | Last 3 | Full | Last 5 |
| **Classifier** | Keyword ($0) | LLM GPT-4o-mini | Keyword ($0) |
| **Cost/conv — Scenario A (4 turns)** | $0.0010 | $0.057 | $0.0159 |
| **Cost/conv — Scenario B (7 turns)** | $0.0012 | $0.069 | $0.0195 |
| **Monthly A** (300 conv/day × 30) | $9.00 | $513.95 | $143.10 |
| **Monthly B** (1,200 conv/day × 30) | $43.07 | $2,490.43 | $702.00 |
| **vs human $4,500/mo (A)** | rẻ 500× | rẻ 8.75× | rẻ 31.5× |
| **vs human $18,000/mo (B)** | rẻ 417× | rẻ 7.22× | rẻ 25.6× |
| **Savings % (A)** | 99.8% | 88.5% | 96.8% |
| **Savings % (B)** | 99.7% | 86.1% | 96.1% |
| **Quality** | Low | High | Med-High |
| **Speed** | High | Med | Med |
| **Điểm yếu chính** | Outdated info (web OFF) + mất ngữ cảnh dài. | Chi phí rất cao khi conv dài (Full history + model đắt). | Routing phức tạp hơn — nhầm intent sẽ dùng sai model. |
| **Best for** | FAQ cơ bản / volume cực cao cần tiết kiệm tối đa. | Khách VIP cần tư vấn chính xác, phức tạp. | Triển khai cân bằng quanh năm cả 2 mùa. |

---

## 4 Quan sát từ bảng

### 1. Config rẻ nhất và đắt nhất?

Rẻ nhất: **Budget Bot** — monthly B = $43.07  
Đắt nhất: **Premium Concierge** — monthly B = $2,490.43  
Chênh: ~57.8× lần

### 2. Knob nào ảnh hưởng cost nhiều nhất?

Model choice ảnh hưởng lớn nhất: đổi từ cheap (Flash-Lite) sang strong (Sonnet 4.6) làm tăng base cost hàng chục lần. History là knob thứ 2: Full history ở Scenario B khiến token input đội lên tuyến tính qua từng turn, trong khi Last 3 cắt giảm đáng kể. Web search ảnh hưởng ít hơn nhưng cộng dồn đáng kể nếu bật cho nhiều intent.

### 3. Tại sao Scenario B không đắt ×4 lần Scenario A?

Vì tỷ lệ handoff ở Scenario B cao hơn nhiều (45% vs 15% ở Scenario A): Booking và Complaint chiếm 45% volume nhưng chấm dứt ngay lượt 1 và chuyển nhân viên — LLM cost = $0. Điều này kiềm chế tổng chi phí thay vì scale thẳng theo hệ số ×4 như volume.

### 4. Có config nào AI đắt hơn human không?

Không. Ngay cả Premium Concierge đắt nhất cũng chỉ $2,490/tháng (Scenario B) — vẫn rẻ hơn human $18,000 gấp 7.22×. AI thắng thêm ở 3 chiều mà chi phí không tính được: hoạt động 24/7, phục vụ đa ngôn ngữ, scale đồng thời nhiều khách mà không tăng headcount.

---

## Bảng kiểm

- [x] Bảng đầy đủ — không còn ô trống
- [x] Đã có 4 câu trả lời quan sát
- [x] Nhóm đồng thuận về số trong bảng (đã sanity check)
