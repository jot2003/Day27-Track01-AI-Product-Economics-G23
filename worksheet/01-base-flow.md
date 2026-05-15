# 01 · Base Flow + Chốt 3 Knobs

> **Mục tiêu**: Hiểu chatbot hoạt động ra sao ở mức base (không chọn config gì) — và xác định 3 knobs nhóm sẽ tweak ở các bước sau.
>
> **Thời gian**: 7 phút (trong 15 phút phần Setup)

---

## Bước 1 — Đọc base flow trong cost reference card

Mở file `cost-reference-card.md` ở phần **2. Base Flow** — xem flow chatbot mặc định. Đây là cấu trúc mọi config sẽ build dựa trên.

Đọc xong, tự kiểm tra hiểu:

- Khi tourist gửi tin nhắn, AI làm gì đầu tiên?
- 5 intent dẫn đến 5 hành động khác nhau — hành động nào tốn LLM, hành động nào không?
- Sau khi route, AI ráp gì lại để generate response?

Nếu chưa hiểu → quay lại đọc lại 1 lần nữa. Đừng đi tiếp khi còn mơ hồ.

---

## Bước 2 — Vẽ lại flow theo cách hiểu của nhóm

Vẽ flow ra giấy hoặc trên bảng (1 thành viên vẽ, cả nhóm góp ý). Có thể dùng ASCII đơn giản:

```text
Tourist gửi tin nhắn (tiếng Anh)
          │
          ▼
┌─ INTENT CLASSIFICATION ────────────────────────────────────┐
│  Keyword matcher hoặc LLM classifier (tùy config)          │
│  → Visa/Policy | Guide/Destination | Weather/Event         │
│  → Tour/Booking | Complaint                                │
└──────┬──────────┬──────────┬──────────┬───────────────────┘
       ▼          ▼          ▼          ▼           ▼
     Visa       Guide     Weather   Booking     Complaint
       │          │          │          │           │
       ▼          ▼          ▼          ▼           ▼
  RAG + Web?    RAG       Web search  Handoff    Escalate
  (chọn lọc)  (KB đủ)   (real-time)   Sales      Manager
       │          │          │         ($0)        ($0)
       └──────────┴──────────┘
                  │
                  ▼
┌─ CONTEXT ASSEMBLY ─────────────────────────────────────────┐
│  System prompt (500 tokens)                                │
│  + Conversation history (Last 3 / Last 5 / Full — config) │
│  + RAG top-5 chunks (1,250 tokens)                         │
│  + Web search results (800 tokens — nếu bật)              │
│  + User message (80 tokens)                               │
└──────────────────────────┬────────────────────────────────┘
                           │
                           ▼
┌─ RESPONSE GENERATION ─────────────────────────────────────┐
│  Model tạo câu trả lời (Cheap / Mid / Strong / Mix)       │
│  Output: ~180 tokens → gửi lại tourist                   │
└───────────────────────────────────────────────────────────┘
```

Khi vẽ, đảm bảo flow có 4 điểm:

1. **Intent classification** — phân loại ý định
2. **Route theo intent** — 5 nhánh đi đâu (RAG / Web search / Handoff / Escalate)
3. **Context assembly** — ráp system prompt + history + RAG + web (nếu bật) + user msg
4. **Response generation** — model tạo câu trả lời

Nếu nhóm vẽ thiếu 1 trong 4 bước → bổ sung trước khi đi tiếp.

---

## Bước 3 — Xác định 3 Knobs

3 knobs là 3 quyết định thiết kế nhóm có thể tweak. Mỗi config nhóm thiết kế = 1 bộ chọn tại 3 knobs này.

Trước khi điền vào ô bên dưới, đọc nhanh mục **3. Decision Points** của `cost-reference-card.md`. Sau đó tự hỏi:

- Knob 1 — Model tier: model rẻ và model mạnh chênh bao nhiêu lần? Có thể mix theo intent không?
- Knob 2 — Web search: intent nào *cần* real-time? intent nào không cần?
- Knob 3 — History: 7 lượt chat cuối đắt hay rẻ? Cắt history có rủi ro gì?

### Knob 1 — Model tier

**Câu hỏi:** Chất lượng câu trả lời ở mức nào?

Options:

```text
□ Cheap        (Gemini Flash-Lite / DeepSeek V4 Flash / GPT-4o-mini)
□ Mid          (Gemini Flash / Claude Haiku 4.5)
□ Strong       (DeepSeek V4 Pro / Claude Sonnet 4.6)
□ Premium      (Claude Opus 4.7 / GPT-5.5)
□ Mix          (model khác nhau cho intent khác nhau — viết rõ)
```

**Câu hỏi gợi mở cho nhóm** (trả lời trước khi chọn):

