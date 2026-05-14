---
artifact: 2 — Cost research (provider pricing thực tế)
buoc: 1 — Cost Model
phase: Tra pricing + tính cost/task
time: 15 phút (xem deck slide 4 để biết khung giờ chính xác trong buổi)
input: 00-context.md + brief + 1-usage-unit.md + prompts/02-cost-formula.md
nop-cuoi: Không — file trung gian
---

# 2 — Cost Research: tra pricing thực tế + tính cost/task

Mục tiêu: tự tra pricing của provider AI, ước tính cost/task chính xác, tổng hợp các cost component (API + tooling + human review + setup).

Lý do làm bước này: bài giảng KHÔNG cho sẵn bảng giá. Trong thực tế, PM phải tự tra pricing — đây là kỹ năng bắt buộc.

Quy tắc: **không có pricing source URL = không có cost number**.

## Quy trình 15 phút

```text
5 phút  — Tra pricing 1-2 provider chính + ghi URL
5 phút  — Tính cost/task theo công thức tokens
5 phút  — Tổng hợp cost component (API + tooling + review + setup)
```

---

## Phần A — Pricing Research

### Bảng tham chiếu — Provider Pricing Reference

Bảng dưới là điểm khởi đầu nhanh. **Bắt buộc xác minh lại trên pricing page chính chủ** trước khi điền vào bảng tra dưới (giá có thể đổi).

| Provider | Model | Input ($/1M tokens) | Output ($/1M tokens) |
|---|---|---|---|
| Anthropic | Claude 3.5 Sonnet | $3.00 | $15.00 |
| OpenAI | GPT-4o | $2.50 | $10.00 |
| OpenAI | GPT-4o-mini | $0.15 | $0.60 |
| Google | Gemini 1.5 Pro | $1.25 | $5.00 |

> **Lưu ý**: số liệu trên là chuẩn 2025-Q1. Click trực tiếp pricing page của provider để xác minh trước khi điền vào assignment — pricing AI hay đổi (Salesforce đổi giá 3 lần trong 18 tháng).

### Provider chính (đã chọn trong 00-context.md phần 6)

**Provider**: [...]

**Model**: [...]

**Pricing URL nguồn**:

