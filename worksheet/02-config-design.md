# 02 · Configuration Design — Đặt tên + Chốt knobs cho ≥3 Configs

> **Mục tiêu**: Biến phác thảo ở `01-base-flow.md` thành ≥3 configurations chi tiết, mỗi config có tên + 3 knobs đã chốt + lý do chọn.
>
> **Thời gian**: 15 phút (đầu phần Main, trước khi tính cost)

---

## Tại sao đặt tên + viết lý do?

Khi present, nhóm sẽ nói "Config 1, Config 2, Config 3" → người nghe sẽ chán ngay. Đặt tên gợi mở (Budget Bot, Premium Concierge, Smart Mix...) giúp memorable + cho thấy nhóm hiểu rõ tradeoff. Viết lý do giúp nhóm tự kiểm tra: "Mình chọn config này vì lý do gì? Có justify được không?"

---

## Cách điền

Với mỗi config: đặt tên + chốt 3 knobs + viết 2–3 câu lý do chọn. Mỗi câu lý do phải gắn với 1 tình huống thực tế (volume thấp / khách hỏi visa nhiều / budget bị siết...).

Tham khảo bảng pricing chi tiết tại `cost-reference-card.md` mục **3. Decision Points**.

---

## Config 1

**Tên config** (gợi mở: "Budget Bot", "Bare Minimum", "Lean Mode", "Night Mode" — đặt tên có cá tính):

```text
Budget Bot
```

### 3 Knobs

**① Model tier**:

```text
Response model: Gemini 2.5 Flash-Lite → giá $0.10 / $0.40  per 1M tokens (input/output)
Classifier model: Keyword → giá $0 / $0  per 1M tokens (hoặc keyword = $0)
```

**② Web search**:

```text
☑ OFF
□ ON selective — bật cho intent: __________________
□ ON broad
```

**③ History management**:

```text
☑ Last 3
□ Last 5
□ Full
□ Summarize every ___ turns
```

### Lý do nhóm chọn config này

Trước khi viết, tự hỏi:

- Config này phục vụ tình huống nào tốt nhất? (mùa thấp điểm? night-time? volume cao đột biến?)
- Trade-off chính là gì? (Rẻ nhưng kém chất lượng? Đắt nhưng chính xác?)
- Khách hàng nào sẽ hài lòng nhất với config này? Khách nào sẽ thất vọng?

```text
Config này phục vụ tốt nhất khi volume cao đột biến (như mùa cao điểm) hoặc cho các câu hỏi FAQ cơ bản với budget bị siết chặt. Trade-off là chi phí cực rẻ (tiết kiệm tối đa) nhưng câu trả lời có thể kém cập nhật thông tin theo thời gian thực (vì tắt web search). Khách hàng hỏi thông tin chung (guide, văn hóa) sẽ hài lòng, nhưng khách cần thông tin chính xác về thời tiết hay chính sách visa mới nhất có thể bị thất vọng.
```

### Rủi ro lớn nhất của config này

```text
Visa info có thể outdated vì web search OFF, và bot có thể quên ngữ cảnh nếu khách hàng chat quá dài (history Last 3).
```

---

## Config 2

**Tên config**:

```text
Premium Concierge
```

### 3 Knobs

**① Model tier**:

```text
Response model: Claude Sonnet 4.6 → giá $3.00 / $15.00  per 1M tokens
Classifier model: GPT-4o-mini → giá $0.15 / $0.60  per 1M tokens (LLM Classifier)
```

**② Web search**:

```text
□ OFF
☑ ON selective — bật cho intent: Visa, Weather, Guide
□ ON broad
```

**③ History management**:

```text
□ Last 3
□ Last 5
☑ Full
□ Summarize every ___ turns
```

### Lý do nhóm chọn config này

```text
Config này tập trung vào trải nghiệm cao cấp (Premium) nhất, sử dụng Strong model (Claude Sonnet 4.6) đảm bảo chất lượng, ngữ cảnh dài được giữ trọn vẹn với Full History. Việc bật Web Search selective giúp thông tin thực tế được cập nhật (đặc biệt Visa và Weather), nhắm vào phục vụ khách hàng VIP đòi hỏi sự chính xác tuyệt đối.
```

### Rủi ro lớn nhất của config này

```text
Chi phí hoạt động sẽ rất cao, dễ làm thâm hụt ngân sách nếu gặp volume cực lớn (Scenario B) do sử dụng Full History (token count phình to theo từng turn) kết hợp model đắt tiền.
```

---

## Config 3

**Tên config**:

```text
Smart Mix
```

### 3 Knobs

**① Model tier**:

```text
Response model (Visa intent): Claude Haiku 4.5 → giá $1.00 / $5.00 per 1M tokens
Response model (Guide/Weather intent): Gemini 2.5 Flash-Lite → giá $0.10 / $0.40 per 1M tokens
Classifier model: Keyword → giá $0 / $0 per 1M tokens (keyword = $0)
```

**② Web search**:

```text
□ OFF
☑ ON selective — bật cho intent: Visa, Weather
□ ON broad
```

**③ History management**:

```text
□ Last 3
☑ Last 5
□ Full
□ Summarize every ___ turns
```

### Lý do nhóm chọn config này

```text
Config này áp dụng nguyên tắc "dùng đúng mức trí thông minh cho đúng loại câu hỏi": intent phức tạp (Visa) dùng model mạnh hơn (Haiku 4.5), trong khi câu hỏi Guide và Weather đơn giản hơn có thể xử lý bằng Flash-Lite rẻ hơn. Web search selective giữ thông tin Visa và thời tiết luôn fresh mà không bật bừa cho tất cả. Last 5 đủ nhớ ngữ cảnh hầu hết conversation (cả Scenario B 7 turns) mà không phình token như Full history.
```

### Rủi ro lớn nhất của config này

```text
Logic routing theo intent phức tạp hơn — nếu classifier nhận sai intent (ví dụ: nhầm câu hỏi Visa thành Guide), bot sẽ dùng Flash-Lite thay vì Haiku, dẫn đến câu trả lời kém chính xác cho thông tin nhạy cảm.
```

---

## Config 4 (optional — nếu thời gian dư)

Nhóm có thể thiết kế thêm config thứ 4 để có thêm điểm so sánh. Không bắt buộc.

**Tên config**:

```text
(điền tên vào đây)
```

### 3 Knobs

```text
Model: ___    Web: ___    History: ___
```

### Lý do

```text
(điền 1–2 câu)
```

---

## Bảng kiểm trước khi tính cost

- [ ] ≥3 configs đã đặt tên (không chỉ "Config 1/2/3")
- [ ] Mỗi config đã chốt rõ 3 knobs (không còn ô trống)
- [ ] Mỗi config có ≥2 câu lý do
- [ ] 3 configs đủ khác biệt — không phải chỉ đổi mỗi 1 knob nhỏ
- [ ] Nhóm đồng thuận đây là 3 configs đáng so sánh

**Nếu 3 configs quá giống nhau** (chỉ đổi model, knobs khác giống hệt) → quay lại tweak. Mục đích là thấy tradeoff — configs giống nhau quá → không thấy tradeoff.

Xong → mở `03-cost-calculation.md` để bắt đầu tính cost.
