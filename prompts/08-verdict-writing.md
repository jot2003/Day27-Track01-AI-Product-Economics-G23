# Prompt tham khảo 8 — Viết Verdict Statement (GO / CONDITIONAL / NO-GO)

**Dùng khi**: nhóm đã có 5 scenarios + combined worst case, cần chốt verdict và viết conditions / changes cụ thể.
**Công cụ gợi ý**: Claude Sonnet/Opus, ChatGPT-4o.
**Lưu kết quả vào**: `worksheet/03-stress-test/2-verdict-draft.md` + Section D.4-D.8 trong `3-FINAL-stress-test-verdict.md`
**Thời gian**: 15 phút

---

## Trước khi vào prompt — 5 câu hỏi nhóm tự trả lời

1. **Base ROI**: ___:1.
2. **Combined worst case ROI**: ___:1.
3. **Survives X/5 scenarios** (X = bao nhiêu scenario có ROI > 1.5:1)?
4. **Buyer trong brief**: ai (CTO/VP/Director/...)?
5. **Honesty test**: nhóm có ngả về GO chỉ vì "GO là đáp án đúng"?

> **Cảnh báo**: nhiều nhóm chọn GO vì cảm giác GO = success. Thực tế, CONDITIONAL với điều kiện rõ là verdict CHUYÊN NGHIỆP nhất.

---

## Prompt chính (paste sau scenarios output)

```text
Bạn là CFO advisor giúp viết verdict cho AI pilot.
Dựa trên BỐI CẢNH ở trên (brief + cost + value + ROI + 5 scenarios + combined worst),
giúp nhóm tôi:

1. Apply criteria → chọn verdict (GO / CONDITIONAL / NO-GO).
2. Viết verdict statement actionable.
3. Liệt kê conditions / changes cụ thể.

YÊU CẦU:

PHẦN 1 — Apply Criteria:

| Criteria | GO | CONDITIONAL | NO-GO |
|---|---|---|---|
| Base ROI | > 3:1 | 1-3:1 | < 1:1 |
| Survives X/5 scenarios | 4-5 | 2-3 | 0-1 |
| Combined worst case | > 1.5:1 | 0.5-1.5:1 | < 0.5:1 |

Apply cho nhóm tôi:
- Base ROI: ___:1 → tier ___
- Survives X/5: ___/5 → tier ___
- Combined worst: ___:1 → tier ___

Nếu 3 row chỉ vào 1 verdict → clear.
Nếu lệch (vd: base GO, combined NO-GO) → nghiêng CONDITIONAL với conditions chặt.

VERDICT đề xuất: ___

PHẦN 2 — Verdict Statement:

Viết 3-4 câu, paste được vào Section D.4. Phải:
- Rõ verdict (GO / CONDITIONAL / NO-GO).
- Số ROI base + combined worst (defendable).
- 1 key condition / change (nếu CONDITIONAL / NO-GO).

Format tùy verdict:

NẾU GO:
"Proceed with pilot as scoped. Brief #___ — [tên]. Base ROI ___:1, sống cả [n/5] scenarios. Combined worst case [scenarios xấu nhất] cho ROI ___:1, trên ngưỡng 1.5:1. Proceed without conditions."

NẾU CONDITIONAL:
"CONDITIONAL GO. Brief #___ — [tên]. Base ROI ___:1, sống [n/5] scenarios. Combined worst case [scenarios] cho ROI ___:1 — biên mỏng. Pilot tiếp tục với conditions: 1) ___ 2) ___ 3) ___. Stop trigger: ___."

NẾU NO-GO:
"NO-GO at current scope. Brief #___ — [tên]. Base ROI ___:1 hoặc combined worst ___:1. Cần thay đổi: 1) ___ 2) ___ 3) ___. Loại: [Not now / Not ever]."

PHẦN 3 — Conditions (nếu CONDITIONAL):

3-5 conditions cụ thể, mỗi cái có 4 trường:
- Tên condition
- Đo bằng metric gì (cụ thể)
- Timeline (vd: tháng 1 EOM, weekly)
- Action nếu fail

Ví dụ:
"1. Adoption phải >= 60% trong tháng 1.
   - Metric: active users / pilot total mỗi tuần.
   - Timeline: tháng 1 EOM.
   - Action: nếu < 50% → pause review pilot, kiểm tra UX + training."

CẢNH BÁO: condition phải MEASURABLE + TIMED. Không "sẽ làm tốt".

PHẦN 4 — Monitoring Metrics:

3-5 metrics nhóm track trong pilot:
- Metric name + frequency + source + threshold.

Vd:
- Adoption rate: weekly từ usage logs, threshold >= 60%.
- Cost/task: weekly từ billing logs, threshold <= $0.01.
- Quality: weekly random sample 50 tasks, threshold >= 75%.
- User CSAT: monthly survey, threshold NPS >= 30.

PHẦN 5 — Stop / Pivot Trigger:

Trigger cứng: nếu X xảy ra trong Y thời gian → pause / pivot.

Vd:
"Trigger 1: Adoption < 40% trong 30 ngày liên tiếp → pause review."
"Trigger 2: Cost/task > $0.05 trong 2 tuần → switch to cheaper model."
"Trigger 3: Quality < 60% trong 30 ngày → halt + iterate prompt."

PHẦN 6 — Changes (nếu NO-GO):

Nếu NO-GO, liệt kê 2-3 changes để khả thi:
- Change name + tác động ROI dự kiến.

Vd:
"Change 1: Đổi từ Claude 3.5 sang GPT-4o-mini cho task simple → cost giảm 80%, ROI 0.7 → 2.1."
"Change 2: Renegotiate constraint 100% review → ROI 2.1 → 3.4."

Loại NO-GO: "Not now (revisit khi A, B)" hay "Not ever (fundamentally không phù hợp)".

YÊU CẦU FORMAT:
- Verdict statement ngắn (3-4 câu), defendable.
- Conditions / monitoring / trigger cụ thể, measurable, timed.
- Trả lời tiếng Việt thoát nghĩa.

YÊU CẦU PHẢN BIỆN:
- Verdict CONDITIONAL có conditions feasible không (không phụ thuộc miracle)?
- Verdict GO có check overestimate base case chưa?
- Verdict NO-GO có thực sự "not ever" hay chỉ "not now"?
```

