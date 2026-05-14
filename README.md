# Day 27 — AI Product Economics: Usage, Cost & Pricing

Day 27 là ngày BUILD: mỗi cặp 2 người nhận **1 challenge brief**, dựng **AI Economics Sheet** (4 sections) với cost / pricing / value / stress test / verdict, và present 6 phút cuối buổi.

Driving question:

> "Nếu người dùng thật sự dùng AI solution này, **kinh tế và rủi ro có sống nổi không**?"

Khác Day 26 (phân tích chiến lược sản phẩm AI có sẵn), Day 27 **tự xây economics từ 0** cho 1 use case fixed (challenge brief). Output là quyết định: GO / CONDITIONAL / NO-GO với conditions cụ thể.

Quy tắc cốt lõi: **không có công thức / nguồn pricing = không có số**. Mọi con số phải truy ngược về brief hoặc về provider pricing thực tế (URL working).

---

## Cấu trúc 1 ngày

```text
09:00-10:00  Theory 60'         Cost / Pricing / Value framework + Worked Example (Support Copilot)
10:00-10:10  Break
10:10-10:50  Lab Step 1 — 40'   Usage Unit + Cost Model (Section A)
10:50-11:30  Lab Step 2 — 40'   Pricing/Access + Value/ROI (Section B + C)
11:30-12:10  Lab Step 3 — 40'   5 Stress Scenarios + Verdict (Section D)
12:10-12:55  Present 45'        4 cặp × ~10' (3' present + 7' Q&A)
12:55-13:00  Close 5'           Recap + D28 preview
```

Lý thuyết 60 phút trang bị framework. Lab 120 phút là phần chính. Present 45 phút rút insight cross-brief.

---

## Nộp bài thế nào? (đọc trước khi vào lab)

### Tên kho GitHub

Cú pháp: **`Day27-MãNhóm`**

Ví dụ: `Day27-G001`, `Day27-G045`, `Day27-A1`.

Kho mẫu của giảng viên: <https://github.com/VinUni-AI20k/Day27-Track01-AI-Product-Economics>

### Cần nộp những file gì?

Nhóm tạo **1 kho GitHub công khai**, đưa toàn bộ thư mục `worksheet/` lên GitHub theo đúng cấu trúc dưới, rồi nộp link qua LMS.

```text
Day27-MãNhóm/                                       ← kho GitHub công khai
│
├── README.md                                       ← Thành viên cặp + link FINAL (xem mẫu dưới)
│
└── worksheet/
    ├── 00-context.md                               ← Bối cảnh nhóm + brief assigned (đã điền)
    │
    ├── 01-cost-model/
    │   ├── 1-usage-unit.md                         ← Trung gian: define usage unit + volume
    │   ├── 2-cost-research.md                      ← Trung gian: pricing research + cost/task
    │   └── 3-FINAL-cost-model.md                   🎯 Section A của Economics Sheet
    │
    ├── 02-pricing-value/
    │   ├── 1-attribution-autonomy.md               ← Trung gian: ma trận 2×2
    │   ├── 2-pricing-model-choice.md               ← Trung gian: pricing model + value metric
    │   └── 3-FINAL-pricing-value-roi.md            🎯 Section B + C của Economics Sheet
    │
    ├── 03-stress-test/
    │   ├── 1-scenario-table.md                     ← Trung gian: 5 scenarios + combined
    │   ├── 2-verdict-draft.md                      ← Trung gian: verdict draft + conditions
    │   └── 3-FINAL-stress-test-verdict.md          🎯 Section D của Economics Sheet
    │
    └── 04-FINAL-economics-sheet.md                 🎯🎯 MASTER FILE — Section A+B+C+D
```

🎯 = section của Economics Sheet (người chấm xem). Các file trung gian là **process** — phải nộp kèm để người chấm thấy nhóm đã đi qua đủ quá trình.

🎯🎯 = MASTER FILE — đây là deliverable cuối cùng người chấm xem trước.

### README đầu kho bài phải có gì?

