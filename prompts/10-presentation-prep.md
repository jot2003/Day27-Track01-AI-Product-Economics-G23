# Prompt tham khảo 10 — Chuẩn bị 6-Phút Trình Bày

**Dùng khi**: nhóm đã có FINAL Economics Sheet, cần chuẩn bị bài trình bày 6 phút (~3 phút trình bày + ~3 phút Q&A) cho slot present cuối lab.
**Công cụ gợi ý**: Claude Sonnet/Opus, ChatGPT-4o.
**Lưu kết quả vào**: Ghi chú riêng / slides riêng (PDF / Google Slides) — không trong worksheet.
**Thời gian**: 10-15 phút

---

## Trước khi vào prompt — 5 câu hỏi nhóm tự trả lời

1. **Có thể được gọi cold-call không**? (Theo skeleton: instructor chọn 4 cặp present. Cố gắng ready.)
2. **Brief + usage unit + ROI base + verdict** — đã memorize chưa?
3. **Worst stress scenario** + ROI mới — đã memorize?
4. **3 condition cứng nhất** (nếu CONDITIONAL) — đã memorize?
5. **Buyer là ai + buyer sẽ hỏi gì** — đã anticipate?

> **Cảnh báo**: bài trình bày 3 phút cần CHẶT. Mỗi giây có giá. Không lan man, không "uhm uhm".

---

## Prompt chính (paste sau FINAL Economics Sheet)

```text
Bạn là Public Speaking coach cho PM AI.
Dựa trên BỐI CẢNH (FINAL Economics Sheet đã hoàn thành),
giúp nhóm tôi chuẩn bị bài trình bày 3 phút + chuẩn bị Q&A 3 phút.

YÊU CẦU CẤU TRÚC:

PHẦN 1 — 3-Min Present Structure:

Cấu trúc cứng (đúng timing):

```
0:00 — 0:30  Brief + Usage Unit
              "Brief #___ [tên]. Use case: [1 câu]. Usage unit: [1 câu]."

0:30 — 1:00  Cost Model
              "Monthly cost $___. Breakdown: API $___ (___%), Tooling $___, Human review $___ (___%), Setup $___."
              [Key insight: cost dominate by ___]

1:00 — 1:30  Value/ROI
              "Monthly value $___ với adoption ___%, quality ___%. Base ROI ___:1."
              [Key insight: ROI sensitive nhất với ___]

1:30 — 2:00  Worst Stress Scenario
              "Combined worst case [scenarios xấu nhất] → ROI ___:1."
              [Key insight: scenario hurt nhất = ___]

2:00 — 3:00  Verdict + Conditions
              "Verdict: [GO / CONDITIONAL / NO-GO]."
              "Lý do: [base ROI + combined worst]."
              "Conditions: 1) ___ 2) ___ 3) ___."
              "Stop trigger: ___."

3:00          STOP. Im lặng. Đợi Q&A.
```

YÊU CẦU: viết script đầy đủ 3 phút theo cấu trúc trên, dùng số/data của brief tôi.

PHẦN 2 — Slides (6 trang đơn giản):

Slide 1: Title + Brief #
Slide 2: Cost breakdown bar chart hoặc list
Slide 3: Monthly Value formula + ROI
Slide 4: 5 scenarios bảng + combined worst highlight
Slide 5: Verdict statement + 3 conditions
Slide 6: Q&A invite

Viết content cho từng slide (tối đa 5-7 line/slide).

PHẦN 3 — Q&A Anticipated (chuẩn bị 5 câu instructor có thể hỏi):

Theo skeleton, instructor có 4 nhóm câu hỏi:
1. Assumptions probe (adoption, quality, cost/task).
2. Stress test probe (worst scenario, mitigation, break-even).
3. Strategic probe (provider risk, scale, CONDITIONAL).
4. Cross-brief probe (compare với cặp khác).

Chuẩn bị 5 câu Q&A:

Q1: "Adoption ___% — based on gì? Có data không?"
A1: [1-2 câu defense với data hoặc justification]

Q2: "Worst scenario nào hurt nhất? Tại sao?"
A2: [scenario + lý do + insight]

Q3: "Combined worst case ___:1 — Pilot có safe không?"
A3: [defend với conditions + trigger]

Q4: "Provider cost × 2 — Replit margin âm story — tránh thế nào?"
A4: [mitigation: lock contract / backup model / monitor cost gate]

Q5: "Verdict CONDITIONAL — khi nào review lại? Metric trigger stop?"
A5: [timeline + trigger cụ thể]

PHẦN 4 — Coach-style feedback:

Sau khi viết script + slides, identify 3 điểm yếu:
- "Đoạn nào dài quá / nói nhanh quá?"
- "Số nào audience khó nắm bắt? Cần visual hỗ trợ?"
- "Tone có quá lạc quan / pessimistic?"

Recommend tweak.

YÊU CẦU FORMAT:
- Script bằng tiếng Việt thoát nghĩa (giả định present bằng tiếng Việt cho lớp).
- Slides content ngắn gọn 5-7 dòng.
- Q&A defense rõ ràng, có evidence.

YÊU CẦU PHẢN BIỆN:
- Trong 3 phút, có thông tin nào nên cắt (nice-to-know but not need-to-know)?
- Verdict có rõ ràng đầu / cuối present không?
- Conditions có specific enough cho audience nhớ?
```

