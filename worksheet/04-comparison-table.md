# 04 · Comparison Table — Bảng so sánh đầy đủ

> **Mục tiêu**: Tổng hợp tất cả số đã tính ở `03-cost-calculation.md` thành 1 bảng so sánh duy nhất — đây là artifact chính nhóm sẽ present.
>
> **Thời gian**: 10 phút (đầu phần Final)

---

## Vì sao có bảng so sánh?

Khi sếp hỏi "Nên deploy config nào?", bạn cần đặt lên bàn **1 bảng** thay vì đọc 3 báo cáo riêng. Bảng so sánh đầy đủ cho phép so sánh thẳng từng dòng, dễ nhìn ra tradeoff.

---

## Bảng chính

Điền số đã tính. Số nào chưa có → quay lại `03-cost-calculation.md` tính cho xong.

| | Config 1 | Config 2 | Config 3 | (Config 4) |
|---|---|---|---|---|
| **Tên** | Budget Bot | Premium Concierge | Smart Mix | — |
| **① Model** | Gemini 2.5 Flash-Lite (all) | Claude Sonnet 4.6 (all) | Haiku 4.5 (Visa) + Flash-Lite (Guide/Weather) | — |
| **② Web search** | OFF | ON selective (Visa, Weather, Guide) | ON selective (Visa, Weather) | — |
| **③ History** | Last 3 | Full | Last 5 | — |
| **Intent classifier** | Keyword | LLM (GPT-4o-mini) | Keyword | — |
| **Cost / conv (Scenario A — 4 turns)** | $0.0010 | $0.057 | $0.0159 | — |
| **Cost / conv (Scenario B — 7 turns)** | $0.0012 | $0.069 | $0.0195 | — |
| **Monthly A** (300 conv/day × 30) | $9.00 | $513.95 | $143.10 | — |
| **Monthly B** (1,200 conv/day × 30) | $43.07 | $2,490.43 | $702.00 | — |
| **vs human $4,500/mo (A)** | rẻ 500× | rẻ 8.75× | rẻ 31.5× | — |
| **vs human $18,000/mo (B)** | rẻ 417× | rẻ 7.22× | rẻ 25.6× | — |
| **Savings % (A)** | 99.8% | 88.5% | 96.8% | — |
| **Savings % (B)** | 99.7% | 86.1% | 96.1% | — |
| **Quality estimate** | Low | High | Med-High | — |
| **Speed estimate** | High | Med | Med | — |
| **Điểm yếu chính** | Outdated info (tắt web) & mất ngữ cảnh dài. | Chi phí rất cao khi conv dài do Full history. | Routing phức tạp hơn — nhầm intent sẽ dùng sai model. | — |
| **Best for** (khi nào nên dùng) | FAQ cơ bản / volume cực cao cần tiết kiệm tối đa. | Khách hàng VIP cần tư vấn phức tạp, chính xác cao. | Triển khai cân bằng quanh năm cho cả 2 mùa. | — |

---

## Quan sát nhanh từ bảng

Trước khi sang file recommendation, trả lời 4 câu — đây là material để present:

### Câu 1 — Config rẻ nhất là gì? Đắt nhất là gì?

```text
Rẻ nhất: Budget Bot — monthly B = $43.07
Đắt nhất: Premium Concierge — monthly B = $2490.43
Chênh: ~57.8× lần
```

### Câu 2 — Knob nào ảnh hưởng cost nhiều nhất?

So sánh các config khác nhau ở knob nào, chênh bao nhiêu. Thường: model tier > history > web search.

```text
Model choice ảnh hưởng lớn nhất. Đổi từ cheap (Flash-Lite) sang strong (Sonnet 4.6) làm tăng base cost hàng chục lần. Bên cạnh đó, History Full ở Scenario B làm chi phí đội lên tuyến tính ở các turn cuối (Token tính dồn), trong khi Last 3 cắt giảm đáng kể lãng phí.
```

### Câu 3 — Tại sao Scenario B không đắt ×4 lần Scenario A?

Volume Scenario B = ×4 lần Scenario A. Turns dài hơn (7 vs 4 = ×1.75). Mong đợi monthly B ≈ A × 7. Thực tế có thể thấp hơn vì sao?

Trước khi viết, nghĩ: intent mix Scenario B có gì khác? Booking + Complaint = $0 LLM ở scenario B là bao nhiêu %?

```text
Vì tỷ lệ Handoff ở Scenario B cao hơn (45% vs 15% ở Scenario A), những intent như Booking và Complaint (chiếm 45%) sẽ chấm dứt rất sớm và được chuyển cho nhân viên (LLM cost = $0 cho lượt tiếp theo), giúp kiềm chế tổng chi phí thay vì scale trực tiếp theo hệ số ×4.
```

### Câu 4 — Có config nào AI đắt hơn human không?

So sánh monthly từng config với human baseline ($4,500 cho A, $18,000 cho B). Nếu AI rẻ hơn → savings %. Nếu đắt hơn → cần justify.

```text
Không có config nào đắt hơn human. Dù Config đắt nhất (Premium Concierge) có Monthly B lên tới $2,490, nhưng vẫn rẻ hơn con người ($18,000) khoảng 7.22 lần. AI mang lợi thế sẵn sàng 24/7, không giới hạn khung giờ, và scale up lượng khách đồng thời mà không cần mất thời gian training.
```

---

## Bảng kiểm trước khi sang file tiếp theo

- [x] Bảng đầy đủ — không còn ô trống
- [x] Đã có 4 câu trả lời cho 4 quan sát ở trên
- [x] Nhóm đồng thuận về số trong bảng (đã sanity check)

Xong → mở `05-recommendation.md` để viết recommendation cuối + chuẩn bị present.