---

## Iterate — đẩy AI sâu hơn nếu output chưa đủ

### Khi nhóm muốn GO nhưng combined worst < 1.5

```text
Nhóm tôi muốn GO vì base ROI = 3.5:1.

NHƯNG combined worst case = 1.2:1 < 1.5:1.

Per framework, đây là CONDITIONAL territory:
- Base GO ngụ ý "robust qua mọi shock".
- Combined worst < 1.5 ngụ ý "pilot có biên mỏng khi 2 scenarios cùng xảy ra".

Honest verdict: CONDITIONAL, KHÔNG GO.

Bằng chứng cho buyer:
- "Base ROI 3.5:1 attractive."
- "Nhưng nếu adoption < 40% AND quality < 60% cùng lúc → ROI 1.2:1 → mất 30% an toàn."
- "Đề xuất CONDITIONAL với conditions: monitor adoption + quality hàng tuần. Nếu cả 2 cùng giảm 2 tuần liên tiếp → trigger review."

CONDITIONAL với conditions cứng còn defend được hơn GO không stress test.

Recommend revise verdict: CONDITIONAL.
```

### Khi nhóm muốn NO-GO sớm

```text
Nhóm tôi muốn NO-GO vì base ROI = 1.4:1 (marginal).

Trước khi NO-GO, identify 3 levers:

LEVER 1: Giảm Cost
- Đổi model premium → mid-tier. Cost/task giảm 60%. ROI mới?
- Bỏ tooling không cần (vd: monitoring không bắt buộc trong pilot). Cost giảm 5%.
- Renegotiate constraint review (vd: tier-1 task auto). Human review cost giảm 30%.

LEVER 2: Tăng Value
- Mở rộng pilot 5 → 15 user. Amortize setup tốt hơn. Value/user giữ nguyên, total value 3×.
- Adoption boost: incentive program $500/month. ROI tăng?
- Quality boost: prompt iteration tuần 1-2. ROI tăng?

LEVER 3: Time horizon
- Pilot 90 ngày → 180 ngày. Setup amortize gấp đôi. Cost/month giảm 30%.

Recalc với lever combination:
- Just LEVER 1 (cheaper model): ROI ___.
- LEVER 1 + 2 (cheaper + broader pilot): ROI ___.
- LEVER 1 + 2 + 3 (cheaper + broader + longer): ROI ___.

Nếu sau lever ROI > 2:1 → CONDITIONAL.
Nếu vẫn < 1.5:1 → NO-GO với 2-3 changes recommend.

Đừng NO-GO trước khi thử lever.
```

### Khi conditions không khả thi

```text
CONDITIONAL conditions nhóm tôi:
- Adoption >= 80% trong tháng 1.
- Quality >= 90% trong tháng 1.

Realistic check:
- Adoption 80% trong tháng 1 ở pilot voluntary → KHÓ. Realistic 50-70% tháng 1.
- Quality 90% trên draft generation → KHÓ. Realistic 75-85% mature, 65-75% tháng 1.

Conditions này không khả thi → CONDITIONAL biến thành NO-GO trá hình.

Revise conditions:
- Adoption >= 50% trong tháng 1, >= 65% tháng 3.
- Quality >= 70% trong tháng 1, >= 80% tháng 3.

Conditions phải đạt được realistic — không là wishful thinking.
```

---

## Phản biện sau khi có output — 5 câu nhóm tự hỏi

1. **Verdict rõ ràng**: GO / CONDITIONAL / NO-GO, không "có thể"?
2. **Statement defendable**: 3-4 câu defend được buyer challenge?
3. **Conditions measurable**: mỗi condition có metric + timeline + action?
4. **Trigger specific**: stop trigger có ngưỡng + thời gian + action cụ thể?
5. **Honest**: verdict reflect data hay reflect "muốn pilot success"?

