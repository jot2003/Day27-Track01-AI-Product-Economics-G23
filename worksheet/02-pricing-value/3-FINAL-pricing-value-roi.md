---
artifact: 3 — FINAL Pricing + Value + ROI (Section B + C của Economics Sheet)
buoc: 2 — Pricing/Access + Value/ROI
phase: Chốt Section B + C
time: 15 phút (xem deck slide 4 để biết khung giờ chính xác trong buổi)
input: 1-attribution-autonomy.md + 2-pricing-model-choice.md + prompts/05-value-formula.md + prompts/06-roi-analysis.md
nop-cuoi: Có — section B + C nộp trong 04-FINAL-economics-sheet.md
---

# 3 — FINAL Pricing + Value + ROI — Section B + C của Economics Sheet

Đây là file cuối của Step 2 Lab. Gộp Section B (Pricing/Access) + Section C (Value/ROI) vào 1 file.

Mục tiêu: chốt pricing model, tính monthly value, tính ROI, kiểm tra ROI có làm sense không.

Quy tắc:

- Mỗi % trong formula phải có justification (vd: adoption 70% vì lý do A, B).
- ROI = Monthly Value / Monthly Cost. Số cụ thể, không "khoảng".
- Nếu adoption > 80% hoặc quality > 90% → bắt buộc justify đặc biệt.

---

## Thông tin nhóm

- **Brief**: # ___ — [tên brief]
- **Cặp**: [tên + mã học viên × 2]
- **Ngày tính**: [YYYY-MM-DD]
- **Phiên bản**: v1

---

## Section B — Pricing / Access Model

### B.1 — Attribution × Autonomy positioning

| Trường | Giá trị | Justification |
|---|---|---|
| Autonomy level | [Low / High] | [1 câu] |
| Attribution level | [Low / High] | [1 câu] |
| Quadrant | ___ | Auto + Attrib quadrant |

### B.2 — Pricing Model

| Trường | Giá trị |
|---|---|
| Pricing model chosen | ___ |
| Pricing structure (cụ thể) | [vd: $25/seat + 1,000 credits, $0.05/extra credit] |
| Value metric | ___ |
| Buyer (role) | ___ |
| Buying trigger | [pain point chính] |

### B.3 — Real-world analog

| Trường | Giá trị |
|---|---|
| Sản phẩm analog | ___ |
| Pricing của họ | ___ |
| Vì sao analog phù hợp | [1 câu] |

### B.4 — Usage Anxiety check

| Trường | Giá trị |
|---|---|
| Usage Anxiety risk | [Low / Medium / High] |
| Mitigation | [...] |

---

## Section C — Value / ROI

### C.1 — Time Saved per Task

Tính NET time saved, không phải GROSS:

| Trường | Giá trị | Lý do |
|---|---|---|
| Original task time (no AI) | ___ phút | Brief field #2 |
| − AI processing wait | − ___ phút | Latency của AI call |
| − Human review time | − ___ phút | Nếu brief có constraint review |
| − Context switching | − ___ phút | User switch tab/tool |
| − Rework time (avg) | − ___ phút | Khi quality fail, time fix |
| **= NET time saved/task** | ___ phút | Sum trừ |

**Quy tắc thực tế**: NET thường = 40-60% của GROSS. Nếu nhóm tính NET > 80% GROSS → có thể đã quên cost overhead.

### C.2 — Loaded Hourly Rate

| Trường | Giá trị | Công thức |
|---|---|---|
| Base hourly rate | $___ /hr | Lương cơ bản |
| Multiplier (benefit + overhead) | × 1.3-1.5 | Loaded |
| **Loaded hourly rate** | $___ /hr | base × multiplier |

### C.3 — Adoption + Quality

| Trường | Giá trị | Justification |
|---|---|---|
| Adoption rate | ___% | [Mandatory tool 60-85% / Optional 30-60% / New behavior 20-50% / Pilot incentive 50-80%] |
| Quality factor | ___% | [Classify 80-95% / Draft 60-80% / Summarization 70-85% / Creative 50-70% / Complex 40-65%] |

**Cảnh báo**:

- Adoption > 80% → phải có data hoặc lý do mạnh.
- Quality > 85% → phải có data từ POC hoặc benchmark.
- Cả hai > 90% → gần như chắc chắn overestimate.