Sao chép mẫu này vào `README.md` ở gốc kho bài và điền:

```markdown
# Day 27 — Mã nhóm [G___]

## Thành viên cặp

| # | Mã học viên | Họ tên đầy đủ |
|---|-------------|---------------|
| 1 | A20-XXXXX   | Nguyễn Văn A  |
| 2 | A20-XXXXX   | Trần Thị B    |

## Brief được giao

Brief # ___ — [tên brief, vd: AI Support Copilot]

## Kết quả cuối

- 🎯🎯 [MASTER — AI Economics Sheet](./worksheet/04-FINAL-economics-sheet.md)
- 🎯 [Section A — Cost Model](./worksheet/01-cost-model/3-FINAL-cost-model.md)
- 🎯 [Section B + C — Pricing/Access + Value/ROI](./worksheet/02-pricing-value/3-FINAL-pricing-value-roi.md)
- 🎯 [Section D — Stress Test + Verdict](./worksheet/03-stress-test/3-FINAL-stress-test-verdict.md)

## Verdict

**[GO / CONDITIONAL / NO-GO]**

Base ROI: ___:1
Combined worst case: ___:1
```

### Các bước nộp

1. Tạo kho GitHub công khai theo cú pháp `Day27-MãNhóm`.
2. Đưa toàn bộ thư mục `worksheet/` lên GitHub theo đúng cấu trúc trên.
3. Tạo `README.md` ở gốc kho bài theo mẫu, điền mã học viên + tên đầy đủ + brief # + verdict.
4. Đảm bảo file MASTER `04-FINAL-economics-sheet.md` có đầy đủ 4 Sections.
5. Một thành viên đại diện nộp link kho bài vào LMS Day 27, kiểm tra link mở được trước **23:59 hôm nay**.

---

## Quy trình làm bài

```text
Đọc lại lecture Day 27 (Cost Triangle, Monetization Triad, Value Metric Spectrum, Stress Test)
   -> Đọc 00-worked-example.md (Brief #1 đã điền — biết FINAL trông thế nào)
   -> Điền 00-context.md (brief assigned + 5 con số chính + provider dự định)
   -> Step 1: Cost Model (40 phút)
      -> Phase 1: Define usage unit + volume estimate (15')
      -> Phase 2: Cost research + cost/task (15')
      -> Phase 3: Chốt Section A (10')
   -> Step 2: Pricing/Access + Value/ROI (40 phút)
      -> Phase 1: Attribution × Autonomy positioning (15')
      -> Phase 2: Pricing model + value metric choice (10')
      -> Phase 3: Chốt Section B + C — Monthly Value + ROI (15')
   -> Step 3: Stress Test + Verdict (40 phút)
      -> Phase 1: 5 stress scenarios table (20')
      -> Phase 2: Verdict draft + conditions (10')
      -> Phase 3: Chốt Section D (10')
   -> Gộp 4 sections vào Master 04-FINAL-economics-sheet.md
   -> Rà soát checklist
   -> Nộp link kho bài qua LMS
```

---

## Step 1 — Cost Model (10:10–10:50, 40 phút)

Mục tiêu: define usage unit + tính Monthly AI Cost cho brief.

File cuối của Step 1: `worksheet/01-cost-model/3-FINAL-cost-model.md` (= Section A của Economics Sheet)

### Phase 1 — Usage Unit + Volume (15 phút)

Mỗi thành viên đề xuất 1 usage unit. Cặp chọn 1, kiểm tra qua **3-part test**:

1. **Đếm được không?** — có thể count số lần AI chạy.
2. **Tốn token không?** — mỗi lần = 1 API call.
3. **Có giá trị user không?** — 1 unit rút thời gian / cải thiện chất lượng?

Sau đó tính volume:

```text
Pilot daily volume = (Pilot users / Total team) × Team daily volume
Monthly volume = Pilot daily volume × 22 working days
```

File dùng ở phase này: `worksheet/01-cost-model/1-usage-unit.md`

