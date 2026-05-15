# 01 · Base Flow + 3 Knobs

> **Mục tiêu**: Xác định cấu trúc chatbot base và 3 knobs nhóm sẽ tweak để tạo ra các configs khác nhau.

---

## Base Flow

```
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

**Lưu ý quan trọng:** Booking + Complaint = handoff ngay lập tức → $0 LLM cost.

---

## 3 Knobs nhóm chọn

### Knob 1 — Model Tier

Các câu hỏi tourist có độ phức tạp rất khác nhau: Guide/FAQ đơn giản hơn, trong khi Visa đòi hỏi thông tin chính xác cao. Nhóm thử cả 3 mức — Cheap (tối thiểu chi phí), Strong (tối đa chất lượng), và Mix (cheap cho FAQ + strong cho Visa) — để so sánh tradeoff thực tế bằng số.

### Knob 2 — Web Search

RAG đủ cho Guide/Destination vì thông tin điểm đến thay đổi chậm. Visa và Weather cần real-time — nếu tắt, chatbot có thể trả lời sai chính sách mới nhất. Bật web bừa cho tất cả intent sẽ đội chi phí không cần thiết ($0.008/query + 800 tokens). Hướng selective (chỉ bật cho Visa + Weather) là phương án hợp lý nhất.

### Knob 3 — History Management

Ở Scenario B (7 turns), Full history nghĩa là turn 7 phải mang theo 6×260 = 1,560 tokens lịch sử thêm vào input — đắt đáng kể với model mạnh. Last 3 rẻ nhất nhưng có nguy cơ mất ngữ cảnh (tourist nói budget $500 từ turn 1, đến turn 7 bot quên). Last 5 là điểm cân bằng hợp lý: đủ nhớ ngữ cảnh quan trọng mà không phình token quá mức.

---

## 3 Combos dự kiến

| Config | Model | Web Search | History |
|---|---|---|---|
| **Budget Bot** | Gemini 2.5 Flash-Lite (all) | OFF | Last 3 |
| **Premium Concierge** | Claude Sonnet 4.6 (all) | ON selective (Visa + Weather) | Full |
| **Smart Mix** | Haiku 4.5 (Visa) + Flash-Lite (Guide/Weather) | ON selective (Visa + Weather) | Last 5 |

---

## Bảng kiểm

- [x] Đã vẽ flow base có đủ 4 bước (Intent → Route → Context → Response)
- [x] Hiểu Booking + Khiếu nại = $0 LLM cost (chuyển con người)
- [x] Đã phác thảo ≥3 combo khác nhau
- [x] Nhóm đồng thuận về hướng đi mỗi combo
