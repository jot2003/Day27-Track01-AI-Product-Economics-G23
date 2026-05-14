---
artifact: 3 — FINAL Stress Test + Verdict (Section D của Economics Sheet)
buoc: 3 — Stress Test + Verdict
phase: Chốt Section D
time: 10 phút (xem deck slide 4 để biết khung giờ chính xác trong buổi)
input: 1-scenario-table.md + 2-verdict-draft.md
nop-cuoi: Có — section D nộp trong 04-FINAL-economics-sheet.md
---

# 3 — FINAL Stress Test + Verdict — Section D của Economics Sheet

Đây là file cuối của Step 3 Lab. Gộp Section D — Stress Test (5 scenarios + combined) + Verdict (decision + conditions / changes).

Mục tiêu: chốt Section D với bảng 5 scenarios hoàn chỉnh + combined worst case + verdict actionable.

Quy tắc:

- Bảng phải có cost / value / ROI mới cho từng scenario.
- Verdict phải có conditions / changes cụ thể với timeline.
- Đây là phần buyer (CTO / VP) sẽ đọc kỹ nhất.

---

## Thông tin nhóm

- **Brief**: # ___ — [tên brief]
- **Cặp**: [tên + mã học viên × 2]
- **Ngày tính**: [YYYY-MM-DD]
- **Phiên bản**: v1

---

## Section D — Stress Test + Verdict

### D.1 — Stress Test Table

| # | Scenario | Change | Cost ($/mo) | Value ($/mo) | ROI | Status |
|---|---|---|---|---|---|---|
| 1 | Base case | (No change — control) | $___ | $___ | ___:1 | ☐ Viable ☐ Marginal ☐ Negative |
| 2 | Heavy usage | Volume × ___ | $___ | $___ | ___:1 | ☐ Viable ☐ Marginal ☐ Negative |
| 3 | Low adoption | Adoption ___% (was ___%) | $___ | $___ | ___:1 | ☐ Viable ☐ Marginal ☐ Negative |
| 4 | Quality failure | Quality ___% (was ___%) | $___ | $___ | ___:1 | ☐ Viable ☐ Marginal ☐ Negative |
| 5 | Provider shock | API cost × ___ | $___ | $___ | ___:1 | ☐ Viable ☐ Marginal ☐ Negative |

### D.2 — Combined Worst Case

| Field | Giá trị |
|---|---|
| Scenario xấu nhất 1 | # ___ (___:1) |
| Scenario xấu nhất 2 | # ___ (___:1) |
| Combined change | [vd: Adoption 30% + API cost × 2] |
| Combined cost | $___ /month |
| Combined value | $___ /month |
| **Combined ROI** | ___:1 |
| Status | ☐ Robust ☐ Survivable ☐ Break-even ☐ Risky ☐ Critical |

### D.3 — Break-even Analysis (optional but recommended)

| Field | Giá trị |
|---|---|
| Break-even adoption | ___% (tại quality = base) |
| Break-even quality | ___% (tại adoption = base) |
| Diễn giải | "Pilot fail nếu adoption < ___ HOẶC quality < ___" |

### D.4 — Verdict

**Verdict**: ☐ GO  ☐ CONDITIONAL  ☐ NO-GO

**Verdict statement** (3-4 câu):

[...]

[...]

[...]

[...]

### D.5 — Conditions (nếu CONDITIONAL)

| # | Điều kiện | Đo bằng gì | Timeline | Action nếu fail |
|---|---|---|---|---|
| 1 | [vd: Adoption ≥ 60% trong tháng 1] | Active users / pilot total | Tháng 1 EOM | Pause review |
| 2 | [vd: Cost/task ≤ $0.05] | Cost per AI call (logs) | Weekly | Switch to cheaper model |
| 3 | [vd: Quality ≥ 70%] | Random sample 50 tasks/week | Weekly | Iterate prompt |
| 4 | [vd: Customer satisfaction NPS ≥ 30] | Survey end of month | Monthly | Re-evaluate |
| 5 | [vd: Provider lock — contract 6 tháng] | Vendor agreement | Pre-pilot | Setup fallback model |

### D.6 — Monitoring Metrics

3-5 metrics nhóm sẽ track hàng tuần / hàng tháng:

