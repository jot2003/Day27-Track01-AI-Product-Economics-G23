# Prompt tham khảo 4 — Chốt Pricing Model + Value Metric

**Dùng khi**: nhóm đã định vị trên ma trận, cần chốt pricing model cụ thể (seat / usage / outcome / hybrid) + value metric (khách trả tiền cho gì).
**Công cụ gợi ý**: Claude Sonnet/Opus, ChatGPT-4o.
**Lưu kết quả vào**: `worksheet/02-pricing-value/2-pricing-model-choice.md` + Section B trong `3-FINAL-pricing-value-roi.md`
**Thời gian**: 10-15 phút

---

## Trước khi vào prompt — 5 câu hỏi nhóm tự trả lời

1. **Quadrant đã chốt** (từ prompt 3): vị trí ___ + ___
2. **Buyer trong brief là ai** (field #6 — Decision needed): CTO / VP Sales / Director / Managing Partner?
3. **Cost/task đã tính** (từ Cost Model): nếu pricing usage-based, phải > cost/task + margin.
4. **User có thể self-limit không** (vd: agent có thể "lười không click AI" → Usage Anxiety risk)?
5. **Buyer expectation về cost predictability**: muốn flat (predictable) hay variable (pay-as-you-grow)?

> **Cảnh báo**: chọn pricing model không phải dựa trên "trending" — phải dựa trên 4 yếu tố: quadrant, buyer, cost structure, user behavior.

---

## Prompt chính (paste sau output của prompt 3)

```text
Bạn là Pricing Strategy expert cho AI products.
Dựa trên BỐI CẢNH ở trên (brief + cost model + quadrant Attribution-Autonomy),
giúp nhóm tôi CHỐT pricing model + value metric cụ thể.

YÊU CẦU:

PHẦN 1 — Pricing Model Choice:
4 model chính:
- Seat / Flat: $X/user/month cố định
- Usage-based: $X / unit volume
- Outcome-based: $X / outcome thực tế
- Hybrid: Seat base + Usage credits, hoặc Tier outcome

Chọn 1 model + giải thích vì sao (so với 3 model khác):
- Lý do quadrant: model nào tự nhiên với quadrant nhóm tôi?
- Lý do buyer: buyer (CTO/VP) sẽ approve model nào dễ hơn?
- Lý do cost structure: cost/task cao hay thấp → model nào sustain?

Đề xuất giá cụ thể:
- Vd: "$25/seat/month + 1,000 credits/seat, $0.05/extra credit"
- Vd: "$0.05/draft, no minimum"
- Vd: "$1.50/resolution, billed monthly"

CẢNH BÁO: pricing usage hoặc outcome PHẢI > cost/task + margin (>= 2-3× cost để có gross margin healthy).

PHẦN 2 — Value Metric Choice:
Value metric = đơn vị khách trả tiền cho.

Đề xuất 3 value metric candidate, test mỗi cái qua 3-part test:
- Countable: customer đo được unit này?
- Meaningful to buyer: buyer hiểu unit này quan trọng?
- Tied to AI value: AI value tăng → metric tăng?

Chọn 1 + lý do.

PHẦN 3 — Buyer + Buying Trigger:
- Buyer là ai (role)?
- Buyer hiện đang spend ngân sách gì cho problem này (alternative cost)?
- Pricing đề xuất so với alternative (hire thêm người? outsource?)?
- Buying trigger: vì sao buyer quyết định mua HÔM NAY?

PHẦN 4 — Usage Anxiety Risk:
Nếu pricing có usage element:
- User cuối có thấy cost mỗi lần dùng không?
- User có khả năng self-limit (không dùng AI vì sợ bill) không?
- Risk: Low / Medium / High
- Mitigation: cap usage trong tier, hide individual cost, free exploration quota, etc.

PHẦN 5 — Sensitivity Analysis:
Nếu pricing giảm 30% (đối thủ rẻ hơn) → margin còn lại?
Nếu cost/task tăng 50% (provider shock) → margin còn lại?
Nếu adoption thấp 50% → revenue per pilot bao nhiêu?

YÊU CẦU FORMAT:
- Trả lời tiếng Việt thoát nghĩa.
- Mỗi đề xuất có lý do cụ thể (không "feeling").

YÊU CẦU PHẢN BIỆN:
- Pricing model có conflict với buyer expectation không?
- Value metric có defendable trong khâu Sales / customer kickoff không?
- Có alternative pricing model nào cũng work, lý do không chọn?
```

---

## Iterate — đẩy AI sâu hơn nếu output chưa đủ

### Khi muốn so sánh 2 pricing model

```text
2 pricing model đều hợp lý cho brief tôi:
- Option A: [vd: $25/seat unlimited]
- Option B: [vd: $1.50/outcome]

So sánh chi tiết:

| Lens | Option A (Seat) | Option B (Outcome) |
|---|---|---|
| Predictable cost cho buyer | ✓ | ✗ (variable) |
| Defend ROI (AI rõ ràng tạo value) | ✗ (khó tách) | ✓ (per outcome rõ) |
| Risk Usage Anxiety | Low | Medium (user lo cost) |
| Sale complexity | Simple | Complex (cần educate) |
| Margin scaling khi pilot scale | Linear with users | Linear with outcomes |
| Buyer (CTO) approve dễ | ✓ Predictable | ✗ Variable |
| ROI defendable cho CFO | ✗ "Bao gồm trong seat" | ✓ "Per outcome rõ" |

Recommend: Option ___ vì ___.

Hoặc cân nhắc Hybrid: $20/seat (base) + $0.50/outcome khi vượt 100 outcome/month.
Hybrid balance được predictability + ROI defendability.
```

### Khi gặp pricing không khả thi với cost

```text
Pricing nhóm tôi đề xuất = $0.05/task, nhưng cost/task = $0.04.

Margin = 25% — không đủ healthy cho SaaS B2B (thường cần >= 70-80% gross margin).

Options:
A. Tăng pricing lên $0.15/task (3× cost) → margin 73%. Risk: khách thấy đắt?
B. Giữ $0.05/task nhưng đặt minimum monthly fee $500 (bundle 10K task) → effective price ~$0.07/task average.
C. Đổi sang seat-based ($25/user) cover cost + margin.

Tính từng option:
- Option A: revenue = volume × $0.15 = $___. Margin = $___. Acceptable?
- Option B: revenue = $500 min × user = $___. Effective margin?
- Option C: revenue = user × $25 = $___. Defendable so với cost?

Recommend option nào defend được trong buyer kickoff?
```

### Khi muốn align với buyer

```text
Buyer trong brief = ___ (role).

Pricing đề xuất của nhóm tôi: ___.

Buyer thường lo lắng:
- CTO: "Cost có scale với usage không? Variable cost = ngân sách khó plan."
- CFO: "ROI defendable không? Có thể tie với business KPI không?"
- VP Operations: "Adoption có tăng theo design không? Usage Anxiety?"
- Managing Partner (law firm): "Per case billable? Recovery from client?"

Pricing đề xuất CÓ tackle lo lắng của buyer không?
Nếu KHÔNG → revise pricing để align hơn.

Vd: brief #4 (Legal) — Managing Partner thích outcome-based (per contract) vì có thể bill lại client. Seat-based khó pass-through.
```

---

## Phản biện sau khi có output — 5 câu nhóm tự hỏi

1. **Pricing model rõ ràng** (1 trong 4 nhóm, có giá cụ thể)?
2. **Value metric** pass 3-part test (countable, meaningful, tied to AI)?
3. **Buyer alignment**: buyer dễ approve pricing này không?
4. **Margin healthy**: pricing > cost × 2-3 (gross margin)?
5. **Usage Anxiety mitigation**: nếu Hybrid hoặc Usage → có mitigation cụ thể?

---

## Ví dụ tốt vs ví dụ chưa tốt

### Chưa tốt

> "Pricing: usage-based, $0.01/call. Đây là model phổ biến cho AI."

Vấn đề: không justify, không link với buyer, không check margin (cost/task có thể > $0.01).

### Tốt

> **Brief #4 — Legal Contract Reviewer**
>
> **Pricing model**: Hybrid Seat + Outcome
> - **Base**: $200/lawyer/month
> - **Outcome**: $5/contract reviewed (đầu tiên 50 contract/month free, sau đó tính)
> - **Total cho pilot scale (3 lawyer × 200 contract / month)**: $600 base + $750 outcome (= $5 × 150 over-cap) = $1,350/month
>
> **Lý do chọn Hybrid**:
> - Buyer (Managing Partner) thích outcome (per contract → bill back to client trong M&A engagement).
> - Base $200/seat đảm bảo predictable cost cho lawyer luôn có access (không Usage Anxiety).
> - 50 free contract/seat tránh bottleneck initial — lawyer dùng thoải mái.
> - Margin: cost/contract = $1.20 (tokens) + $0.50 (vector DB) = $1.70. Pricing $5 → 65% gross margin. Healthy.
>
> **Value metric**: 1 contract reviewed (countable ✓, meaningful to MP ✓, tied to AI ✓ — AI output là issue list per contract).
>
> **Real-world analog**: Harvey AI ($500-$1000/seat) — pure seat, nhưng do Harvey scope rộng hơn. Brief tôi narrow hơn → hybrid để fit.
>
> **Usage Anxiety**: Low. Base $200 + 50 free contract = lawyer không bị "đếm từng contract". Chỉ over-cap mới tính extra.

---

## Anti-pattern khi prompt — tránh

| Đừng làm | Nên làm |
|---|---|
| Chọn pricing "trending" (vd: outcome vì hot) | Justify từ quadrant + buyer + cost |
| Pricing < cost/unit | Pricing >= 2-3× cost cho margin healthy |
| Bỏ Buyer perspective | Buyer dễ approve không? |
| Skip Usage Anxiety check ở Hybrid | Mọi pricing có usage element → check anxiety |
| Round numbers ($10, $50, $100) | Số phản ánh research (vd: $25 vì Cursor; $1.50 vì Zendesk) |

---

## Format save vào `2-pricing-model-choice.md`

```markdown
## Phần A — Pricing Model Choice
[Paste model + giá + lý do]

## Phần B — Value Metric
[Paste metric + 3-part test]

## Phần C — Buyer + Buying Trigger
[Paste]

## Phần D — Usage Anxiety Check
[Paste]
```

---

## Câu hỏi mở rộng — nâng cao phản biện (optional)

```text
Sau khi chốt pricing, giúp tôi nhìn 3 angle STRATEGIC:

1. **Pricing evolution**: pilot → production → mature, pricing có change?
   - Pilot: discount 50% để get adoption.
   - Production: full price.
   - Mature: pricing power increase nếu là moat?

2. **Competitive pricing**: 1 đối thủ ra mắt với giá 50% cheaper, react thế nào?
   - Match: lose margin.
   - Differentiate: emphasize quality/integration → keep price.
   - Bundle: add features to justify premium.

3. **Buyer journey**: từ awareness → trial → purchase, pricing đóng vai trò gì ở mỗi giai đoạn?
   - Free trial (14 ngày, 100 task)? Free tier (10 task/month forever)?
   - Self-serve hay sale-led? Pricing có hiển thị công khai không?

Trả lời 3 câu này giúp brief có pricing strategy đầy đủ, không chỉ "1 con số".
```