### Phase 2 — Cost Research (15 phút)

Tự tra pricing **không cho sẵn**:

- Vào pricing page provider (OpenAI / Anthropic / Google) → tìm $/1M tokens.
- Ước tính tokens/task (input + output) → tính cost/task = (in × in_price + out × out_price) / 1M.
- Tra thêm tooling (vector DB, monitoring), human review cost, setup cost.

Quy tắc: **mỗi giá tiền phải có URL working**.

File dùng: `worksheet/01-cost-model/2-cost-research.md`

### Phase 3 — Chốt Section A (10 phút)

Gộp vào `3-FINAL-cost-model.md` với 8 sub-section (A.1 Usage Unit → A.8 Budget Check).

Công thức Monthly Cost:

```text
Monthly Cost = (Volume × API cost/task) + Tooling + (Volume × Review cost) + Setup amortize
```

---

## Step 2 — Pricing/Access + Value/ROI (10:50–11:30, 40 phút)

Mục tiêu: chốt pricing model, tính Monthly Value, tính ROI.

File cuối: `worksheet/02-pricing-value/3-FINAL-pricing-value-roi.md` (= Section B + C)

### Phase 1 — Attribution × Autonomy Positioning (15 phút)

Đặt sản phẩm trên ma trận 2×2:

- **Autonomy**: AI tự làm (High) hay hỗ trợ human (Low)?
- **Attribution**: AI là cause rõ (High) hay khó tách (Low)?

Quadrant quyết định pricing model tự nhiên:

```text
                Low Attribution        High Attribution
Low Autonomy    Seat / Flat            Hybrid (Seat + Credits)
                (Grammarly)            (Cursor)
High Autonomy   Usage-based            Outcome-based
                (OpenAI API)           (Intercom Fin)
```

File: `worksheet/02-pricing-value/1-attribution-autonomy.md`

### Phase 2 — Pricing Model + Value Metric (10 phút)

Chọn 1 trong 4 pricing model + đặt giá cụ thể + chọn value metric pass 3-part test.

Kiểm tra Usage Anxiety risk nếu pricing có usage element.

File: `worksheet/02-pricing-value/2-pricing-model-choice.md`

### Phase 3 — Chốt Monthly Value + ROI (15 phút)

Tính NET time saved (không Gross):

```text
NET = Original - AI wait - Human review - Context switch - Rework
```

Monthly Value formula:

```text
Gross = Volume × NET time × (Hourly rate / 60)
Adjusted = Gross × Adoption% × Quality%
NET Value = Adjusted - Rework cost
```

ROI = Monthly Value / Monthly Cost.

**Realistic check**:

- Adoption > 80% → cần data hard.
- Quality > 85% → cần POC data.
- NET > 80% Gross → check overhead.
- ROI > 20:1 → likely overestimate.

---

## Step 3 — Stress Test + Verdict (11:30–12:10, 40 phút)

Mục tiêu: test ROI có sống dưới 5 scenarios + combined worst → chốt verdict.

File cuối: `worksheet/03-stress-test/3-FINAL-stress-test-verdict.md` (= Section D)

### Phase 1 — 5 Stress Scenarios (20 phút)

Mỗi scenario thay đổi 1 biến:

| # | Scenario | Change |
|---|---|---|
| 1 | Base | Control — no change |
| 2 | Heavy usage | Volume × 2-3 (power user pattern) |
| 3 | Low adoption | Adoption 30-40% (pilot fail mode) |
| 4 | Quality failure | Quality 50-60% (model issue) |
| 5 | Provider shock | API cost × 2-3 (deprecate / repricing) |

Combined worst = 2 scenarios xấu nhất xảy ra đồng thời.

File: `worksheet/03-stress-test/1-scenario-table.md`

### Phase 2 — Verdict Draft (10 phút)

Apply criteria:

