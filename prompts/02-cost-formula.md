# Prompt tham khảo 2 — Tính Cost Formula với Provider Pricing

**Dùng khi**: nhóm đã có usage unit, cần tự tra pricing thực tế + tính cost/task chính xác.
**Công cụ gợi ý**: Claude Sonnet/Opus, ChatGPT-4o (với web search), Perplexity Pro.
**Lưu kết quả vào**: `worksheet/01-cost-model/2-cost-research.md` + Section A.7 trong `3-FINAL-cost-model.md`
**Thời gian**: 15-20 phút

---

## Trước khi vào prompt — 5 câu hỏi nhóm tự trả lời

1. **Usage unit đã chốt là gì?** (Pull từ `1-usage-unit.md`).
2. **Token estimate đã có chưa?** (Input + output bao nhiêu tokens 1 lần chạy?)
3. **Provider candidate**: OpenAI / Anthropic / Google / Azure / Open source?
4. **Có RAG không** (vector DB, embedding cost)? Có monitoring không?
5. **Brief có constraint human review không** — nếu có, review time bao nhiêu phút?

> **Cảnh báo**: AI hay bịa pricing — đặc biệt với model mới hoặc model deprecated. Luôn click URL pricing page để verify.

---

## Prompt chính (paste sau `00-context.md` + `1-usage-unit.md`)

```text
Bạn là Product Manager AI có kinh nghiệm tính cost cho AI products.
Dựa trên BỐI CẢNH ở trên (00-context.md + usage unit đã định nghĩa),
giúp nhóm tôi tra pricing + tính Monthly AI Cost cho brief.

ĐIỀU KIỆN TRƯỚC: usage unit đã rõ. Tôi muốn tính cost từ A đến Z.

YÊU CẦU:

PHẦN 1 — Pricing Research:
Cho 3 model candidate phù hợp với usage unit:
- Model A (cheaper): tên model + input $/1M tokens + output $/1M tokens + URL pricing page
- Model B (mid-tier): [tương tự]
- Model C (premium): [tương tự]

Sau đó RECOMMEND model nào cho brief tôi:
- Lý do chọn (chất lượng vs giá vs latency).
- Nếu sai → cost sai thế nào (sensitivity).

CẢNH BÁO RÕ: nếu bạn không chắc chắn về 1 số tiền pricing, GHI RÕ "chưa verified, cần click URL".
Đừng bịa số.

PHẦN 2 — Token estimate:
Cho usage unit của tôi, estimate:
- Input tokens (prompt + context + system): ___ tokens (range hợp lý)
- Output tokens (response): ___ tokens
- Multi-step nếu có: tổng tokens cộng lại.

Sau đó tính cost/task = (input × in_price + output × out_price) / 1,000,000.

PHẦN 3 — Tooling cost:
Brief tôi có cần các tooling sau không? Nếu có, ước tính giá tháng + URL:
- Vector DB (cho RAG): cần / không cần
- Monitoring (Langfuse, Helicone): cần / không cần
- Orchestration (n8n, LangChain): cần / không cần
- Embedding API (nếu RAG): cần / không cần

PHẦN 4 — Human review cost:
Nếu brief có constraint human review:
- Reviewer hourly rate ước tính: $___/hr (loaded = base × 1.3-1.5)
- Review time/task: ___ phút (từ brief hoặc giả định)
- Cost/review = (phút / 60) × hourly rate
- Monthly review cost = monthly volume × cost/review.

PHẦN 5 — Setup cost (amortize):
Ước tính setup 1 lần ($):
- Integration: ___ engineer × ___ tuần × ___/tuần
- Security review: ___
- Prompt engineering iteration: ___
- Training cho user: ___

Amortize đều cho pilot duration → setup/month.

PHẦN 6 — Monthly Cost Formula:
Tổng hợp:
Monthly Cost = (volume × cost/task) + tooling + (volume × review cost) + setup amortize
            = $___ /month

PHẦN 7 — Budget check:
So với budget brief: ___% trong budget? Action nếu over budget?

YÊU CẦU FORMAT:
- Mỗi giá tiền phải có URL nguồn.
- Mỗi giả định (token estimate, review time) phải có lý do.
- Trả lời bằng tiếng Việt thoát nghĩa.

YÊU CẦU PHẢN BIỆN:
- Pricing model nào dễ "blow up" khi volume scale (vd: per-token model expensive khi context dài)?
- Có cost hidden nào nhóm tôi đang quên không?
- Cost/task có hợp lý so với industry benchmark không?
```

---

## Iterate — đẩy AI sâu hơn nếu output chưa đủ

### Khi AI đưa pricing có vẻ bịa

```text
Pricing bạn đưa cho Model X ($___/1M tokens) — tôi không click được URL bạn cite,
hoặc URL trả 404, hoặc pricing page không match.

Verify lại:
1. Click trực tiếp pricing page chính thức của provider (vd: openai.com/api/pricing,
   anthropic.com/pricing, cloud.google.com/vertex-ai/pricing).
2. Ghi rõ "as of [ngày kiểm tra]" — pricing đổi thường xuyên.
3. Nếu pricing có tier (vd: 0-10M tokens, 10M+) → ghi rõ tier nhóm tôi rơi vào.
4. Nếu provider có enterprise discount (cần contract) → ghi rõ "list price, enterprise có thể negotiate ___-___%".

Đừng đưa số mà không có URL working.
```

### Khi muốn so sánh 2-3 model