---

## Iterate — đẩy AI sâu hơn nếu output chưa đủ

### Khi script dài hơn 3 phút

```text
Script bạn viết dài ___ words → ___ phút (avg 150 wpm Vietnamese).

Vượt 3 phút. Cắt:

PRIORITY KEEP (must include):
- Brief # + usage unit (30s).
- Cost number + dominate component (30s).
- ROI base + adoption/quality assumption (30s).
- Combined worst case + ROI (30s).
- Verdict + 3 conditions + stop trigger (60s).

PRIORITY CUT (skip nếu không đủ thời gian):
- Detailed cost breakdown all 4 components.
- All 5 stress scenarios (chỉ kể combined worst).
- Real-world analog detail.
- Sensitivity analysis chi tiết.

Re-write script trong 3 phút strict, dùng priority keep.
```

### Khi muốn Q&A defense mạnh

```text
Instructor Q&A có 4 nhóm probe. Cho mỗi nhóm, chuẩn bị 2 defense:

NHÓM 1 — ASSUMPTIONS PROBE
Q1a: "Adoption 65% — based on gì?"
A1a: "Brief có UX integrated trong Zendesk + training 1 session. Range typical pilot mandatory 60-85% → 65% bảo thủ lower bound."

Q1b: "Quality 80% — POC data hay benchmark?"
A1b: "Benchmark Claude 3.5 trên draft generation 75-85%, adjust 80% account KB outdated 30%. Conservative."

NHÓM 2 — STRESS PROBE
Q2a: "Worst scenario nào hurt nhất?"
A2a: "Low adoption + Quality fail combined → ROI 0.6:1. Cost fixed, value collapse với adoption × quality."

Q2b: "Mitigation cụ thể?"
A2b: "1) Adoption monitor weekly, trigger pause < 40%. 2) Quality random sample 50 tasks weekly. 3) Backup model fallback."

NHÓM 3 — STRATEGIC PROBE
Q3a: "Scale 5 → 25 agent, ROI thay đổi thế nào?"
A3a: "Cost mostly linear (API + review), setup amortize tốt hơn. ROI tăng ~10-15% nhờ amortize."

Q3b: "OpenAI giảm giá 50%, có nên switch?"
A3b: "API chỉ 1% total cost — switch không impact ROI nhiều. Focus quality + adoption higher impact."

NHÓM 4 — CROSS-BRIEF
Q4a: "Brief khác có pattern tương tự?"
A4a: "3 brief lớp đều cost dominate human review. AI economics khác brief nhưng review pattern giống."

Viết 8 defense ngắn — chuẩn bị cho mọi nhóm câu hỏi.
```

### Khi muốn slide content tối ưu

```text
Slides cho 3-min present cần tối giản. Mỗi slide:

Slide 1 (Title):
- "Brief #___ [Tên]"
- "AI Economics Lab — D27"
- Cặp name + brief assigned

Slide 2 (Cost):
- "Monthly Cost: $___"
- Stacked bar: API ___% | Tooling ___% | Review ___% | Setup ___%
- 1 line: "Dominate: ___ (___% total)"

Slide 3 (Value/ROI):
- "Monthly Value: $___"
- "ROI Base: ___:1"
- 1 line formula: "value × adoption% × quality%"

Slide 4 (Stress):
- Bảng 5 scenarios với ROI
- Combined worst highlight (color red nếu < 1.5:1)
- 1 line: "Worst: [scenarios] → ___:1"

Slide 5 (Verdict):
- BIG: "VERDICT: [GO / CONDITIONAL / NO-GO]"
- 3 conditions (max 3 lines)
- 1 stop trigger

Slide 6 (Q&A):
- "Q&A"
- Brief # + key numbers (Cost, Value, ROI base, ROI worst)
- For audience refer

Total: 6 slides, 5-7 line max per slide. No dense paragraph.
```

---

## Phản biện sau khi có output — 5 câu nhóm tự hỏi