| Criteria | GO | CONDITIONAL | NO-GO |
|---|---|---|---|
| Base ROI | > 3:1 | 1.5-3:1 | < 1.5:1 |
| Survives X/5 | 4-5 | 2-3 | 0-1 |
| Combined worst | > 1.5:1 | 1-1.5:1 | < 1:1 |

CONDITIONAL là phổ biến nhất (70%+ AI pilot). GO chỉ khi base ROI > 3:1 AND survives 4/5 AND combined > 1.5:1.

File: `worksheet/03-stress-test/2-verdict-draft.md`

### Phase 3 — Chốt Section D (10 phút)

Gộp vào FINAL với 8 sub-section (D.1 Stress Table → D.8 Changes nếu NO-GO).

Conditions cứng (nếu CONDITIONAL): 3-5 điều kiện measurable + timed + action.

---

## Challenge Brief Bank — 10 briefs

Mỗi cặp nhận 1 trong 10 brief. Chi tiết trong `challenge-brief-bank.md`.

| # | Brief | Domain |
|---|---|---|
| 1 | AI Support Copilot | B2B SaaS customer support (FULL example) |
| 2 | AI Content Moderator | Social platform trust & safety |
| 3 | AI Medical Triage Assistant | Bệnh viện cấp cứu |
| 4 | AI Legal Contract Reviewer | Văn phòng luật M&A |
| 5 | AI Sales Email Generator | E-commerce B2B sales |
| 6 | AI Code Review Assistant | Fintech engineering |
| 7 | AI Inventory Forecaster | Retail chain supply chain |
| 8 | AI Student Essay Grader | University grading |
| 9 | AI Insurance Claim Processor | Bảo hiểm phi nhân thọ |
| 10 | AI Real Estate Listing Generator | Đại lý bất động sản |

---

## Tài liệu trong thư mục này

| File / Thư mục | Dùng để làm gì |
|---|---|
| `challenge-brief-bank.md` | 10 challenge brief (1 cặp 1 brief) |
| `glossary.md` | Bảng thuật ngữ Day 27 (cost, pricing, value, stress test, verdict) |
| `worksheet/00-context.md` | Điền bối cảnh nhóm + brief assigned 1 lần đầu buổi |
| `worksheet/00-worked-example.md` | 📖 Bản Economics Sheet đã điền cho Brief #1 — đọc trước Lab để biết mức chi tiết mong đợi |
| `worksheet/01-cost-model/` | Step 1 — 3 files (1-usage-unit, 2-cost-research, 3-FINAL-cost-model) |
| `worksheet/02-pricing-value/` | Step 2 — 3 files |
| `worksheet/03-stress-test/` | Step 3 — 3 files |
| `worksheet/04-FINAL-economics-sheet.md` | 🎯🎯 MASTER file — gộp 4 sections |
| `prompts/` | 10 prompt tham khảo cho từng phase |

---

## Bảng dùng prompt tham khảo

| Prompt tham khảo | Dùng khi nào | Lưu kết quả vào |
|---|---|---|
| `prompts/01-define-usage-unit.md` | Define usage unit (Step 1 Phase 1) | `01-cost-model/1-usage-unit.md` |
| `prompts/02-cost-formula.md` | Tra pricing + tính cost/task (Step 1 Phase 2) | `01-cost-model/2-cost-research.md` |
| `prompts/03-attribution-autonomy.md` | Định vị ma trận 2×2 (Step 2 Phase 1) | `02-pricing-value/1-attribution-autonomy.md` |
| `prompts/04-pricing-model-choice.md` | Chốt pricing model (Step 2 Phase 2) | `02-pricing-value/2-pricing-model-choice.md` |
| `prompts/05-value-formula.md` | Tính Monthly Value (Step 2 Phase 3) | `02-pricing-value/3-FINAL` Section C |
| `prompts/06-roi-analysis.md` | Tính ROI + sensitivity (Step 2 Phase 3) | `02-pricing-value/3-FINAL` Section C.6 + C.7 |
| `prompts/07-stress-scenario.md` | Build 5 scenarios (Step 3 Phase 1) | `03-stress-test/1-scenario-table.md` |
| `prompts/08-verdict-writing.md` | Viết verdict + conditions (Step 3 Phase 2) | `03-stress-test/2-verdict-draft.md` |
| `prompts/09-cross-brief-comparison.md` | So sánh kết quả với cặp khác brief (post-lab) | `04-FINAL-economics-sheet.md` (phần Comparison) |
| `prompts/10-presentation-prep.md` | Chuẩn bị 6 phút trình bày (cuối lab) | Script / slides riêng |