- Mục tiêu chính là chi phí thấp hay chất lượng cao?
- Tourist hỏi câu phức tạp hay đơn giản hơn?
- Có nên dùng cheap cho phân loại + strong cho trả lời không?

```text
Nhóm nhận thấy các câu hỏi tourist có độ phức tạp rất khác nhau: Guide/FAQ đơn giản hơn, trong khi Visa đòi hỏi thông tin chính xác cao. Hướng đi chính là thử cả 3 mức — Cheap (tối thiểu chi phí), Strong (tối đa chất lượng), và Mix (cheap cho FAQ + strong cho Visa) — để so sánh tradeoff thực tế bằng số.
```

### Knob 2 — Web search

**Câu hỏi:** Có cần thông tin real-time không?

Options:

```text
□ OFF              (chỉ dùng RAG — knowledge base có sẵn)
□ ON selective    (bật cho 1–2 intent cần real-time: visa, weather)
□ ON broad         (bật cho hầu hết intent)
```

**Câu hỏi gợi mở:**

- Visa policy đổi mỗi tháng — RAG có đủ không?
- Weather là thông tin real-time tự nhiên — không có lựa chọn khác đúng không?
- Web search tốn $0.005/call + 800 tokens — bật bừa có lợi không?

```text
RAG đủ cho Guide/Destination vì thông tin điểm đến thay đổi chậm. Visa và Weather cần real-time — nếu tắt, chatbot có thể trả lời sai chính sách mới nhất. Bật web bừa cho tất cả intent sẽ đội chi phí không cần thiết: mỗi query thêm $0.008 + 800 tokens. Hướng selective (chỉ bật cho Visa + Weather) là phương án hợp lý nhất.
```

### Knob 3 — History management

**Câu hỏi:** Chatbot cần nhớ bao nhiêu context của conversation?

Options:

```text
□ Last 3 turns        (nhẹ nhất, dễ quên)
□ Last 5 turns        (cân bằng)
□ Full history        (nhớ tất cả, đắt nhất ở conv dài)
□ Summarize every 5   (nâng cao — cần 1 LLM call phụ để tóm tắt)
```

**Câu hỏi gợi mở:**

- Tourist hay nói "tôi đã nói budget là $500 ở turn 1" rồi turn 7 hỏi gợi ý — nếu quên thì sao?
- Scenario A trung bình 4 lượt → full history có tốn nhiều không?
- Scenario B trung bình 7 lượt → mỗi turn thêm 260 tokens — tổng thêm bao nhiêu?

```text
Ở Scenario B (7 turns), Full history nghĩa là turn 7 phải mang theo 6×260 = 1,560 tokens lịch sử thêm vào input — đắt đáng kể với model mạnh. Last 3 cắt nguy cơ mất ngữ cảnh đầu conversation (tourist nói budget $500 từ turn 1, đến turn 7 bot quên). Last 5 là điểm cân bằng hợp lý cho Smart Mix: đủ nhớ ngữ cảnh quan trọng mà không phình token quá mức.
```

---

## Bước 4 — Sơ bộ nhóm muốn thử những combo nào?

Chưa cần quyết định cuối cùng. Chỉ cần phác thảo: nhóm dự định thử ít nhất 3 combo khác nhau. Càng khác nhau, càng dễ thấy tradeoff.

**Combo 1 (định hướng cheap)**:

```text
Model: Gemini 2.5 Flash-Lite    Web: OFF    History: Last 3    (đặt tên dự kiến: Budget Bot)
```

**Combo 2 (định hướng premium)**:

```text
Model: Claude Sonnet 4.6    Web: ON selective (Visa + Weather)    History: Full    (đặt tên dự kiến: Premium Concierge)
```

**Combo 3 (định hướng balanced / smart mix)**:

```text
Model: Mix — Gemini Flash-Lite cho Guide/FAQ, Claude Haiku 4.5 cho Visa    Web: ON selective (Visa + Weather)    History: Last 5    (đặt tên dự kiến: Smart Mix)
```

**Combo 4** (optional — nếu nhóm có ý tưởng khác):

```text
(không thiết kế thêm — 3 combo đã đủ khác biệt để thấy tradeoff rõ ràng)
```

---

## Bảng kiểm trước khi sang file tiếp theo

- [x] Đã vẽ flow base có đủ 4 bước (Intent → Route → Context → Response)
- [x] Hiểu Booking + Khiếu nại = $0 LLM cost (chuyển con người)
- [x] Đã phác thảo ≥3 combo khác nhau (chưa cần chi tiết)
- [x] Nhóm đồng thuận về hướng đi mỗi combo

Xong → 10:25 chuyển sang **Main phase**. Mở `02-config-design.md`.
