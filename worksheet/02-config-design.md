# 02 · Configuration Design — 3 Configs

> **Mục tiêu**: Thiết kế ≥3 configurations chi tiết, mỗi config có tên + 3 knobs đã chốt + lý do chọn.

---

## Config 1 — Budget Bot

### 3 Knobs

| Knob | Lựa chọn | Chi tiết |
|---|---|---|
| **① Model** | Cheap | Gemini 2.5 Flash-Lite — $0.10/$0.40 per 1M tokens (input/output) |
| **② Web search** | OFF | Chỉ dùng RAG |
| **③ History** | Last 3 | Nhớ 3 lượt gần nhất |
| **Classifier** | Keyword | $0 |

### Lý do

Config này phục vụ tốt nhất khi volume cao đột biến (mùa cao điểm) hoặc cho các câu hỏi FAQ cơ bản với budget bị siết chặt. Trade-off là chi phí cực rẻ (tiết kiệm tối đa) nhưng câu trả lời có thể kém cập nhật thông tin theo thời gian thực (vì tắt web search). Khách hàng hỏi thông tin chung (guide, văn hóa) sẽ hài lòng, nhưng khách cần thông tin chính xác về thời tiết hay chính sách visa mới nhất có thể bị thất vọng.

### Rủi ro lớn nhất

Visa info có thể outdated vì web search OFF, và bot có thể quên ngữ cảnh nếu khách hàng chat quá dài (history Last 3).

---

## Config 2 — Premium Concierge

### 3 Knobs

| Knob | Lựa chọn | Chi tiết |
|---|---|---|
| **① Model** | Strong | Claude Sonnet 4.6 — $3.00/$15.00 per 1M tokens (input/output) |
| **② Web search** | ON selective | Bật cho Visa, Weather, Guide |
| **③ History** | Full | Nhớ toàn bộ conversation |
| **Classifier** | LLM (GPT-4o-mini) | $0.15/$0.60 per 1M tokens |

### Lý do

Config này tập trung vào trải nghiệm cao cấp nhất: sử dụng Strong model (Claude Sonnet 4.6) đảm bảo chất lượng, ngữ cảnh dài được giữ trọn vẹn với Full History. Việc bật Web Search selective giúp thông tin thực tế được cập nhật (đặc biệt Visa và Weather), nhắm vào phục vụ khách hàng VIP đòi hỏi sự chính xác tuyệt đối.

### Rủi ro lớn nhất

Chi phí hoạt động rất cao, dễ làm thâm hụt ngân sách nếu gặp volume cực lớn (Scenario B) do sử dụng Full History (token count phình to theo từng turn) kết hợp model đắt tiền.

---

## Config 3 — Smart Mix

### 3 Knobs

| Knob | Lựa chọn | Chi tiết |
|---|---|---|
| **① Model** | Mix | Claude Haiku 4.5 (Visa) — $1.00/$5.00 per 1M tokens; Gemini 2.5 Flash-Lite (Guide/Weather) — $0.10/$0.40 per 1M tokens |
| **② Web search** | ON selective | Bật cho Visa, Weather |
| **③ History** | Last 5 | Nhớ 5 lượt gần nhất |
| **Classifier** | Keyword | $0 |

### Lý do

Config này áp dụng nguyên tắc "dùng đúng mức trí thông minh cho đúng loại câu hỏi": intent phức tạp (Visa) dùng model mạnh hơn (Haiku 4.5), trong khi câu hỏi Guide và Weather đơn giản hơn xử lý bằng Flash-Lite rẻ hơn. Web search selective giữ thông tin Visa và thời tiết luôn fresh mà không bật bừa cho tất cả. Last 5 đủ nhớ ngữ cảnh hầu hết conversation (cả Scenario B 7 turns) mà không phình token như Full history.

### Rủi ro lớn nhất

Logic routing theo intent phức tạp hơn — nếu classifier nhận sai intent (nhầm câu hỏi Visa thành Guide), bot sẽ dùng Flash-Lite thay vì Haiku, dẫn đến câu trả lời kém chính xác cho thông tin nhạy cảm.

---

## Bảng kiểm

- [x] ≥3 configs đã đặt tên (không chỉ "Config 1/2/3")
- [x] Mỗi config đã chốt rõ 3 knobs
- [x] Mỗi config có ≥2 câu lý do
- [x] 3 configs đủ khác biệt — thấy rõ tradeoff
- [x] Nhóm đồng thuận đây là 3 configs đáng so sánh
