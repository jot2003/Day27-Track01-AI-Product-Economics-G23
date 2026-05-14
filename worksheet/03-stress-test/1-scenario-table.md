---
artifact: 1 — Bảng 5 stress scenarios
buoc: 3 — Stress Test + Verdict
phase: Điền bảng 5 kịch bản + ROI mới
time: 20 phút (xem deck slide 4 để biết khung giờ chính xác trong buổi)
input: 01-cost-model/3-FINAL-cost-model.md + 02-pricing-value/3-FINAL-pricing-value-roi.md + prompts/07-stress-scenario.md
nop-cuoi: Không — file trung gian
---

# 1 — Bảng 5 Stress Scenarios

Mục tiêu: tính lại ROI trong 5 kịch bản khác nhau để xem AI economics có "sống" được khi biến động.

Lý do làm bước này: ROI ở base case là dự đoán lạc quan. Trong thực tế, mọi giả định đều có thể sai. Stress test xem ROI có chịu được khi 1 biến đổi.

Quy tắc: **mỗi scenario chỉ thay đổi 1 biến**. Các biến khác giữ nguyên từ base case.

## Quy trình 20 phút

```text
2 phút  — Pull số từ base case (Section A + C)
14 phút — Điền 5 scenarios (mỗi cái 2-3 phút)
4 phút  — Tính combined worst case (2 scenarios xấu nhất đồng thời)
```

---

## Phần A — Base case Recap

Pull số từ FINAL Section A + C:

| Metric | Giá trị |
|---|---|
| Monthly Cost (base) | $___ |
| Monthly Value (base) | $___ |
| ROI (base) | ___ : 1 |
| Adoption rate (base) | ___% |
| Quality factor (base) | ___% |
| Monthly volume (base) | ___ tasks |
| Cost/task (base) | $___ |
| NET time saved/task | ___ phút |

---

## Phần B — 5 Scenarios Table

Điền cho từng scenario. Mỗi scenario: thay 1 biến, giữ nguyên 7 biến còn lại.

### Scenario 1 — Base case (control)

| Field | Giá trị |
|---|---|
| Change | (No change — control) |
| Cost | $___ (= base) |
| Value | $___ (= base) |
| **ROI** | ___ : 1 |
| Status | [Viable >3:1 / Marginal 1-3:1 / Negative <1:1] |

### Scenario 2 — Heavy Usage

User dùng nhiều hơn kỳ vọng (power user pattern).

| Field | Giá trị | Lý do |
|---|---|---|
| Change | Volume × ___ (2x / 3x / 5x) | Power user, scope creep |
| New monthly volume | ___ tasks | base volume × multiplier |
| New monthly cost | $___ | volume tăng → API + tooling per-task + human review per-task tăng |
| New monthly value | $___ | volume tăng → value tăng (cùng tỷ lệ) |
| **ROI** | ___ : 1 | Value / Cost |
| Status | [Viable / Marginal / Negative] |

**Lưu ý**: Heavy usage test xem **cost có blow up nhanh hơn value không**.

- Ví dụ Replit: margins âm vì user 20% dùng AI cực nhiều, cost vượt revenue.
- Nếu cost tăng tỉ lệ với volume, value cũng tăng tỉ lệ → ROI base = ROI heavy. Đó là dấu hiệu unit economics ổn.
- Nếu cost có "step" jump (vd: vượt enterprise tier) → ROI sụp.

### Scenario 3 — Low Adoption

Chỉ 30-40% user pilot thực sự dùng AI.

| Field | Giá trị | Lý do |
|---|---|---|
| Change | Adoption ___ % → ___ % | UX khó / training thiếu / user resist change |
| New monthly value | $___ | Gross × New adoption × Quality |
| Monthly cost | $___ | Fixed (infrastructure đã setup, không scale down dễ) |
| **ROI** | ___ : 1 | New value / cost |
| Status | [...] |

**Lưu ý**: Cost vẫn cố định (tooling subscription, setup amortize) ngay cả khi user không dùng → ROI nhạy mạnh với adoption.

### Scenario 4 — Quality Failure

AI output kém hơn dự đoán (chỉ 50-60% quality thay vì 80%).

| Field | Giá trị | Lý do |
|---|---|---|
| Change | Quality ___ % → ___ % | Model bug, edge case, KB outdated |
| Rework cost tăng | + $___/month | Time fix bad outputs |
| New monthly value | $___ | Gross × Adoption × New quality − Rework |
| Monthly cost | $___ | Có thể tăng nhẹ vì retry / regen |
| **ROI** | ___ : 1 | |
| Status | [...] |

### Scenario 5 — Provider Shock

Provider đổi giá (×2) hoặc deprecate model.

| Field | Giá trị | Lý do |
|---|---|---|
| Change | API cost × ___ (2x / 3x) | Provider tăng giá / model deprecated, switch to expensive replacement |
| New API cost/month | $___ | Old API cost × multiplier |
| New monthly cost | $___ | New API + tooling + review + setup |
| Monthly value | $___ | Same as base |
| **ROI** | ___ : 1 | |
| Status | [...] |