1. **Time check**: script trong 3 phút strict (150 wpm × 3 min = ~450 từ)?
2. **Verdict clear**: verdict mention đầu + cuối present?
3. **Numbers memorable**: 3-5 con số chính (cost, value, ROI base, ROI worst, adoption threshold) — đã memorize?
4. **Q&A coverage**: 5 câu Q&A cover 4 nhóm probe?
5. **Confidence**: nhóm có thể defend nếu instructor probe deeper?

---

## Ví dụ tốt vs ví dụ chưa tốt

### Chưa tốt

> "Brief # 1 AI support copilot. Cost cao, ROI cũng cao, verdict CONDITIONAL với conditions."

Vấn đề: không số cụ thể, không structure, không actionable.

### Tốt

> **Script 3-Min Present — Brief #1**
>
> **(0:00-0:30)** "Brief 1 — AI Support Copilot. B2B SaaS 200 nhân viên, 800 ticket/ngày. Pilot 5 agent trong 90 ngày, ngân sách 5,000 đô. Usage unit: 1 ticket reply draft — atomic AI call, đếm được, có giá trị 9 phút saved per task."
>
> **(0:30-1:00)** "Monthly cost 2,803 đô. Breakdown: API chỉ 30 đô (1%), tooling 120 đô (4%), human review 1,320 đô (47%), setup amortize 1,333 đô (48%). Insight: cost dominate by human review — không phải API. Đây là pattern phổ biến với pilot có 100% review constraint."
>
> **(1:00-1:30)** "Monthly value 5,797 đô với adoption 65%, quality 80%, NET time saved 7.6 phút per task. Base ROI 2.07 chấm 1 — tier Marginal."
>
> **(1:30-2:00)** "Stress test 5 scenarios. Worst nhất: Low adoption (30%) + Quality fail (50%) combined → ROI 0.6 chấm 1 — pilot không sống nếu cả 2 cùng fail. Heavy usage và Provider shock chỉ hurt nhẹ."
>
> **(2:00-3:00)** "Verdict: CONDITIONAL GO. Lý do: base ROI 2.07 attractive, nhưng combined worst 0.6 cảnh báo. Conditions: 1) Adoption >= 60% tháng 1, >= 70% tháng 2 — đo weekly. 2) Quality >= 75% — sample 50 tasks/tuần. 3) Lock Anthropic enterprise contract 6 tháng. Stop trigger: adoption < 40% trong 30 ngày liên tiếp → pause review pilot. Targeted ROI cuối pilot: >= 2.5 chấm 1."
>
> **(3:00)** STOP. Đợi Q&A.

---

## Anti-pattern khi prompt — tránh

| Đừng làm | Nên làm |
|---|---|
| Script 5 phút cho slot 3 phút | Cắt nice-to-know, giữ need-to-know |
| Verdict ở cuối + lặp lại 3 lần | Verdict ở đầu + cuối, mention 2 lần |
| Q&A defense chung chung | Defense có evidence: data, benchmark, brief field |
| Slide dense (10+ lines) | Max 5-7 lines/slide |
| Quên buyer perspective trong Q&A | Defense câu cho từng buyer (CTO/CFO/VP) |

---

## Format save (không trong worksheet)

Lưu:
- `present-script.md` — script 3 phút.
- `present-slides.md` hoặc PDF — 6 slides content.
- `qa-defense.md` — 8 câu Q&A defense.

Test:
- Đọc script bằng timer → có đúng 3 phút?
- Cặp tự Q&A nhau 5 câu → có defense rõ?

---

## Câu hỏi mở rộng — nâng cao phản biện (optional)

```text
Sau khi prepare, giúp tôi rehearse mental model:

1. **Opening hook** (5 giây đầu):
   - Cách 1: "Brief 1 là ___" — boring start.
   - Cách 2: "ROI 2.07 chấm 1 base — nhưng combined worst 0.6. Đó là tại sao CONDITIONAL." — hook with tension.
   - Recommend opening hook cho brief tôi.

2. **Closing punch** (5 giây cuối):
   - Cách 1: "Verdict CONDITIONAL." — flat ending.
   - Cách 2: "Pilot sống nếu adoption ≥ 60%. Đó là lý do CONDITIONAL — không phải GO. Adoption là biến cứu nguy." — memorable.
   - Recommend closing punch cho brief tôi.

3. **Mental contingency**:
   - Nếu instructor hỏi câu nhóm không chuẩn bị: tactic là gì?
   - "Câu hỏi hay. Tôi chưa modeling câu đó cụ thể, nhưng dựa trên framework: ___."
   - "Tôi sẽ test scenario này post-class và update FINAL sheet."

3 góc này = polish present từ "ổn" thành "ấn tượng".
```
