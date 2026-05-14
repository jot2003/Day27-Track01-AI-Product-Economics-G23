# Prompt tham khảo 6 — Tính ROI Ratio + Break-even

**Dùng khi**: nhóm đã có Monthly Cost + Monthly Value, cần tính ROI và đánh giá interpretation + break-even thresholds.
**Công cụ gợi ý**: Claude Sonnet/Opus, ChatGPT-4o.
**Lưu kết quả vào**: Section C.6 + C.7 trong `worksheet/02-pricing-value/3-FINAL-pricing-value-roi.md`
**Thời gian**: 10 phút

---

## Trước khi vào prompt — 5 câu hỏi nhóm tự trả lời

1. **Monthly Cost** đã tính: $___.
2. **Monthly Value** đã tính: $___.
3. **ROI ratio** = Value / Cost = ___:1. (Tự tính trước.)
4. **Range interpretation** (xem bảng trong `3-FINAL-pricing-value-roi.md`).
5. **Có ROI hợp lý** so với industry / brief tier?

> **Cảnh báo**: ROI > 20:1 hoặc < 1:1 là dấu hiệu cần kiểm tra lại. ROI > 20:1 = thường overestimate value. ROI < 1:1 = pivot hoặc redesign.

---

## Prompt chính (paste sau Cost + Value output)

```text
Bạn là CFO advisor cho AI products.
Dựa trên BỐI CẢNH ở trên (brief + cost model + value model),
giúp nhóm tôi tính ROI và interpret.

YÊU CẦU:

PHẦN 1 — ROI Ratio:
ROI = Monthly Value / Monthly Cost.

Nhóm tôi có:
- Monthly Cost: $___
- Monthly Value: $___
- ROI = ___:1

Verify công thức: chỉ chia Value / Cost — không phải (Value − Cost) / Cost (đó là margin %).

PHẦN 2 — ROI Interpretation:

| ROI range | Interpretation | Verdict tendency |
|---|---|---|
| > 5:1 | Strong | GO (check overestimate?) |
| 3-5:1 | Solid | GO |
| 1.5-3:1 | Marginal | CONDITIONAL |
| 1-1.5:1 | Weak | CONDITIONAL chặt |
| < 1:1 | Negative | NO-GO |
| > 20:1 | Có thể overestimate | Check assumption |

ROI nhóm tôi rơi vào tier nào? Tier đó cho verdict tendency gì?

PHẦN 3 — Reality Check:

Nhóm tôi tự hỏi:
1. Có overestimate adoption không (> 80%)?
2. Có overestimate quality không (> 85%)?
3. Có dùng Gross thay vì NET time saved không?
4. Có quên cost component nào (human review, setup, monitoring)?
5. Có sai loaded hourly rate (chỉ base salary, quên multiplier)?

Nếu YES bất kỳ câu nào → recalc ROI với assumption realistic hơn → ROI mới là bao nhiêu?

PHẦN 4 — Break-even Analysis:

Tại quality = base, hỏi: adoption bao nhiêu thì ROI = 1:1?

Công thức:
ROI = 1 = Value / Cost
   = (Gross Value × Adoption × Quality) / Cost
=> Adoption = Cost / (Gross Value × Quality)

Tính cho nhóm: ___%

Diễn giải: "Nếu adoption < ___% → pilot fail (Value < Cost)."

Tại adoption = base, hỏi: quality bao nhiêu thì ROI = 1:1?

Tính cho nhóm: ___%

Diễn giải tương tự.

PHẦN 5 — Sensitivity Analysis:

Tạo bảng ROI sensitivity:

| Adoption | Quality 60% | Quality 70% | Quality 80% | Quality 90% |
|---|---|---|---|---|
| 30% | ___:1 | ___:1 | ___:1 | ___:1 |
| 50% | ___:1 | ___:1 | ___:1 | ___:1 |
| 70% | ___:1 | ___:1 | ___:1 | ___:1 |
| 90% | ___:1 | ___:1 | ___:1 | ___:1 |

Identify "sweet spot" — combination adoption + quality cần đạt để ROI > 3:1.

PHẦN 6 — Industry Comparison:
ROI nhóm tôi có hợp lý so với:
- SaaS B2B mature: ROI typically 3-5:1 (đã tính cost full stack).
- AI pilot at small scale: thường 1-3:1 (cost amortize cao).
- AI tại enterprise scale: thường 5-10:1.

Nếu ROI nhóm tôi >> hoặc << industry → flag bất thường.

YÊU CẦU FORMAT:
- Mỗi tính có công thức.
- Mỗi insight có 1-2 câu lý do.
- Trả lời tiếng Việt thoát nghĩa.

YÊU CẦU PHẢN BIỆN:
- ROI có quá đẹp không (overestimate)?
- ROI có quá xấu không (over-conservative)?
- Sensitivity analysis có lộ ra "ngưỡng sống chết" nào không?
```

