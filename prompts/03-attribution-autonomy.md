# Prompt tham khảo 3 — Attribution × Autonomy Positioning

**Dùng khi**: nhóm đã có Cost Model, bắt đầu Step 2 — cần định vị AI product trên ma trận 2×2 để chọn pricing model phù hợp.
**Công cụ gợi ý**: Claude Sonnet/Opus, ChatGPT-4o, Gemini 1.5 Pro.
**Lưu kết quả vào**: `worksheet/02-pricing-value/1-attribution-autonomy.md`
**Thời gian**: 10-15 phút

---

## Trước khi vào prompt — 5 câu hỏi nhóm tự trả lời

1. **Usage unit** đã chốt là gì? (Quan trọng vì autonomy + attribution đánh giá theo unit.)
2. **Trong brief, AI tự làm xong việc hay chỉ hỗ trợ?** (Đọc lại field #5 — constraint).
3. **Output AI có visible với end user** (vd: customer thấy AI reply) hay invisible (chỉ team thấy)?
4. **Có thể nói "AI làm được X" không** (cụ thể), hay chỉ "AI giúp team làm X"?
5. **Brief có 100% human review** → autonomy auto thấp.

> **Cảnh báo**: AI có thể đặt sai vị trí (vd: high autonomy cho brief có constraint review). Tự kiểm tra logic dựa trên brief.

---

## Prompt chính (paste sau `00-context.md` + Cost Model output)

```text
Bạn là Product Strategist AI có kinh nghiệm về pricing models.
Dựa trên BỐI CẢNH ở trên (brief + usage unit + cost model), giúp nhóm tôi:

1. ĐỊNH VỊ AI product trên Ma trận ATTRIBUTION × AUTONOMY.
2. SUGGEST pricing model phù hợp tự nhiên.
3. VALIDATE với real-world analog.

CONTEXT MA TRẬN:
- Autonomy: AI tự làm xong (high) vs hỗ trợ human (low)
- Attribution: rõ AI là cause (high) vs khó tách phần đóng góp (low)

Quadrant → pricing tự nhiên:
- Low Auto + Low Attrib  → Seat/Flat (Grammarly, Slack AI)
- Low Auto + High Attrib → Hybrid Seat+Credits (Cursor, Canva)
- High Auto + Low Attrib → Usage-based (OpenAI API, AWS)
- High Auto + High Attrib → Outcome-based (Intercom Fin, Chargeflow)

YÊU CẦU:

PHẦN 1 — Autonomy assessment:
Cho brief tôi, AI thuộc:
- Low: ___ (assists human, human ra quyết định cuối)
- High: ___ (AI tự ra quyết định / hành động)

Justification 2-3 câu dựa trên:
- Constraint trong brief (field #5)
- Risk boundary (field #9)
- Workflow (field #2)

CẢNH BÁO: nếu brief có "100% human review" hoặc "agent must approve" → KHÔNG được high autonomy.

PHẦN 2 — Attribution assessment:
Cho usage unit của tôi, attribution:
- Low: khó tách AI khỏi team effort (vd: AI giúp team viết → kết quả là "team viết tốt")
- High: rõ AI là cause (vd: AI flag 1 clause → rõ AI tạo flag)

Justification 2-3 câu.

PHẦN 3 — Quadrant:
- Autonomy: ___
- Attribution: ___
- Quadrant: ___

Pricing tự nhiên cho quadrant này: ___

PHẦN 4 — Real-world analog:
Tìm 2 sản phẩm AI thật trong cùng quadrant (cùng domain hoặc cross-domain):
- Sản phẩm A: tên + pricing + URL
- Sản phẩm B: tên + pricing + URL

Có pattern chung không? Pricing họ chọn có gợi ý gì cho nhóm tôi?

PHẦN 5 — Edge case check:
Brief có rơi vào "medium" (vừa low vừa high) không? Nếu có:
- Nghiêng về Low hay High Autonomy → vì constraint nào?
- Nghiêng về Low hay High Attribution → vì pattern nào?

Recommend: Hybrid pricing (Seat + Usage) thường là default cho "medium" position.

YÊU CẦU FORMAT:
- Trả lời bằng tiếng Việt thoát nghĩa.
- Mỗi assessment có justification cụ thể, không chỉ "tôi nghĩ".

YÊU CẦU PHẢN BIỆN:
- Nếu nhóm tôi chọn high autonomy nhưng brief có review constraint → flag inconsistency.
- Nếu nhóm tôi chọn high attribution nhưng buyer khó measure → flag risk.
- Nếu pricing model gợi ý không khớp với buyer (CTO vs CFO) → flag friction.
```

---

## Iterate — đẩy AI sâu hơn nếu output chưa đủ

### Khi muốn cross-check vị trí với analog

```text
Vị trí bạn assign cho brief tôi là [Auto ___ + Attrib ___] = quadrant ___.

Cross-check với 3 sản phẩm:

1. [Sản phẩm cụ thể trong cùng domain, vd: Zendesk AI cho support]
   - Vị trí của họ trên ma trận: [...]
   - Pricing họ chọn: [...]
   - Có khớp với quadrant tôi không?

2. [Sản phẩm khác domain nhưng cùng pattern, vd: Harvey AI cho legal]
   - [tương tự]

3. [Sản phẩm có constraint tương tự nhóm tôi, vd: brief có review constraint → tìm AI product có review constraint]
   - [tương tự]

Nếu cả 3 analog đều ở Low Auto + Low Attrib và pricing seat-based → confirm cho brief tôi.
Nếu phân tán → review lại justification.
```

### Khi muốn challenge autonomy assessment

```text
Tôi assess autonomy = HIGH, nhưng brief có constraint "agent must review before send".

Có inconsistency không?
- Nếu agent always review → AI không thực sự autonomous → nên là LOW.
- Nếu agent review chỉ 50% case → có thể medium → đánh giá lại.
- Nếu agent review chỉ tier-1 case → còn lại auto → split: tier-1 = low auto, tier-2+ = high auto?

Recommend: brief đa số là LOW autonomy do constraint compliance. Đừng đánh giá high vì "AI làm phần lớn việc" — review = quyết định cuối.
```

### Khi muốn lựa chọn giữa pricing model

```text
Quadrant của tôi = ___ → pricing tự nhiên = ___.

Nhưng có 2 alternative model cũng hợp lý:
- Alternative A: [tên model], lý do hợp lý
- Alternative B: [tên model], lý do hợp lý

So sánh 3 model qua 4 lens:
| Lens | Pricing tự nhiên | Alternative A | Alternative B |
|---|---|---|---|
| Buyer dễ approve? | | | |
| Predictable cost? | | | |
| Defend được ROI? | | | |
| Risk Usage Anxiety? | | | |

Recommend cuối: ___ với lý do ___.
```

---

## Phản biện sau khi có output — 5 câu nhóm tự hỏi

1. **Autonomy check**: low autonomy có khớp với constraint trong brief không?
2. **Attribution check**: high attribution có defendable không (buyer measure được AI value)?
3. **Quadrant clarity**: vị trí có clear, không "ở giữa cả 4"?
4. **Analog check**: real-world analog có cùng quadrant không?
5. **Pricing makes sense**: pricing model gợi ý có khớp với buyer + cost structure không?

---

## Ví dụ tốt vs ví dụ chưa tốt

### Chưa tốt

> "AI Support Copilot là high autonomy + high attribution → outcome-based."

Vấn đề: brief có constraint "no auto-send" → KHÔNG thể high autonomy.

### Tốt

> **Brief #1 — AI Support Copilot**
>
> **Autonomy**: LOW.
> - Justification: brief field #5 nói "no auto-send to customer (legal/compliance)". Agent senior review trước khi send. AI hỗ trợ draft, agent ra quyết định cuối → low autonomy.
>
> **Attribution**: MEDIUM (leaning high).
> - Justification: 1 draft = 1 AI output cụ thể, có thể measure (% drafts used as-is, % edited heavy, % discarded). Tuy nhiên outcome cuối (CSAT) bị ảnh hưởng bởi agent skill + KB quality nữa, không chỉ AI.
>
> **Quadrant**: Low Autonomy + Medium-High Attribution → Hybrid (Seat + Credits).
>
> **Pricing đề xuất**: $25/seat/month, bundle 1,000 AI drafts/seat. Extra: $0.05/draft.
>
> **Real-world analog**:
> - Cursor: $20/seat + tiered credits cho IDE AI completion.
> - Lavender: $39/seat + extra usage for sales email AI.
>
> **Edge case note**: nếu IT muốn flat (predictable cost), có thể chọn $35/seat unlimited — nhưng risk Usage Anxiety nếu user dùng nhiều bị bottleneck.

---

## Anti-pattern khi prompt — tránh

| Đừng làm | Nên làm |
|---|---|
| Pick quadrant random | Justify từ brief field 2, 5, 9 |
| High autonomy + brief có review constraint | Constraint review → low autonomy luôn |
| Bỏ analog | Cross-check với 2-3 sản phẩm thật |
| Pricing không link với cost | Pricing đề xuất phải > cost/unit + margin |
| Bỏ Usage Anxiety check ở Hybrid model | Hybrid có credit limit → check anxiety |

---

## Format save vào `1-attribution-autonomy.md`

```markdown
## Phần B — Trả lời 2 câu hỏi

### Câu hỏi 1: Autonomy
[Paste assessment]

### Câu hỏi 2: Attribution
[Paste assessment]

## Phần C — Đặt vị trí trên ma trận
[Paste quadrant + pricing tự nhiên]

## Phần D — Validate với real-world analog
[Paste analog table]
```

---

## Câu hỏi mở rộng — nâng cao phản biện (optional)

```text
Sau khi định vị, giúp tôi suy nghĩ 3 câu hỏi STRATEGIC:

1. **Pricing model migration**: nếu brief tôi MVP với seat (low auto + low attrib), nhưng 2 năm sau
   AI khá autonomy (vì agent quen, mở auto-respond) → migration pricing thế nào?
   - Move sang outcome-based? Cần grace period bao lâu?

2. **Pricing model cho buyer khác**: cùng pricing có phù hợp cho buyer khác không?
   - Buyer là CTO → ai care về cost predictability.
   - Buyer là CFO → care về ROI defendability.
   - Buyer là VP Operations → care về adoption.

3. **Bundle vs unbundle**: AI feature này nên bán riêng hay bundle với product cũ?
   - Bundle: easier sale nhưng khó measure AI ROI.
   - Unbundle: defendable AI value nhưng add procurement friction.

Trả lời 3 câu này để chuẩn bị cho buổi present + Q&A từ instructor.
```