### C.4 — Monthly Volume

| Trường | Giá trị | Nguồn |
|---|---|---|
| Monthly volume (tasks) | ___ | Section A.2 |

### C.5 — Monthly Value Formula

```text
Gross Monthly Value
  = Monthly volume × NET time saved (min) × (Hourly rate / 60)
  = ___ × ___ × ($___ / 60)
  = $___

Adjusted for adoption + quality
  = Gross × Adoption × Quality
  = $___ × ___% × ___%
  = $___ /month

Minus rework cost (already in NET? Nếu rework time đã trừ trong NET → bỏ qua bước này)
  − $___
  
= NET Monthly Value $___
```

### C.6 — ROI

```text
ROI = Monthly Value / Monthly Cost
    = $___ / $___
    = ___:1
```

### C.7 — ROI Interpretation

| ROI range | Interpretation | Verdict tendency |
|---|---|---|
| > 5:1 | Strong | Có thể GO (nhưng kiểm tra overestimate?) |
| 3-5:1 | Solid | Có thể GO |
| 1.5-3:1 | Marginal | CONDITIONAL |
| 1-1.5:1 | Weak | CONDITIONAL với điều kiện chặt (hoặc NO-GO nếu combined worst < 1:1) |
| < 1:1 | Negative | NO-GO |
| > 20:1 | Có thể overestimate | Check assumption |

**ROI của nhóm**: ___ : 1

**Interpretation**: [...]

**Reality check** (nhóm tự hỏi):

- Có quá lạc quan ở adoption? [Có / Không, lý do]
- Có quá lạc quan ở quality? [Có / Không, lý do]
- Có quên cost component nào ở Section A? [Có / Không]
- Có dùng GROSS time saved thay vì NET? [Có / Không]

---

## Section B + C — Insight ban đầu

Sau khi tính, ghi 2-3 insight:

1. **Value driver chính**: [vd: "Time saved chiếm 95% giá trị, chỉ 5% là quality improvement"]
2. **ROI sensitivity**: [Adoption hay quality nhạy hơn? Nếu adoption giảm 20% → ROI giảm bao nhiêu?]
3. **Buyer view**: [ROI này có defend được trước buyer (CTO/VP) không? Mức ROI nào họ chấp nhận thông thường?]

---

## Checklist nộp Section B + C

- [ ] Section B.1 — Quadrant cụ thể với justification.
- [ ] Section B.2 — Pricing model + giá cụ thể.
- [ ] Section B.3 — Real-world analog có nguồn.
- [ ] Section B.4 — Usage Anxiety đánh giá Low/Med/High với mitigation.
- [ ] Section C.1 — NET time saved tính theo công thức trừ overhead.
- [ ] Section C.2 — Loaded hourly rate có multiplier.
- [ ] Section C.3 — Adoption + Quality có justification.
- [ ] Section C.5 — Monthly Value tính theo 3 bước: Gross → Adjusted → NET.
- [ ] Section C.6 — ROI là số cụ thể (___ : 1).
- [ ] Section C.7 — Interpretation phù hợp với ROI range.

Đếm số trường đã điền: ___ / 25+ trường

Yêu cầu tối thiểu: 22 trường có số / giá trị cụ thể.

---

## Anti-pattern

| Đừng làm | Nên làm |
|---|---|
| "Adoption 100%" | Realistic: 50-80% pilot, justify |
| "Quality 95%" | Realistic: theo benchmark + brief |
| Dùng Gross time saved | NET = Gross − wait − review − switch − rework |
| ROI = 30:1 không question | Question — gần như chắc chắn overestimate |
| ROI < 1:1 đi tiếp luôn | Stop, check assumption hoặc đổi cách tiếp cận AI |
| Loaded rate = base salary | Loaded = base × 1.3-1.5 (benefit, overhead) |
| Quên context switching | Mỗi lần đổi tool/tab = thời gian thực |
| Pricing < cost/unit | Không bền vững — pricing phải > cost + margin |

---

## Next: Stress Test

Sau khi có ROI base case, chuyển sang `worksheet/03-stress-test/` để test xem ROI có sống dưới biến động không. ROI đẹp ở base case có thể sụp đổ ở stress test — đó là lúc verdict thực sự được quyết định.