---

## Iterate — đẩy AI sâu hơn nếu output chưa đủ

### Khi ROI > 20:1 (suspicious đẹp)

```text
ROI nhóm tôi = 25:1 — over the 20:1 threshold.

Likely overestimate. Audit:

1. Adoption check: nhóm đặt > 80%? Justify từ data hay assumption?
2. Quality check: nhóm đặt > 85%? POC data hay benchmark?
3. NET time saved check: > 80% Gross? Đã trừ review + switch + rework?
4. Cost check: quên component nào? Human review luôn là biggest cost.
5. Volume check: monthly volume tính cho PILOT scope hay full team?

Recalc với adjustment:
- Adoption: tối đa 70% (realistic mandatory pilot).
- Quality: tối đa 80% (realistic draft task).
- NET = 50% Gross (typical).
- Include human review cost ($X/task).

ROI sau adjustment: ___:1.

Nếu vẫn > 10:1 sau adjustment → có thể true. Nếu drop xuống 2-5:1 → adjustment đúng, original quá lạc quan.
```

### Khi ROI < 1:1

```text
ROI nhóm tôi = 0.7:1 < 1 → pilot không khả thi ở base case.

Trước khi NO-GO, identify lever để tăng ROI:

LEVER 1: Giảm Cost
- Đổi model (premium → mid → cheap): cost/task giảm 50-80%.
- Bỏ tooling không cần thiết.
- Renegotiate constraint (vd: tier-1 task auto, tier-2+ review).

LEVER 2: Tăng Value
- Mở rộng scope pilot (5 → 15 user → amortize tốt hơn).
- Adoption tăng (training + incentive).
- Quality tăng (prompt engineering, fine-tune).

LEVER 3: Đổi cost model
- Setup không amortize trong pilot 90 ngày, mà spread 1 năm → cost/tháng giảm.
- Renegotiate provider pricing (enterprise tier).

Apply lever, recalc ROI. Sau adjustment:
- Worst case (no adjustment): 0.7:1 NO-GO.
- With LEVER 1 (cheaper model): ___:1.
- With LEVER 2 (broader pilot): ___:1.
- With LEVER 1 + 2: ___:1.

Recommend lever combination khả thi nhất.
```

### Khi muốn sensitivity table

```text
Tạo sensitivity table chi tiết cho brief tôi:

Variables to vary:
- Adoption: 30, 50, 70, 90%
- Quality: 60, 70, 80, 90%
- Cost/task: cost base, × 0.5 (cheaper model), × 2 (provider shock)

Output 3 bảng (1 cho mỗi cost scenario), mỗi bảng 4×4 = 16 cell với ROI.

Identify:
- Cell GO (ROI > 3:1): bao nhiêu cell / 16?
- Cell CONDITIONAL (1-3:1): bao nhiêu?
- Cell NO-GO (<1:1): bao nhiêu?

Từ pattern, suggest:
- "Pilot ổn nếu adoption >= 60% AND quality >= 70% AT cost base."
- "Provider shock 2× → cần adoption + quality cùng >= 80% mới sống."
- "Cheaper model → relaxe yêu cầu, có thể quality 60% vẫn ok."
```

---

## Phản biện sau khi có output — 5 câu nhóm tự hỏi

1. **Công thức check**: ROI = Value / Cost (không phải margin).
2. **Range check**: ROI rơi vào tier nào (>5, 3-5, 1.5-3, 1-1.5, <1, >20)?
3. **Overestimate check**: > 20:1 → audit.
4. **Underestimate check**: < 1:1 → identify lever trước khi NO-GO.
5. **Sensitivity check**: break-even adoption + quality có lộ ngưỡng sống/chết?

---