---

## Ví dụ tốt vs ví dụ chưa tốt

### Chưa tốt

> "Verdict: CONDITIONAL. Pilot tiếp tục với một số điều kiện cần monitor. Sẽ track adoption và quality."

Vấn đề: không cụ thể, không measurable, không timed, không trigger.

### Tốt

> **Brief #1 — Verdict**
>
> **VERDICT: CONDITIONAL GO**
>
> "Brief #1 AI Support Copilot. Base ROI 2.07:1, sống 3/5 individual scenarios. Combined worst case (Low adoption + Quality fail) cho ROI 0.6:1 — Risky. Pilot tiếp tục với 4 conditions chặt + stop trigger rõ. Targeted ROI cuối pilot: > 2.5:1."
>
> **Conditions**:
>
> 1. **Adoption ≥ 60% trong tháng 1, ≥ 70% trong tháng 2**.
>    - Metric: active users / pilot total mỗi tuần.
>    - Timeline: weekly check, monthly milestone.
>    - Action fail: pause pilot, intensify training, redesign UX.
>
> 2. **Quality ≥ 75% trong pilot (random sample 50 tasks/tuần)**.
>    - Metric: % drafts dùng without major edits.
>    - Timeline: weekly sample.
>    - Action fail: prompt engineering sprint, KB audit + update.
>
> 3. **Cost/task ≤ $0.012 (= API + tooling, không include human review)**.
>    - Metric: monthly billing / monthly volume.
>    - Timeline: monthly.
>    - Action fail: switch to cheaper model fallback.
>
> 4. **Lock Anthropic enterprise contract 6 tháng**.
>    - Action: negotiate pre-pilot, contract clause.
>    - Action fail (không lock được): setup backup GPT-4o-mini fallback.
>
> **Monitoring Metrics** (dashboard track weekly):
> - Adoption rate, Cost/task, Quality factor, Agent CSAT, Monthly budget burn rate.
>
> **Stop Trigger** (pause review):
> - Trigger 1: Adoption < 40% trong 30 ngày liên tiếp.
> - Trigger 2: Quality < 60% trong 30 ngày liên tiếp.
> - Trigger 3: Compliance event (vi phạm policy, customer complaint AI-related).
> - Trigger 4: Monthly cost > $4,000 (= 80% budget) liên tiếp 2 tháng.
>
> **Buyer view**: CONDITIONAL với conditions cứng + trigger rõ → CTO có thể defend trước CFO. ROI 2.07:1 base, có buffer adoption 32% break-even, defendable với data.

---

## Anti-pattern khi prompt — tránh

| Đừng làm | Nên làm |
|---|---|
| GO mà combined worst < 1.5 | Honest: CONDITIONAL |
| CONDITIONAL không có condition cụ thể | 3-5 conditions measurable + timed |
| Condition phụ thuộc miracle (adoption 95%) | Realistic threshold |
| NO-GO mà không identify lever | Try lever trước, NO-GO sau khi exhausted |
| Trigger = "nếu pilot fail" | Trigger = "Adoption < 40% trong 30 ngày" |
| Quên buyer perspective | Buyer (CTO/VP) defend được trước CFO không? |

---

## Format save vào `2-verdict-draft.md` và Section D

```markdown
## Phần C — Verdict của nhóm
[Paste verdict + statement + conditions / changes]

## Section D.4 — Verdict
[Paste]

## Section D.5 — Conditions
[Paste bảng]

## Section D.6 — Monitoring
[Paste]

## Section D.7 — Stop Trigger
[Paste]

## Section D.8 — Changes (nếu NO-GO)
[Paste]
```

---

## Câu hỏi mở rộng — nâng cao phản biện (optional)

```text
Sau khi viết verdict, suy nghĩ 3 câu để chuẩn bị defend:

1. **Buyer challenge** (hardest question):
   - CTO sẽ hỏi: "Tại sao CONDITIONAL chứ không GO?"
   - CFO sẽ hỏi: "Combined worst case 0.6:1 — pilot có thực sự safe?"
   - VP Operations sẽ hỏi: "Adoption 60% trong tháng 1 — based on gì?"
   - Chuẩn bị 1-2 câu defense cho mỗi challenge.

2. **D28 panel question** (anticipate):
   - Panel sẽ hỏi: "Nếu cost API tăng 5×, pilot có sống không?"
   - Panel sẽ hỏi: "Adoption trong production khác pilot thế nào?"
   - Panel sẽ hỏi: "1 năm sau, ROI có thay đổi không?"

3. **Counter-narrative**:
   - "Nhưng pilot ROI 2:1 vẫn nhỏ — có nên không build, đầu tư vào khác?"
   - Counter: "Pilot ROI 2:1 + optionality. Compétiteur làm → cost of not trying."
   - "Adoption 30% case thấp — pilot fail mode. Plan migration?"

3 câu này chuẩn bị defense rõ cho D28 — không chỉ đọc verdict mà respond intelligently.
```