| Metric | Frequency | Source | Threshold |
|---|---|---|---|
| Adoption rate | Weekly | Usage logs | ≥ ___% |
| Cost per task | Weekly | Billing logs | ≤ $___ |
| Quality factor | Weekly | Sample 50 tasks | ≥ ___% |
| User satisfaction | Monthly | Survey | NPS ≥ ___ |
| Total monthly cost | Monthly | Finance | ≤ $___ |

### D.7 — Stop / Pivot Trigger

Trigger cụ thể: nếu 1 trong các điều kiện sau xảy ra → pause pilot và re-evaluate.

- Trigger 1: [Adoption < ___% trong 30 ngày liên tiếp]
- Trigger 2: [Cost/task > $___ trong 2 tuần liên tiếp]
- Trigger 3: [Quality < ___% trong 30 ngày]
- Trigger 4: [Compliance / risk event nghiêm trọng]

### D.8 — Changes Needed (nếu NO-GO)

Nếu NO-GO — không phải dừng, mà là "cần thay đổi gì để khả thi":

| # | Change | Tác động ROI dự kiến |
|---|---|---|
| 1 | [vd: Đổi từ Claude 3.5 sang GPT-4o-mini cho task simple] | Cost giảm 80%, ROI tăng từ 0.8:1 lên 2.1:1 |
| 2 | [vd: Mở rộng pilot từ 5 lên 20 user] | Amortize setup tốt hơn, ROI tăng |
| 3 | [vd: Renegotiate constraint 100% human review] | Giảm review cost, ROI tăng |

**Loại NO-GO**:

- ☐ "Not now" — có thể revisit khi A, B, C
- ☐ "Not ever" — fundamentally không phù hợp

---

## Section D — Insight đáng chú ý

Sau khi stress test, ghi 2-3 insight:

1. **Scenario hurt nhất**: [vd: "Low adoption hurt nhất — vì cost fixed, value giảm trực tiếp theo % adoption"]
2. **Combined worst pattern**: [vd: "Adoption + Quality cùng giảm khiến ROI sụp nhanh hơn từng cái riêng"]
3. **Buyer takeaway**: [vd: "Buyer cần biết adoption là biến quan trọng nhất, đầu tư training quan trọng hơn đầu tư model"]

---

## Checklist nộp Section D

- [ ] Bảng D.1 — 5 scenarios có cost + value + ROI mới + status.
- [ ] Bảng D.2 — Combined worst case dùng 2 scenarios xấu nhất.
- [ ] Bảng D.3 — Break-even adoption + quality (optional but +)
- [ ] D.4 — Verdict CHỌN rõ + statement 3-4 câu.
- [ ] D.5 — Nếu CONDITIONAL: 3-5 conditions với measurement + timeline + action.
- [ ] D.6 — 3-5 monitoring metrics với threshold.
- [ ] D.7 — Stop/pivot trigger cụ thể.
- [ ] D.8 — Nếu NO-GO: 2-3 changes với tác động ROI dự kiến.

Đếm số trường đã điền: ___ / 35+ trường

Yêu cầu tối thiểu: 28 trường có số / quyết định cụ thể.

---

## Anti-pattern

| Đừng làm | Nên làm |
|---|---|
| Stress test ROI giống nhau cả 5 scenarios | Ít nhất 1-2 scenarios phải hurt rõ |
| Combined = scenario 5 đơn lẻ | Combined = 2 scenarios đồng thời |
| Verdict không có conditions | CONDITIONAL phải có 3-5 conditions |
| Conditions = "sẽ track adoption" | Conditions = "Adoption ≥ 60% trong tháng 1" |
| Stop trigger = "nếu pilot fail" | Stop trigger = "Adoption < 40% trong 30 ngày" |
| NO-GO không nói changes | NO-GO = "cần đổi A, B, C để khả thi" |
| Bỏ insight ban đầu | Mọi Section đều có 2-3 insight rút ra |

---

## Next: Master FINAL Economics Sheet

Sau khi chốt Section D, đã đủ 4 sections. Gộp tất cả vào `worksheet/04-FINAL-economics-sheet.md` — đây là deliverable cuối cùng nộp lên LMS.

Khi gộp, đặt thứ tự: A (Cost) → B (Pricing) → C (Value/ROI) → D (Stress Test + Verdict).
