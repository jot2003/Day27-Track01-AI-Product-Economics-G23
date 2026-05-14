# Prompt tham khảo 9 — So sánh Cross-Brief

**Dùng khi**: nhóm đã hoàn thành Economics Sheet, muốn so sánh kết quả với 1-2 cặp khác brief khác — rút insight pattern across briefs.
**Công cụ gợi ý**: Claude Sonnet/Opus, ChatGPT-4o.
**Lưu kết quả vào**: Phần "Comparison với cặp khác brief" trong `04-FINAL-economics-sheet.md`
**Thời gian**: 10 phút (sau giờ Lab chính, có thể làm trong giờ Present)

---

## Trước khi vào prompt — 5 câu hỏi nhóm tự trả lời

1. **Brief nhóm tôi** là gì (# + tên)?
2. **Brief 2 cặp khác** đã share kết quả với mình là gì?
3. **3 metrics chính** so sánh: Monthly Cost, Monthly Value, ROI.
4. **Pattern tìm kiếm**: cost structure khác nhau ở chỗ nào? Verdict khác nhau lý do gì?
5. **Insight target**: tổng quát hoá pattern từ 3 brief.

> **Cảnh báo**: cross-brief comparison KHÔNG để "thắng/thua" giữa nhóm. Để rút **insight transferable** về AI economics — patterns vượt brief.

---

## Prompt chính (paste sau khi có Economics Sheet 3 brief)

```text
Bạn là Senior Product Manager AI có kinh nghiệm cross-portfolio.
Dựa trên 3 brief Economics Sheet (brief nhóm tôi + 2 brief cặp khác),
giúp tôi extract patterns + insights.

DATA NHẬP VÀO:

Brief A (nhóm tôi): #___ "[tên]"
- Usage unit: ___
- Monthly cost: $___ (API ___%, tooling ___%, review ___%, setup ___%)
- Monthly value: $___
- Base ROI: ___:1
- Verdict: ___
- Pricing model: ___

Brief B (cặp khác): #___ "[tên]"
- [tương tự]

Brief C (cặp khác): #___ "[tên]"
- [tương tự]

YÊU CẦU PHÂN TÍCH:

PHẦN 1 — Bảng so sánh:

| Aspect | Brief A | Brief B | Brief C |
|---|---|---|---|
| Domain | | | |
| Usage unit | | | |
| Monthly volume (tasks) | | | |
| Cost/task | $___ | $___ | $___ |
| Cost component dominate | [vd: API / Human review / Tooling] | | |
| Monthly cost | $___ | $___ | $___ |
| Monthly value | $___ | $___ | $___ |
| Base ROI | ___:1 | ___:1 | ___:1 |
| Combined worst ROI | ___:1 | ___:1 | ___:1 |
| Pricing model | | | |
| Verdict | | | |

PHẦN 2 — Pattern Analysis:

Identify 3-4 patterns:

PATTERN 1 — Cost structure pattern
- Brief nào có cost dominate bởi API? Lý do? (vd: high volume + low review = API dominate).
- Brief nào có cost dominate bởi Human Review? Lý do? (vd: 100% review constraint).
- Brief nào có cost dominate bởi Tooling? Lý do?

PATTERN 2 — Volume vs Cost/task pattern
- Brief có high volume + low cost/task (support, content) vs Brief có low volume + high cost/task (legal, medical)?
- Trade-off khác nhau cho mỗi pattern?

PATTERN 3 — Verdict pattern
- Hầu hết verdict là gì (GO / CONDITIONAL / NO-GO)?
- Pattern nào dẫn đến CONDITIONAL (vd: 3 trong 4 = CONDITIONAL nếu có constraint review)?

PATTERN 4 — Pricing model pattern
- Brief với high attribution (legal, claim) → outcome-based dễ hơn?
- Brief với low attribution (support, content) → seat-based dễ hơn?
- Có ngoại lệ không?

PHẦN 3 — Insights transferable:

3 insight rút ra:

1. "Insight 1": [vd: AI economics dominate by Human Review cost khi brief có 100% review constraint. API cost insignificant.]

2. "Insight 2": [vd: ROI sensitive nhất với adoption — không phải cost. Adoption tăng 20% → ROI tăng 30%, nhưng cost giảm 20% chỉ tăng ROI 20%.]

3. "Insight 3": [vd: CONDITIONAL chiếm 70% verdict — đó là realistic, không phải pessimistic. Pilot AI thực tế đa số là CONDITIONAL.]

PHẦN 4 — Lesson cho buyer:

Nếu CTO/VP hỏi "Pattern giữa các AI pilot của chúng ta là gì?", reply:
- [vd: "Human review cost dominate. Optimize ROI = tối ưu review, không phải tối ưu model."]
- [vd: "Adoption là biến quan trọng nhất. Đầu tư training > đầu tư AI quality."]
- [vd: "Provider risk thấp khi API < 10% total cost. Nhưng quan trọng cho ML startup."]

PHẦN 5 — Cross-brief learning cho nhóm tôi:

So với Brief B + C, brief tôi:
- Stronger ở: ___
- Weaker ở: ___
- Có thể borrow từ Brief B/C: ___ (vd: pricing model, mitigation conditions)

YÊU CẦU FORMAT:
- Bảng + bullet rõ ràng.
- Trả lời tiếng Việt thoát nghĩa.

YÊU CẦU PHẢN BIỆN:
- Có pattern nào có thể là coincidence không (chỉ 3 brief — sample nhỏ)?
- Có pattern nào surprising không?
- Pattern nào contradicting với common wisdom?
```

---

## Iterate — đẩy AI sâu hơn nếu output chưa đủ

### Khi muốn deeper cost structure analysis

```text
Bảng cost structure 3 brief:

| Component | Brief A | Brief B | Brief C |
|---|---|---|---|
| API ($ + %) | $30 (1%) | $300 (60%) | $15 (10%) |
| Tooling ($ + %) | $120 (4%) | $50 (10%) | $200 (15%) |
| Human review ($ + %) | $2,500 (90%) | $0 (0%) | $1,000 (75%) |
| Setup ($ + %) | $150 (5%) | $150 (30%) | $0 (0%) |
| **Total** | **$2,800** | **$500** | **$1,215** |

Analyze:
1. Vì sao Brief A có Human Review 90% còn Brief B có 0%?
   (Brief A: 100% review constraint. Brief B: high autonomy, no review.)
2. Brief B có API 60% — provider risk cao nhất. Mitigation?
3. Brief C cost mid-range $1,215 — balanced. Có pattern gì?

Recommend lesson cho mỗi brief để optimize cost.
```

### Khi muốn rút conclusion vĩ mô

```text
Sau khi phân tích 3 brief, đưa ra 3 conclusion vĩ mô về AI economics:

1. "AI cost không phải về API — về human-in-the-loop."
   - Bằng chứng: 2/3 brief có human review dominate.
   - Implication: PM phải tối ưu review process, không chỉ chọn model rẻ.

2. "ROI break-even thường ở adoption 30-40%."
   - Bằng chứng: 3 brief đều break-even ở adoption ~35%.
   - Implication: pilot success metric quan trọng nhất = adoption tracking.

3. "Pricing model phụ thuộc Attribution > Autonomy."
   - Bằng chứng: high attribution → outcome-based dễ pass; low attribution → seat-based.
   - Implication: trước khi định pricing, hỏi "AI tạo outcome đo được không?".

3 conclusion này có defensible với data 3 brief không?
```

### Khi muốn map với industry pattern

```text
3 brief của lớp + 3 ví dụ industry public:

| Brief | Industry analog | Họ học được gì |
|---|---|---|
| #1 Support Copilot | Intercom Fin, Ada, Zendesk AI | Outcome-based works ở high autonomy |
| #2 Content Moderator | OpenAI Moderation, Hive AI | API-dominate, scale matters |
| #3 Medical Triage | Buoy Health, Babylon Health | Trust + regulation = slow adoption |

Cross-reference: brief lớp tôi có pattern giống/khác industry?
- Pattern giống: ___
- Pattern khác: ___ (lý do: pilot scale vs production scale)

Insight: ___
```

---

## Phản biện sau khi có output — 5 câu nhóm tự hỏi

1. **Pattern check**: 3 brief có thực sự cho pattern, hay là coincidence?
2. **Insight check**: insight có actionable cho PM tương lai?
3. **Surprising check**: có pattern nào ngược với common wisdom?
4. **Buyer view**: CTO hỏi "What's pattern across pilots?" → có defendable answer?
5. **Transferable check**: lesson cho brief tôi có cụ thể, không chỉ chung chung?

---

## Ví dụ tốt vs ví dụ chưa tốt

### Chưa tốt

> "3 brief khác nhau. Brief 1 ROI 2.1, brief 2 ROI 5, brief 3 ROI 1.2."

Vấn đề: chỉ liệt kê, không pattern, không insight.

### Tốt

> **Cross-Brief Comparison — Lớp AI20K-D27**
>
> **Bảng so sánh** (chỉ kéo cost + ROI key):
>
> | Brief | Domain | Cost ($/mo) | Cost dominate | ROI base | Verdict |
> |---|---|---|---|---|---|
> | #1 (us) Support Copilot | B2B SaaS | $2,803 | Human Review 47% | 2.07:1 | CONDITIONAL |
> | #2 Content Moderator | Social platform | $3,200 | Human Review 92% | 1.5:1 | CONDITIONAL |
> | #4 Legal Contract | M&A law | $1,400 | API 35%, Review 50% | 2.7:1 | CONDITIONAL |
>
> **Pattern 1 — Cost dominate by Human Review**:
> - 3/3 brief có Human Review > 40% cost.
> - Lý do: cả 3 đều có constraint "100% review" hoặc tương đương.
> - Insight: API cost (5-15%) thường minor. Tối ưu review process quan trọng hơn chọn model rẻ.
>
> **Pattern 2 — Volume vs Cost/task trade-off**:
> - Brief #1: high volume (3,520/mo) + low cost/task ($0.0084).
> - Brief #2: extreme volume (146K/mo) + ultra-low cost/task ($0.000135).
> - Brief #4: low volume (200/mo) + high cost/task ($2.50).
> - Insight: 2 economic models — Volume Play (#1, #2) vs Premium Play (#4). Different optimization.
>
> **Pattern 3 — Verdict pattern**:
> - 3/3 = CONDITIONAL. None GO, none NO-GO.
> - Lý do: pilot scale + uncertain adoption + emerging provider pricing.
> - Insight: CONDITIONAL là default cho AI pilot. CTO nên expect CONDITIONAL, không GO chắc chắn.
>
> **Pattern 4 — Pricing model**:
> - Brief #1: Hybrid Seat + Credits.
> - Brief #2: Usage-based (per flag pre-screen).
> - Brief #4: Hybrid Seat + Outcome.
> - Insight: 2/3 chọn Hybrid — không phải pure pricing. Hybrid balance predictability + ROI defendability.
>
> **Lesson cho nhóm tôi**:
> - Borrow từ Brief #2: scale advantage. Nếu pilot tôi mở rộng 5 → 25 agent → cost dominated by API (như #2) → có thể cheaper model fallback hợp lý hơn.
> - Borrow từ Brief #4: outcome-based component. Có thể thử $X/seat + outcome $Y/draft accepted → defend ROI rõ hơn cho CFO.

---

## Anti-pattern khi prompt — tránh

| Đừng làm | Nên làm |
|---|---|
| Chỉ liệt kê 3 brief, không so sánh | Đặt vào bảng + identify pattern |
| Không có actionable insight | Mỗi pattern có implication cho PM |
| Conclusion chung chung "AI khác nhau" | Cụ thể "Human review dominate when constraint review" |
| Coincidence treated as pattern | Caveat: sample 3 brief, cần n=10+ mới robust |
| Bỏ industry analog | Cross-ref với real product (Intercom, Hive, etc.) |

---

## Format save vào `04-FINAL-economics-sheet.md` (phần Comparison)

```markdown
## Comparison với cặp khác brief

[Paste bảng + 3-4 pattern + lesson cho nhóm]
```

---

## Câu hỏi mở rộng — nâng cao phản biện (optional)

```text
Cross-brief insight là proxy cho 1 câu hỏi lớn hơn:

"Có universal 'AI is expensive / cheap' không, hay luôn phụ thuộc?"

Sau khi xem 3 brief, trả lời:

1. **Universal claim test**: nếu nói "AI cost luôn dominate by API" — có phải universally đúng?
   - Bằng chứng: 3/3 brief lớp tôi cost dominate Human Review, không API.
   - Conclusion: claim sai. AI cost dominate by **constraint structure** (review vs auto).

2. **Per-brief specific**:
   - Brief có 100% review → human review dominate.
   - Brief có high autonomy → API dominate.
   - Brief có narrow domain → setup dominate (fine-tune cost).

3. **PM mental model**:
   - Trước stress test: assume "AI cost = API cost".
   - Sau stress test: "AI cost = constraint cost + opportunity cost".
   - Đây là shift quan trọng cho PM AI mới.

Trả lời 3 câu này = D28 panel question prepare. Panel sẽ hỏi "Pattern là gì? Insight cho PM?" — trả lời được = strong defense.
```