---

## Cách dùng prompt tham khảo

1. Mở Claude / ChatGPT / Gemini / Perplexity tuỳ bước.
2. Đưa toàn bộ `worksheet/00-context.md` + brief (từ `challenge-brief-bank.md`) vào đầu cuộc trò chuyện.
3. Đưa thêm các file đã làm ở phase trước (vd: `1-usage-unit.md` cho prompt 02; `3-FINAL-cost-model.md` cho prompt 05).
4. Chọn prompt tham khảo phù hợp từ thư mục `prompts/`, rồi chỉnh lại theo bối cảnh nhóm.
5. AI tạo bản nháp.
6. Nhóm đọc lại, sửa, kiểm chứng, rồi lưu vào đúng file bài tập.

AI chỉ hỗ trợ dựng bản nháp. Nhóm vẫn chịu trách nhiệm:

- Click URL pricing để kiểm tra.
- Justify mỗi % (adoption, quality).
- Sanity check ROI (>20:1 hay <1:1 = audit).
- Defend verdict trước Q&A.

### Lưu ý quan trọng khi dùng AI

- **Đừng để AI bịa pricing**: AI có thể bịa số cho model mới hoặc deprecated. Luôn click URL pricing page.
- **Đừng để AI viết verdict cuối**: AI tổng hợp tốt nhưng không có quan điểm — nhóm phải tự đưa verdict + defend.
- **Đừng để AI optimist quá**: AI có xu hướng đặt adoption 80%+ và quality 90%+. Reality check theo benchmark.

---

## Checklist trước khi nộp

### Step 1 — Cost Model

- [ ] Usage unit pass 3-part test (đếm, tốn token, có giá trị).
- [ ] Pilot daily volume tính theo công thức (pilot/total × team daily).
- [ ] Có URL pricing source cho provider + model.
- [ ] Cost/task tính theo công thức tokens (không "estimate").
- [ ] Human review cost include nếu brief có constraint.
- [ ] Setup cost amortize theo tháng pilot.
- [ ] Monthly cost formula có 4 component cộng lại = total.
- [ ] Budget check so với brief field #8.

### Step 2 — Pricing/Access + Value/ROI

- [ ] Attribution × Autonomy positioning có justification.
- [ ] Pricing model rõ (1 trong 4) + giá cụ thể.
- [ ] Value metric pass 3-part test.
- [ ] Real-world analog có URL.
- [ ] Usage Anxiety đánh giá Low/Med/High.
- [ ] NET time saved = Gross − wait − review − switch − rework.
- [ ] Adoption + Quality có justification.
- [ ] ROI là số cụ thể (___ : 1).
- [ ] Realistic check (không > 20:1 hoặc < 1:1 không lý do).

### Step 3 — Stress Test + Verdict

- [ ] 5 scenarios có cost + value + ROI mới + status.
- [ ] Combined worst case dùng 2 scenarios xấu nhất.
- [ ] Break-even adoption + quality tính (optional but +).
- [ ] Verdict CHỌN rõ (GO / CONDITIONAL / NO-GO).
- [ ] Nếu CONDITIONAL: 3-5 conditions với measurement + timeline + action.
- [ ] 3-5 monitoring metrics với threshold.
- [ ] Stop/pivot trigger cụ thể (số + thời gian + action).

### Master FINAL