- [vd: <https://openai.com/api/pricing/>]
- [vd: <https://www.anthropic.com/pricing>]
- [Chụp screenshot nếu pricing page hay đổi]

### Bảng pricing tra được

Pull giá theo định dạng "USD per 1M tokens":

| Provider | Model | Input ($/1M tokens) | Output ($/1M tokens) | Note |
|---|---|---|---|---|
| [Provider 1] | [Model A] | $___ | $___ | [vd: standard tier] |
| [Provider 1] | [Model B] | $___ | $___ | [vd: cheaper tier] |
| [Provider 2] | [Model C] | $___ | $___ | [vd: backup option] |

**Model nhóm CHỌN cuối**: ___

**Lý do chọn**: [chất lượng / giá / latency / region / model gần phù hợp với task]

---

## Phần B — Cost Component khác (ngoài API)

Tra thêm các chi phí ngoài API:

### Vector DB / Embedding (nếu có RAG)

- Vector DB nhóm dùng: [Pinecone / Qdrant / Weaviate / pgvector / không cần]
- Giá: $___/tháng (gói nhỏ nhất cho pilot scale)
- URL: [...]

### Monitoring / Logging

- Tool: [Langfuse / Langsmith / Helicone / không cần]
- Giá: $___/tháng
- URL: [...]

### Orchestration / Workflow

- Tool: [n8n / Zapier / custom / không cần]
- Giá: $___/tháng
- URL: [...]

### Human review cost

- Mức lương người review (theo brief hoặc giả định): $___/giờ
- Số phút review/task: ___ phút
- Cost/review = (phút / 60) × $___/giờ = $___/task
- Lưu ý: nếu brief không cho lương, giả định loaded rate (lương + benefit + overhead) = 1.3-1.5× lương cơ bản.

### Setup cost (amortize)

- Setup gồm: integration developer time, security review, training, prompt engineering iteration.
- Ước tính setup 1 lần: $___ (vd: 1 engineer × 2 tuần = $8,000)
- Amortize đều cho thời gian pilot: $___ / ___ tháng = $___/tháng

---

## Phần C — Tính Cost/Task

### Step C1 — Token estimate

Ước tính token cho 1 lần chạy:

- **Input tokens** (prompt + context + system prompt): ___ tokens
  - Cách ước tính: 1 token ≈ 4 ký tự tiếng Anh / 1.5 từ tiếng Việt.
  - Vd: ticket dài 500 từ ≈ 750 tokens.
- **Output tokens** (response): ___ tokens
  - Vd: bản nháp reply 300 từ ≈ 400 tokens.

### Step C2 — API cost/task

Công thức:

```text
API cost/task = (input_tokens × input_price + output_tokens × output_price) / 1,000,000
```

Tính cho nhóm:

```text
API cost/task = (___ × $___ + ___ × $___) / 1,000,000
              = $___
              ≈ $0.0___ /task
```

### Step C3 — Tooling cost/task (nếu apportion theo task)

Nếu tooling tính tháng (vd: Pinecone $70/tháng), chuyển về cost/task:

```text
Tooling cost/task = Monthly tooling cost / Monthly volume
                  = $___ / ___ task
                  = $0.0___ /task
```

### Step C4 — Human review cost/task

(Đã tính ở phần B — Human review cost)

```text
Human review cost/task = $___ /task (= phút × hourly rate / 60)
```

### Step C5 — Tổng cost/task

```text
Total cost/task = API + tooling + human review
                = $___ + $___ + $___
                = $___ /task
```

---

## Phần D — Bảng tham chiếu (mức cost/task thông thường)

Sau khi tính, so sánh với mức cost/task thường gặp để sanity check:

| Loại task | Cost/task thông thường | Lý do |
|---|---|---|
| Classification đơn giản (label, route) | $0.001 - $0.01 | Token ngắn, model rẻ |
| Draft generation ngắn (1 reply) | $0.01 - $0.05 | Token vừa, model trung |
| Phân tích phức tạp (1 doc analyze) | $0.10 - $0.50 | Token dài, model mạnh |
| Multi-step agent (search + reason + act) | $0.50 - $5.00 | Nhiều API call/task |
| Long context (legal contract, full audit) | $1.00 - $20.00 | 100K+ tokens input |

**Cost/task của nhóm** = $___ /task

**Có hợp lý không** so với bảng trên? [Có / Không — nếu không, kiểm tra lại token estimate hoặc model chọn]

---

## Phần E — Kiểm chứng

Trước khi chuyển sang `3-FINAL-cost-model.md`, rà soát:

- [ ] Đã có URL pricing source cho mỗi provider.
- [ ] Đã chọn 1 model cụ thể (không "model nào đó").
- [ ] Cost/task tính ra số cụ thể (vd: $0.012), không "khoảng".
- [ ] Human review cost được include nếu brief yêu cầu human review.
- [ ] Tooling cost có ghi rõ provider + giá tháng + URL.
- [ ] Setup cost được amortize theo thời gian pilot (không tính cả 1 cục vào tháng 1).

---

## Phần F — Phản biện (push back AI tự bịa)

Nếu nhóm dùng AI để gợi ý pricing, kiểm tra lại:

- AI có thể bịa giá (đặc biệt model mới ra) — luôn click URL pricing trực tiếp.
- AI có thể nói "Claude 3.5 Sonnet $5/1M input" — sai. Click anthropic.com/pricing để xác minh.
- AI có thể bỏ sót cost component (vd: chỉ đếm API, quên human review).
- Nếu cost/task < $0.001 hoặc > $50 cho task trung bình → kiểm tra lại token estimate.

---

## Câu hỏi mở (cho Phase 3 — FINAL)

- Câu hỏi 1: Setup cost amortize bao nhiêu tháng là hợp lý cho brief này?
- Câu hỏi 2: Nhóm có muốn so sánh 2 model (vd: GPT-4o vs Claude 3.5) để check cost sensitivity không?
- Câu hỏi 3: [...]

Sau bước này, chuyển sang `3-FINAL-cost-model.md` để gộp toàn bộ vào bảng Section A của Economics Sheet.