**Lưu ý thực tế**:

- Salesforce đổi giá AI 3 lần trong 18 tháng (2024).
- OpenAI giảm giá 280× trong 2 năm (good news, nhưng đừng dựa vào trend giảm tiếp).
- Anthropic Claude 3.5 deprecation timeline → buộc upgrade lên Claude 3.7 hoặc 4 (giá khác).

---

## Phần C — Combined Worst Case

Chọn 2 scenario xấu nhất từ 4 scenarios (2-5) → áp dụng đồng thời.

### Bước C1 — Identify 2 scenarios xấu nhất

Nhìn lại 4 scenarios (2-5), 2 cái có ROI thấp nhất là:

- **Scenario xấu nhất 1**: ___ — ROI ___ : 1
- **Scenario xấu nhất 2**: ___ — ROI ___ : 1

### Bước C2 — Combined calculation

Áp dụng 2 thay đổi đồng thời:

| Field | Giá trị | Công thức |
|---|---|---|
| Change 1 | ___ | (vd: Adoption 30%) |
| Change 2 | ___ | (vd: API cost × 2) |
| Combined cost | $___ | Áp cả 2 thay đổi lên cost |
| Combined value | $___ | Áp cả 2 thay đổi lên value |
| **Combined ROI** | ___ : 1 | |
| Status | [...] |

### Bước C3 — Interpretation

| Combined ROI | Interpretation | Verdict tendency |
|---|---|---|
| > 3:1 | Robust — sống tốt cả khi 2 biến động cùng lúc | GO |
| 1.5-3:1 | Survivable — sống được nhưng margin mỏng | GO |
| 1-1.5:1 | Break-even — cần mitigation plan | CONDITIONAL |
| 0.5-1:1 | Risky — cần redesign hoặc re-scope | NO-GO |
| < 0.5:1 | Critical — không bền — re-consider GO | NO-GO |

**Combined ROI của nhóm**: ___ : 1

**Interpretation**: [...]

---

## Phần D — Break-even Analysis (Optional but recommended)

Tính ngưỡng adoption hoặc quality mà ROI = 1:1 (break-even).

### Break-even adoption

Tại quality = base, hỏi: **adoption bao nhiêu thì ROI = 1:1?**

```text
Cost (fixed) = Gross Value × X% × Quality%
X% = Cost / (Gross Value × Quality%)
X% = $___ / ($___ × ___%) = ___%
```

**Break-even adoption**: ___%

Diễn giải: "Nếu adoption < ___%, ROI < 1:1 → pilot fail."

### Break-even quality

Tại adoption = base, hỏi: **quality bao nhiêu thì ROI = 1:1?**

```text
Cost = Gross Value × Adoption% × Y%
Y% = Cost / (Gross Value × Adoption%)
Y% = $___ / ($___ × ___%) = ___%
```

**Break-even quality**: ___%

---

## Phần E — Kiểm tra

Trước khi chuyển sang `2-verdict-draft.md`, rà soát:

- [ ] Tất cả 5 scenarios có cost + value + ROI cụ thể.
- [ ] Mỗi scenario chỉ thay đổi 1 biến.
- [ ] Heavy usage có lý do (vd: 2x volume vì power user 20% dùng 80% capacity).
- [ ] Low adoption có lý do (vd: 30% vì UX khó hoặc user mới quen 1 tháng đầu).
- [ ] Quality failure có lý do (vd: 50% vì KB outdated 30% + model thiếu domain).
- [ ] Provider shock có ví dụ thực tế (vd: Anthropic deprecate Claude 3.5 → buộc Claude 4 đắt hơn 60%).
- [ ] Combined worst case dùng 2 scenarios cụ thể (không "tất cả tệ").
- [ ] Break-even adoption + quality có tính (optional but recommended).

---

## Anti-pattern

| Đừng làm | Nên làm |
|---|---|
| "Heavy usage scenario: not applicable cho brief tôi" | Mọi brief đều có heavy usage risk — ít nhất scope creep |
| Low adoption = 50% (giống base) | Low scenario phải XẤU hơn base (vd: 30% nếu base = 70%) |
| Quality failure = 80% | Quality failure phải XẤU rõ (vd: 50%) — không phải tweak nhẹ |
| Provider shock = giá × 1.1 | Realistic shock = 2-3× hoặc model deprecated |
| Combined = chỉ scenario 5 | Combined PHẢI 2 scenarios xảy ra đồng thời |
| Quên rework cost trong quality fail | Quality fail → rework cost tăng đáng kể |
| Break-even ignore | Optional nhưng helpful — biết "ngưỡng sống chết" |

---

## Câu hỏi mở (cho `2-verdict-draft.md`)

- Câu hỏi 1: Scenario nào hurt nhất? Vì sao?
- Câu hỏi 2: Combined worst case có >1:1 không? Nếu không, redesign gì?
- Câu hỏi 3: Break-even adoption có realistic không?

Sau bước này, chuyển sang `2-verdict-draft.md` để viết verdict draft với điều kiện cụ thể.
