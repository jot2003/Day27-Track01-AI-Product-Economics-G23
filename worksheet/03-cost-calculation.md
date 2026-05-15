# 03 · Cost Calculation — Chi phí từng Config × 2 Scenarios

> **Mục tiêu**: Tính cost/turn → cost/conversation → monthly cho cả 2 scenarios (low season + high season).

---

## Tham số chung

| Tham số | Giá trị |
|---|---|
| System prompt | 500 tokens |
| User message | 80 tokens |
| Assistant response | 180 tokens (output) |
| 1 prior turn (history) | 260 tokens |
| RAG top-5 chunks | 1,250 tokens |
| Web search results | 800 tokens (khi bật) |
| Web search API | $0.008 / query (Tavily) |
| Human baseline | $0.50 / conversation |

### Scenario A — Mùa thấp điểm

| Tham số | Giá trị |
|---|---|
| Volume | 300 conversations / ngày |
| Turns/conv | avg 4 lượt |
| Intent mix | Guide 50%, Visa 25%, Weather 10%, Booking 10%, Complaint 5% |
| AI-served ratio | 85% (15% handoff) |
| Human baseline/tháng | $4,500 |

### Scenario B — Mùa cao điểm

| Tham số | Giá trị |
|---|---|
| Volume | 1,200 conversations / ngày (×4) |
| Turns/conv | avg 7 lượt |
| Intent mix | Guide 30%, Visa 15%, Weather 10%, Booking 35%, Complaint 10% |
| AI-served ratio | 55% (45% handoff) |
| Human baseline/tháng | $18,000 |

---

## Config 1 — Budget Bot

**Model:** Gemini 2.5 Flash-Lite ($0.10/$0.40 per 1M) · **Web:** OFF · **History:** Last 3 · **Classifier:** Keyword ($0)

| Item | Scenario A (4 turns) | Scenario B (7 turns) |
|---|---|---|
| Cost / conversation (avg) | $0.0010 | $0.0012 |
| Monthly cost | $9.00 | $43.07 |
| Human baseline | $4,500 | $18,000 |
| Rẻ hơn human | 500× | 417× |
| Savings % | 99.8% | 99.7% |

**Nhận xét:** Cost/conv siêu thấp ($0.0010) vì dùng Gemini 2.5 Flash-Lite, tắt toàn bộ Web Search và Keyword Classifier ($0). Tuy dưới mức $0.005 nhưng phép tính đã bao gồm đủ RAG và History Last 3. Mức tiết kiệm vô cùng ấn tượng so với human.

---

## Config 2 — Premium Concierge

**Model:** Claude Sonnet 4.6 ($3.00/$15.00 per 1M) · **Web:** ON selective (Visa, Weather, Guide) · **History:** Full · **Classifier:** GPT-4o-mini

| Item | Scenario A (4 turns) | Scenario B (7 turns) |
|---|---|---|
| Cost / conversation (avg) | $0.057 | $0.069 |
| Monthly cost | $513.95 | $2,490.43 |
| Human baseline | $4,500 | $18,000 |
| Rẻ hơn human | 8.75× | 7.22× |
| Savings % | 88.5% | 86.1% |

**Nhận xét:** Cost/conv khá cao nhưng vẫn dưới $0.10. Monthly B tốn gần $2,500 nhưng vẫn rẻ hơn human ~7×. Sự tăng vọt từ Scenario A sang B là do Full History — các turn sau trong 7 turns bị đội giá nặng (token accumulation).

---

## Config 3 — Smart Mix

**Model:** Haiku 4.5 ($1.00/$5.00) cho Visa + Flash-Lite ($0.10/$0.40) cho Guide/Weather · **Web:** ON selective (Visa, Weather) · **History:** Last 5 · **Classifier:** Keyword ($0)

| Item | Scenario A (4 turns) | Scenario B (7 turns) |
|---|---|---|
| Cost / conversation (avg) | $0.0159 | $0.0195 |
| Monthly cost | $143.10 | $702.00 |
| Human baseline | $4,500 | $18,000 |
| Rẻ hơn human | 31.5× | 25.6× |
| Savings % | 96.8% | 96.1% |

**Nhận xét:** Cost/conv nằm trong range $0.005–$0.10 — hợp lý. Smart Mix đắt hơn Budget Bot (~16×) vì Visa dùng Haiku 4.5 + web search ON, nhưng rẻ hơn Premium Concierge (~3.6×) vì Guide và Weather dùng Flash-Lite và history chỉ Last 5.

---

## Quality + Speed Estimate

| Config | Quality | Speed | Lý do |
|---|---|---|---|
| Budget Bot | Low | High | Model siêu rẻ, tắt web, history ngắn → tốc độ nhanh nhưng thông tin có thể outdated. |
| Premium Concierge | High | Med | Model xịn, bật web selective, Full History → chất lượng cao nhưng độ trễ tăng. |
| Smart Mix | Med-High | Med | Visa dùng Haiku 4.5 → chính xác; Guide dùng Flash-Lite → nhanh; web ON cho Visa+Weather thêm ~1s. |

---

## Bảng kiểm

- [x] Tất cả 3 configs đã có cost/conv + monthly cho cả 2 scenarios
- [x] Đã so sánh từng config với human baseline ($0.50/conv)
- [x] Có quality + speed estimate cho mỗi config
- [x] Đã sanity check — không có số quá lạ