## Ví dụ tốt vs ví dụ chưa tốt

### Chưa tốt

> "ROI = 8.7:1. Strong. GO."

Vấn đề: không check overestimate, không break-even, không sensitivity, không industry comparison.

### Tốt

> **Brief #1 — ROI Analysis**
>
> **Base ROI**: $5,797 / $2,803 = **2.07:1**.
>
> **Tier**: Marginal (1.5-3:1) → CONDITIONAL tendency.
>
> **Reality check**:
> - Adoption 65% — realistic cho mandatory pilot với UX integrated ✓.
> - Quality 80% — upper bound draft, có thể drop 75% nếu KB outdated → recalc với 75% → ROI = 1.94:1.
> - NET time saved 7.6 min (63% Gross) — slightly upper, justify nhờ inline integration.
> - Cost include human review ($1,320 = 47% cost) — đã include ✓.
> - Loaded rate $25 (base $20 × 1.25) — reasonable.
>
> **Break-even**:
> - Adoption break-even (quality = 80%): adoption = $2,803 / ($11,147 × 80%) = **31.4%**.
> - Quality break-even (adoption = 65%): quality = $2,803 / ($11,147 × 65%) = **38.7%**.
> - Diễn giải: pilot vẫn sống nếu adoption > 32% HOẶC quality > 39%. Buffer rộng từ base.
>
> **Sensitivity** (ROI):
> | Adoption | Quality 60% | Quality 70% | Quality 80% | Quality 90% |
> |---|---|---|---|---|
> | 30% | 0.7:1 | 0.8:1 | 0.96:1 | 1.07:1 |
> | 50% | 1.19:1 | 1.39:1 | 1.59:1 | 1.79:1 |
> | 70% | 1.67:1 | 1.95:1 | 2.23:1 | 2.50:1 |
> | 90% | 2.15:1 | 2.50:1 | 2.86:1 | 3.21:1 |
>
> Sweet spot (ROI > 3:1): cần adoption >= 90% AND quality >= 90%. Khó đạt ở pilot.
> Realistic (ROI > 2:1): adoption >= 70% AND quality >= 80%. Đạt được nếu training tốt.
>
> **Industry comparison**: 2.07:1 ở tier mid-range cho AI pilot small scale. Hợp lý. Mature production thường lên 3-5:1 sau scale.
>
> **Verdict tendency**: CONDITIONAL với điều kiện adoption + quality monitoring.

---

## Anti-pattern khi prompt — tránh

| Đừng làm | Nên làm |
|---|---|
| ROI ratio nhầm thành margin % | ROI = Value / Cost (vd: 2:1, 3.6:1) |
| Chấp nhận ROI > 20:1 mà không audit | Audit assumption, recalc với conservative |
| ROI < 1:1 đi NO-GO ngay | Identify lever 1-3, recalc trước |
| Bỏ sensitivity table | Sensitivity = bằng chứng cho stress test sau |
| Bỏ break-even | Break-even adoption / quality = ngưỡng cứu nét |

---

## Format save vào Section C.6 + C.7

```markdown
### C.6 — ROI
[Paste ROI cụ thể + công thức]

### C.7 — ROI Interpretation
[Paste tier + reality check + comparison]
```

---

## Câu hỏi mở rộng — nâng cao phản biện (optional)

```text
Sau khi tính ROI, suy nghĩ 3 góc STRATEGIC:

1. **Time horizon**: ROI 2:1 tháng đầu — sau 3 tháng / 1 năm / 3 năm như thế nào?
   - Setup amortize hết → cost giảm.
   - Adoption tăng → value tăng.
   - Provider price giảm → cost giảm.
   ROI lifetime: thường > ROI tháng đầu.

2. **Compounding value**:
   - AI learning từ usage data → quality tăng theo thời gian (data flywheel).
   - User skill với AI tăng → adoption tăng + bug giảm.
   - 1 năm sau: ROI có thể × 2 so với base.

3. **Optionality value**:
   - Pilot AI là option mở rộng: nếu success → scale; nếu fail → kill.
   - Cost of NOT trying = opportunity cost (compétiteur làm trước).
   - Even ROI 1.5:1 có thể defend nếu optionality cao.

Trả lời 3 góc này giúp brief có lập luận đầy đủ cho buyer — không chỉ "ROI tháng nào".
```