```text
Tính cost cho 3 model candidate ở pilot scale (volume = ___ tasks/month):

| Model | Cost/task | Monthly API cost | % of budget |
|---|---|---|---|
| Cheap (vd: GPT-4o-mini) | $___ | $___ | ___% |
| Mid (vd: GPT-4o, Claude 3.5 Sonnet) | $___ | $___ | ___% |
| Premium (vd: Claude 3 Opus, GPT-4.5) | $___ | $___ | ___% |

Recommend model phù hợp dựa trên:
- Budget headroom (cost <50% budget = safe).
- Quality cần thiết cho usage unit.
- Latency cần thiết (model lớn thường chậm hơn).

Nếu cheap model quality đủ → chọn cheap. Đừng default premium.
```

### Khi muốn break down theo cost component

```text
Cost/month nhóm tôi tính ra = $___. Break down theo % các component:

| Component | $/month | % |
|---|---|---|
| API cost | $___ | ___% |
| Tooling (vector DB + monitoring + ...) | $___ | ___% |
| Human review cost | $___ | ___% |
| Setup (amortized) | $___ | ___% |

Phân tích:
- Component nào dominate (>50%)? Đó là cost driver chính → tối ưu nó trước.
- Component nào nhỏ (<5%)? Không cần tập trung optimize.
- Có component nào surprising (cao hoặc thấp ngoài dự đoán)?
```

---

## Phản biện sau khi có output — 5 câu nhóm tự hỏi

1. **URL check**: mỗi giá tiền có URL working pricing page không?
2. **Token check**: token estimate có realistic cho usage unit của nhóm không?
3. **Hidden cost check**: có quên human review / setup / monitoring không?
4. **Sanity check**: cost/task có rơi trong range typical (xem bảng tham chiếu trong `2-cost-research.md` Phần D)?
5. **Budget check**: total monthly cost trong budget brief không? Nếu over, có hành động cụ thể?

---

## Ví dụ tốt vs ví dụ chưa tốt

### Chưa tốt

> "Cost/task khoảng $0.01. Monthly cost khoảng $500."

Vấn đề: không có công thức, không có URL, không có breakdown.

### Tốt

> **Model**: Claude 3.5 Sonnet (Anthropic). Pricing: $3/1M input, $15/1M output. Source: <https://www.anthropic.com/pricing>, accessed 2026-05-14.
>
> **Token estimate**:
>
> - Input: 800 tokens (ticket text 500 + 3 KB articles 300).
> - Output: 400 tokens (draft reply 300 từ).
>
> **Cost/task**: (800 × $3 + 400 × $15) / 1,000,000 = $0.0024 + $0.006 = **$0.0084 /task**.
>
> **Monthly volume**: 5 agent / 25 × 800 ticket × 22 ngày = **3,520 task/month**.
>
> **Monthly API cost**: 3,520 × $0.0084 = **$29.57**.
>
> **Tooling**: Pinecone (vector DB) $70/mo + Langfuse $50/mo = **$120/month**. Source: pricing pages.
>
> **Human review**: 3,520 task × 3 min review × ($25/hr / 60) = **$1,320/month**. (Loaded rate = $20 base × 1.25 = $25.)
>
> **Setup**: 1 engineer × 2 tuần × $2,000/tuần = $4,000. Amortize over 90-day pilot (3 tháng) = **$1,333/month**.
>
> **Total Monthly Cost**: $30 + $120 + $1,320 + $1,333 = **$2,803/month**.
>
> **Budget check**: $2,803 / $5,000 = 56% of budget — within budget ✓.

---

## Anti-pattern khi prompt — tránh

| Đừng làm | Nên làm |
|---|---|
| Hỏi "Cost bao nhiêu?" | Đưa usage unit + volume + brief, request từng component |
| Chấp nhận pricing AI đưa | Click URL, verify từng giá |
| Quên human review cost | Nếu constraint review → đây là phần lớn cost |
| Setup = $0 | Setup luôn có (integration + prompt engineering) |
| Round numbers ($100, $500) | Số chính xác từ công thức (vd: $2,803) |
| Pricing không "as of date" | Pricing đổi thường → ghi ngày check |

---

## Format save vào `2-cost-research.md` Phần A + Phần C

```markdown
## Phần A — Pricing Research

[Paste bảng pricing 3 model + recommend model + URL]

## Phần C — Tính Cost/Task

### Step C1 — Token estimate
[Paste]

### Step C2 — API cost/task
[Paste công thức + số]

### Step C3 — Tooling cost/task
[Paste]

### Step C4 — Human review cost/task
[Paste]

### Step C5 — Tổng cost/task
[Paste]
```

---

## Câu hỏi mở rộng — nâng cao phản biện (optional)

```text
Sau khi tính cost, giúp tôi nhìn 3 góc khác:

1. **Cost sensitivity**: nếu volume × 5 (pilot → mở rộng team), cost component nào tăng tuyến tính,
   component nào có "step" jump (vd: vượt enterprise tier)?

2. **Provider comparison**: ngoài provider chính, có alternative nào rẻ hơn 50%+ không?
   - Open source via Replicate / Together AI?
   - Self-hosted (yêu cầu GPU)?
   - Trade-off (quality, latency, support)?

3. **Cost optimization opportunity**:
   - Cache (lưu kết quả AI cho input lặp lại) — giảm cost bao nhiêu %?
   - Smaller model cho easy task, big model cho hard task (tiered)?
   - Batch processing thay vì real-time?

Trả lời 3 góc này để chuẩn bị cho Step 3 Stress Test (provider shock scenario).
```

3 câu này giúp nhóm thấy cost không cố định — có nhiều lever để tối ưu khi stress test ROI.
