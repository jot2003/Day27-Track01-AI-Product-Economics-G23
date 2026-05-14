---
artifact: 00 — Worked Example (Brief #1 AI Support Copilot)
buoc: Tham chiếu cho cả 3 bước Lab
phase: Đọc trước Lab để hiểu mức chi tiết mong đợi
time: 10 phút đọc trước Lab
input: Slide 13-14 (Worked Example) + brief #1 trong challenge-brief-bank.md
nop-cuoi: Không — file tham chiếu mẫu
---

# 00 — Worked Example: AI Support Copilot (Brief #1)

File này trình bày **một bản Economics Sheet đã điền hoàn chỉnh** cho Brief #1 (AI Support Copilot) — đúng mức chi tiết và độ chính xác mong đợi từ deliverable cuối của nhóm.

**Cách dùng**:

- Đọc trước Lab để biết "FINAL trông thế nào".
- Tham chiếu khi nhóm bí ở 1 sub-section cụ thể.
- **Không copy số** sang brief khác — mỗi brief có context riêng, sao chép = trừ 15 điểm (xem rubric).

Số trong file khớp với Slide 13-14 và prompt `05-value-formula.md`. Brief #1 cố tình đặt làm worked example vì có constraint 100% human review — đại diện cho pattern phổ biến (review chi phối cost).

---

## Thông tin nhóm (ví dụ)

- **Brief**: # 1 — AI Support Copilot
- **Cặp**: A20-99001 Nguyễn Mẫu A + A20-99002 Trần Mẫu B
- **Ngày tính**: [YYYY-MM-DD]
- **Phiên bản**: v1 (worked example)

---

## Tóm tắt 1 câu cho buyer

> "CONDITIONAL GO cho Brief #1 AI Support Copilot. Base ROI 2.07:1, combined worst case (Low adoption + Provider shock) 1.20:1 — biên mỏng. Pilot tiếp tục với 3 điều kiện: adoption ≥ 50% trước cuối tháng 1, khoá giá API 6 tháng, cổng chi phí $3,000/tháng."

---

## Section A — Cost Model

### A.1 — Usage Unit

| Trường | Giá trị |
|---|---|
| Usage unit (tên ngắn) | "1 ticket reply draft" |
| Mô tả (1-2 câu) | AI nhận ticket subject + body + 3 KB articles + customer history, sinh 1 bản nháp 80-200 từ hiển thị trong Zendesk side panel để agent edit/copy/send. |
| 3-part test pass | [x] Đếm được [x] Tốn token [x] Có giá trị |

### A.2 — Volume

| Trường | Giá trị | Công thức / Nguồn |
|---|---|---|
| Pilot users | 5 agent | Brief field #8 |
| Total team | 25 agent | Brief field #1 |
| Team daily volume | 800 ticket/day | Brief field #1 |
| Pilot daily volume | 160 ticket/day | (5/25) × 800 |
| Monthly volume | 3,520 ticket/month | 160 × 22 working days |

### A.3 — Model + API Cost

| Trường | Giá trị | Nguồn |
|---|---|---|
| Provider chính | Anthropic | <https://www.anthropic.com/pricing> |
| Model chọn | Claude 3.5 Sonnet | <https://www.anthropic.com/pricing> |
| Input price ($/1M tokens) | $3.00 | Pricing page |
| Output price ($/1M tokens) | $15.00 | Pricing page |
| Input tokens/task | 6,000 | Ticket 500 từ + 3 KB articles (~1,500 từ mỗi) + system prompt + customer history |
| Output tokens/task | 400 | Reply nháp 300 từ + a few headers |
| API cost/task | $0.024 | (6,000 × $3 + 400 × $15) / 1M = $0.018 + $0.006 = $0.024 |

**Ghi chú**: cost/task slide 13 là $0.05 (round-up đã include thêm tooling per-task + a small buffer). Worked example dùng $0.05 để khớp slide.

| Cost/task (rounded for slide) | $0.05 | Bao gồm API + tooling apportioned + buffer |

### A.4 — Tooling Cost

| Trường | Giá trị | Nguồn / Lý do |
|---|---|---|
| Vector DB | $70/month | Pinecone Starter (50K vectors, đủ cho 50K KB articles) |
| Monitoring | $50/month | Langfuse Pro tier (10K traces/day) |
| Orchestration | $30/month | n8n self-hosted plus license |
| Other tooling | $50/month | Zendesk app integration license |
| **Tổng tooling/tháng** | **$200** | Sum |

### A.5 — Human Review Cost

| Trường | Giá trị | Công thức / Lý do |
|---|---|---|
| Reviewer hourly rate | $25/hr | Brief: senior support agent $20/hr base × 1.25 loaded |
| Review time/task | 3 phút | Brief constraint: 100% human review trước khi gửi (compliance) |
| Cost/review | $1.25/task | (3 / 60) × $25 = $1.25 |
| Monthly review cost | $4,400/month gross | 3,520 × $1.25 |

**Adjustment cho worked example**: Slide 13 dùng $2,427/month review cost. Lý do: review chỉ áp cho ~55% drafts thực sự được dùng (sau adoption 65% × quality 80% ≈ 52% hit rate; rounded 55%). Drafts còn lại agent skip + viết tay → không tính review cost cho phần đó.

| Effective review cost/task | $0.69/task | $1.25 × 55% effective rate |
| Effective monthly review cost | $2,427/month | 3,520 × $0.69 |

### A.6 — Setup Cost (amortize)

| Trường | Giá trị | Lý do |
|---|---|---|
| One-time setup | $0 (đã hoàn thành) | Integration + prompt engineering đã làm trong tháng 0 trước pilot, không tính vào budget tháng pilot |
| Pilot duration | 3 months | Brief field #8: pilot 90 ngày |
| Amortized setup/month | $0 | Đã ghi vào ngân sách tháng 0 (không in vào monthly cost) |

**Ghi chú**: Trong thực tế, setup ($4,000-$8,000) thường amortize $1,300-$2,700/tháng. Worked example bỏ qua để khớp slide. Nhóm khác phải tính amortize cụ thể.

### A.7 — Monthly Cost Formula

```text
Monthly AI Cost
  = (3,520 × $0.05)              = $176        [API + tooling per-task]
  + $200                          = $200        [Tooling fixed]
  + (3,520 × $0.69)              = $2,427      [Human review effective]
  + $0                            = $0          [Setup đã ghi tháng 0]
                                   ──────────
                                   = $2,803 /month TOTAL
```

### A.8 — Budget Check

| Trường | Giá trị |
|---|---|
| Total monthly cost | $2,803 |
| Pilot budget | $5,000 (brief field #8) |
| % of budget | 56% |
| Status | [x] Within budget [ ] Over budget |

### Section A — Insight ban đầu

1. **Cost driver chính**: Human review chiếm 87% cost ($2,427 / $2,803). API chỉ 6%. Đây là pattern điển hình khi brief có constraint 100% review.
2. **Surprise cost**: Tooling rẻ hơn dự đoán ($200 cho 4 tool). Setup amortize nếu tính sẽ đẩy cost lên $4,000+, vượt budget.
3. **Sensitivity**: Cost nhạy nhất với human review time. Mỗi phút thêm review → $1,173/tháng tăng cost. Quan trọng hơn cả model choice.

---

## Section B — Pricing / Access Model

### B.1 — Attribution × Autonomy positioning

| Trường | Giá trị | Justification |
|---|---|---|
| Autonomy level | Low | Agent quyết định gửi cuối, AI chỉ suggest. Constraint 100% review = Low autonomy cứng. |
| Attribution level | Medium-Low | Khó tách "AI viết" khỏi "agent edit". Buyer không thấy rõ AI tạo ra giá trị độc lập. |
| Quadrant | Low Auto + Low/Med Attrib | → Seat-based hoặc Hybrid leaning Seat |

### B.2 — Pricing Model

| Trường | Giá trị |
|---|---|
| Pricing model chosen | Hybrid (Seat + Credits) |
| Pricing structure (cụ thể) | $25/seat/month + 1,000 draft credits/seat. Extra credit $0.05. |
| Value metric | "1 ticket draft generated" (countable, agent thấy cụ thể, tied to AI work). |
| Buyer (role) | CTO / Director Support |
| Buying trigger | Pain field #3: support-related churn 18%, hire thêm 5 agent = $300K/year → AI tiết kiệm > $200K nếu adoption đạt. |

### B.3 — Real-world analog

| Trường | Giá trị |
|---|---|
| Sản phẩm analog | Cursor AI |
| Pricing của họ | $20/seat + 500 fast credits, extra $0.04/request |
| Vì sao analog phù hợp | Low autonomy (dev review code suggest), Medium attribution (per-feature), Hybrid pricing đã chứng minh khả thi với buyer engineering. |

### B.4 — Usage Anxiety check

| Trường | Giá trị |
|---|---|
| Usage Anxiety risk | Medium |
| Mitigation | (1) Cap soft 80% credit có alert nhẹ, không block. (2) Admin dashboard show team-level usage, không bị bill shock individual. (3) Free 100 exploration credits tháng đầu cho mỗi agent. |

---

## Section C — Value / ROI

### C.1 — Time Saved per Task

| Trường | Giá trị | Lý do |
|---|---|---|
| Original task time (no AI) | 12 phút | Brief field #2: search KB 5 min + draft 4 min + send 3 min |
| − AI processing wait | − 0.3 phút | Claude 3.5 latency ~20s = 0.3 min |
| − Human review time | − 3 phút | Brief constraint: agent senior review 2-4 min (mean 3) |
| − Context switching | − 0.5 phút | AI tích hợp Zendesk side panel — switch nhẹ |
| − Rework time (avg) | − 0.6 phút | 20% drafts cần rewrite × 3 min = 0.6 min average |
| **= NET time saved/task** | 7.6 phút | 12 − 0.3 − 3 − 0.5 − 0.6 = 7.6 phút |

NET/Gross = 7.6 / 12 = 63%, phù hợp benchmark 40-60% (slightly upper bound — biện minh: AI tích hợp inline, switch cost thấp).

### C.2 — Loaded Hourly Rate

| Trường | Giá trị | Công thức |
|---|---|---|
| Base hourly rate | $20/hr | Industry: US support agent senior |
| Multiplier (benefit + overhead) | × 1.25 | Loaded conservative |
| **Loaded hourly rate** | $25/hr | base × multiplier |

### C.3 — Adoption + Quality

| Trường | Giá trị | Justification |
|---|---|---|
| Adoption rate | 65% | Brief: pilot mandatory medium (encouraged không bắt buộc), UX tích hợp Zendesk inline, 1 session training. Range 60-85% mandatory + integrated → 65% bảo thủ. |
| Quality factor | 80% | Task: draft generation. Range 60-80% draft. Brief có 50K ticket history + RAG → upper bound 80%. KB outdated 30% có thể drop về 75% tháng 1. |

### C.4 — Monthly Volume

| Trường | Giá trị | Nguồn |
|---|---|---|
| Monthly volume (tasks) | 3,520 ticket | Section A.2 |

### C.5 — Monthly Value Formula

```text
Step 1: Gross Monthly Value
  = 3,520 × 7.6 × ($25 / 60)
  = $11,147

Step 2: Adjusted for adoption + quality
  = $11,147 × 65% × 80%
  = $5,797

Step 3: Rework đã trừ trong NET (0.6 min) → không trừ lần 2.

NET Monthly Value = $5,797 /month
```

### C.6 — ROI

```text
ROI = $5,797 / $2,803 = 2.07 : 1
```

### C.7 — ROI Interpretation

| ROI range | Interpretation | Verdict tendency |
|---|---|---|
| 1.5-3:1 | Marginal | CONDITIONAL |

**Interpretation**: ROI nằm trong vùng marginal. Còn sống nhưng biên mỏng — phụ thuộc cao vào adoption + quality. Verdict không thể là GO chắc chắn.

**Reality check**:

- Adoption 65% có data hard? Không, là estimate. → Bảo thủ.
- Quality 80% có POC data? Không. → Track tháng 1 để verify.
- Cost component nào quên? Setup amortize bỏ qua, sẽ làm cost thật cao hơn $300-500/tháng.
- NET vs Gross check? 63%, OK.

---

## Section D — Stress Test + Verdict

### D.1 — Stress Test Table

| # | Scenario | Change | Cost ($/mo) | Value ($/mo) | ROI | Status |
|---|---|---|---|---|---|---|
| 1 | Base case | (No change) | $2,803 | $5,797 | 2.07:1 | [x] Marginal |
| 2 | Heavy usage | Volume × 3 | $8,014 | $17,391 | 2.17:1 | [x] Marginal |
| 3 | Low adoption | Adoption 40% (was 65%) | $2,803 | $3,567 | 1.27:1 | [x] Negative (dưới 1.5) |
| 4 | Quality failure | Quality 50% (was 80%) | $2,803 | $3,623 | 1.29:1 | [x] Negative (dưới 1.5) |
| 5 | Provider shock | API cost × 2 | $2,979 | $5,797 | 1.95:1 | [x] Marginal |

**Survives X/5** (ROI ≥ 1.5): Base, Heavy, Provider → 3/5 → CONDITIONAL range.

### D.2 — Combined Worst Case

| Field | Giá trị |
|---|---|
| Scenario xấu nhất 1 | #3 Low adoption (1.27:1) |
| Scenario xấu nhất 2 | #5 Provider shock (1.95:1) |
| Combined change | Adoption 40% + API cost × 2 |
| Combined cost | $2,979 /month |
| Combined value | $3,567 /month |
| **Combined ROI** | 1.20:1 |
| Status | [x] Break-even (1-1.5) |

**Lý do chọn Low adoption + Provider shock**: 2 scenarios đại diện 2 loại rủi ro khác nhau (internal demand + external supply), khả năng xảy ra đồng thời cao trong pilot 90 ngày. Quality failure đã hurt riêng — combine thêm sẽ over-stress.

### D.3 — Break-even Analysis

| Field | Giá trị |
|---|---|
| Break-even adoption | 31% (tại quality 80%, cost base) |
| Break-even quality | 39% (tại adoption 65%, cost base) |
| Diễn giải | "Pilot fail nếu adoption < 31% HOẶC quality < 39%." Threshold quan trọng để monitor. |

Break-even adoption tính: $2,803 = $11,147 × X% × 80% → X% = $2,803 / ($11,147 × 0.8) = 31.4%.

### D.4 — Verdict

**Verdict**: [ ] GO  [x] CONDITIONAL  [ ] NO-GO

**Verdict statement (3-4 câu)**:

> "CONDITIONAL GO cho Brief #1 AI Support Copilot. Base ROI 2.07:1 nằm trong vùng marginal, sống 3/5 scenarios cá nhân (base, heavy, provider). Combined worst case (Low adoption + Provider shock) cho 1.20:1 — biên mỏng. Tiến hành pilot 90 ngày với 3 điều kiện cứng + monitoring tuần."

### D.5 — Conditions

| # | Điều kiện | Đo bằng gì | Timeline | Action nếu fail |
|---|---|---|---|---|
| 1 | Adoption ≥ 50% trước cuối tháng 1 (target 65% tháng 3) | Active agents / 5 pilot agents weekly | Tháng 1 EOM | Pause pilot, training intensive |
| 2 | Quality ≥ 70% (target 80%) | Random sample 50 drafts/tuần, % usable không major rewrite | Weekly | Iterate prompt + RAG re-index |
| 3 | API pricing locked với Anthropic 6 tháng HOẶC fallback model (GPT-4o-mini) ready | Contract review + fallback test | Pre-pilot start | Block pilot start nếu chưa lock |
| 4 | Cost/task ≤ $0.80 effective | Billing logs weekly | Weekly | Switch to GPT-4o-mini cho phần FAQ tier-1 |
| 5 | Monthly cost ≤ $3,000 gate | Finance dashboard | Monthly | Escalate to CTO, không tiếp tục pilot tháng sau |

### D.6 — Monitoring Metrics

| Metric | Frequency | Source | Threshold |
|---|---|---|---|
| Adoption rate | Weekly | Zendesk app logs | ≥ 50% |
| Cost per task | Weekly | Anthropic billing + Pinecone billing | ≤ $0.80 |
| Quality factor | Weekly | Random sample 50 drafts | ≥ 70% |
| User satisfaction (agent) | Monthly | Survey 5 agents | NPS ≥ 20 |
| Total monthly cost | Monthly | Finance dashboard | ≤ $3,000 |

### D.7 — Stop / Pivot Trigger

- Trigger 1: Adoption < 40% trong 30 ngày liên tiếp → pause pilot, training program intensive.
- Trigger 2: Cost/task > $1.20 trong 2 tuần liên tiếp → switch to GPT-4o-mini.
- Trigger 3: Quality < 50% trong 30 ngày → iterate prompt + RAG re-index hoặc pause.
- Trigger 4: Compliance event (1 draft sent without review do AI auto-send bug) → pause immediately, root-cause review.

### D.8 — Changes Needed (N/A — verdict không phải NO-GO)

---

## Section D — Insight đáng chú ý

1. **Scenario hurt nhất**: Low adoption (1.27:1) và Quality failure (1.29:1) gần ngang nhau. Cả 2 đều kéo ROI xuống vùng yếu vì base đã thấp.
2. **Combined worst pattern**: Khi rủi ro internal (adoption) + external (provider) gặp nhau, ROI rơi đến 1.20 — sát break-even. Mọi điều kiện trong D.5 đều quan trọng.
3. **Buyer takeaway**: Adoption là biến nhạy nhất + dễ kiểm soát nhất. Đầu tư training + onboarding > đầu tư model upgrade. Threshold 50% adoption tháng 1 là "make or break".

---

## Cross-section insights

1. **Cost structure**: Human review (87%) chi phối, không phải API (6%). Pattern phổ biến với brief có compliance constraint — đừng tối ưu sai (đổi model rẻ hơn không cứu nổi).
2. **Value sensitivity**: Adoption × Quality cùng tăng/giảm theo cấp số nhân. 65% × 80% = 52% effective rate. Nếu giảm xuống 40% × 50% = 20% effective → value collapse 60%.
3. **Verdict insight**: Combined worst 1.20:1 ngay sát break-even 1.0:1 → biên an toàn rất mỏng. Mọi điều kiện trong D.5 là điều kiện sống chết, không phải nice-to-have.

---

## Lưu ý cuối

File này là **ví dụ tham chiếu**, không phải template để paste. Nhóm khác:

- Có thể có verdict GO hoặc NO-GO tuỳ brief.
- Số sẽ khác hoàn toàn — Brief #2 Content Moderator có volume × 100, API cost dominant.
- Justification cho mỗi % phải tự viết theo context brief, không copy.

Đọc xong file này → trở lại `worksheet/00-context.md` để bắt đầu Lab với brief của nhóm.