- [ ] Executive summary 1-2 câu cho buyer.
- [ ] Section A đủ 8 sub-sections.
- [ ] Section B đủ 4 sub-sections.
- [ ] Section C đủ 7 sub-sections.
- [ ] Section D đủ 8 sub-sections.
- [ ] 3 cross-section insights.
- [ ] Comparison D26 (nếu có overlap).

### Nộp

- [ ] Kho GitHub công khai, tên đúng cú pháp `Day27-MãNhóm`, mở được.
- [ ] README đầu kho có bảng mã học viên + tên đầy đủ + brief # + verdict.
- [ ] File MASTER `04-FINAL-economics-sheet.md` có thể click trực tiếp từ README.
- [ ] Link kho bài đã nộp qua LMS trước **23:59**.

---

## Lỗi hay mắc

| Đừng làm | Nên làm |
|---|---|
| Bỏ qua `00-context.md` | Điền bối cảnh + brief # + 5 con số chính trước khi vào lab |
| Nộp mỗi file MASTER | Giữ cả 9 file trung gian (3 file × 3 step) cho người chấm thấy process |
| Usage unit "AI hỗ trợ X" | Cụ thể "1 ___" pass 3-part test |
| Dùng full-team volume | PILOT volume (pilot/total × team daily × 22) |
| Cost/task = $0 (quên pricing) | Click URL pricing, tính theo tokens |
| Pricing chỉ API, quên review | Human review cost thường dominate (50-90%) |
| Setup cost = $0 | Setup luôn có (integration + prompt engineering) |
| Adoption 100% / Quality 95% | Realistic: 50-80% adoption, 60-85% quality |
| Gross time saved (không trừ overhead) | NET = Gross − wait − review − switch − rework |
| ROI > 20:1 không question | Audit assumption, recalc conservative |
| ROI < 1:1 NO-GO ngay | Identify lever (cheaper model, broader pilot) trước |
| Verdict GO chắc chắn | CONDITIONAL với conditions cứng defendable hơn |
| Conditions chung chung "track adoption" | Conditions cụ thể: "Adoption ≥ 60% tháng 1, weekly check" |
| Combined worst = 1 scenario | Combined = 2 scenarios đồng thời |
| Bỏ stop trigger | Trigger = số + thời gian + action cụ thể |
| Đặt tên kho `Day-27-team-final` | Đúng cú pháp `Day27-MãNhóm` (vd: `Day27-G007`) |

---

## Liên kết với D26 và D28

Day 27 là cầu nối giữa D26 (Strategy) và D28 (Defense):

- **D26 input**: Evidence Board (4 Lens + Spark/Loop/System) — biết product chiến lược nào survive.
- **D27 build**: Economics Sheet (Cost + Pricing + Value + Stress Test + Verdict) — biết product nào survive **về kinh tế**.
- **D28 defense**: Combine D26 + D27, present trước panel CTO/CFO/mentor, defend bằng cả strategic + economic logic.

Trước khi kết thúc D27, nhóm nên chuẩn bị thêm cho D28:

- Review verdict + conditions kỹ — buyer sẽ probe.
- Anticipate 5 câu hỏi khó nhất (xem `prompts/10-presentation-prep.md`).
- Slide chuẩn bị riêng (PDF / Google Slides) — không trong worksheet.

Đường dẫn cuối: D26 Evidence Board → **D27 Economics Sheet** → D28 Approval Bundle.

---

## Lời khuyên cuối

1. **Mỗi số phải có công thức**. Đây là kỷ luật của Day 27.
2. **CONDITIONAL không phải thất bại**. CONDITIONAL với conditions cứng > GO chắc chắn không stress test.
3. **Buyer view luôn quan trọng**. Mỗi quyết định hỏi: CTO/CFO có defend được không?
4. **Iterate prompt 1-2 lần** trước khi paste vào worksheet. AI bản nháp đầu thường lạc quan.
5. **Glossary là bạn**. Khi gặp thuật ngữ → tham chiếu `glossary.md` trước khi prompt AI.

Chúc nhóm có 1 ngày Build thành công. Mai gặp ở D28 Defense — mang theo cả D26 và D27.
