# Prompt tham khảo 7 — Build 5 Stress Scenarios

**Dùng khi**: nhóm đã có Cost + Value + ROI base case, cần stress test 5 scenarios (base, heavy, low adopt, quality fail, provider shock) + combined worst.
**Công cụ gợi ý**: Claude Sonnet/Opus, ChatGPT-4o.
**Lưu kết quả vào**: `worksheet/03-stress-test/1-scenario-table.md` + Section D.1, D.2 trong `3-FINAL-stress-test-verdict.md`
**Thời gian**: 20 phút

---

## Trước khi vào prompt — 5 câu hỏi nhóm tự trả lời

1. **Base case**: Cost $___, Value $___, ROI ___:1.
2. **Variables base**: Adoption ___%, Quality ___%, Cost/task $___, Volume ___ tasks/month.
3. **Sensitivity insight** (từ prompt 6): variable nào nhạy nhất với ROI?
4. **Brief field #9 (Risk boundary)**: rủi ro chính trong brief?
5. **Industry shock case**: có ví dụ industry tương tự (Replit margin âm, Salesforce 3× pricing change) không?

> **Cảnh báo**: stress test khác sensitivity. Sensitivity = thay đổi 1 biến nhỏ. Stress = thay đổi 1 biến NHIỀU (2-3×, hoặc 30-50% drop) để mô phỏng "ngày xấu".

---

## Prompt chính (paste sau Cost + Value + ROI output)

```text
Bạn là Risk Manager cho AI products.
Dựa trên BỐI CẢNH ở trên (brief + ROI base case),
giúp nhóm tôi build 5 STRESS SCENARIOS + combined worst case.

YÊU CẦU CHUNG: mỗi scenario thay đổi 1 biến (giữ nguyên 7 biến khác). Combined = 2 scenarios xảy ra đồng thời.

YÊU CẦU CHI TIẾT:

PHẦN 1 — Scenario 1 (Base case — control):
Just confirm số base. No changes.

PHẦN 2 — Scenario 2 (Heavy Usage):
Power user pattern: 20% user dùng 80% capacity.

Define multiplier:
- Multiplier hợp lý cho brief tôi: × ___ (2x / 3x / 5x)
- Lý do: [vd: agent over-rely on AI vì UX dễ; SDR dùng AI nhiều hơn vì save time; user discover usage trick]

Tính lại:
- New monthly volume: ___ × ___ = ___ tasks
- New monthly cost: cost component scale theo volume thế nào?
  - API cost: tuyến tính (volume × cost/task).
  - Tooling: thường flat (vector DB, monitoring).
  - Human review: tuyến tính.
  - Setup: flat (đã amortize).
- New monthly value: tuyến tính với volume (value/task × volume).
- New ROI: New value / New cost.

INSIGHT: Heavy usage test xem cost có BLOW UP nhanh hơn value không.
- Nếu cost tăng linear với volume + value cũng tăng linear → ROI base = ROI heavy. Unit economics OK.
- Nếu cost có "step jump" (vượt enterprise tier, tooling free → paid) → ROI sụp.
- Real example: Replit margins âm vì user 20% dùng AI extreme, cost > revenue.

PHẦN 3 — Scenario 3 (Low Adoption):
Pilot fail adoption.

Define drop:
- New adoption: ___% (vs base ___%)
- Lý do: [vd: UX khó / training thiếu / user resist / no incentive]

Tính lại:
- New monthly value: gross × new adoption × quality
- Monthly cost: GIỮ NGUYÊN (infrastructure fixed, không scale down dễ)
- New ROI: New value / cost

INSIGHT: Low adoption thường hurt nhiều nhất vì:
- Cost fixed (tooling subscription, setup amortize) — không giảm khi user không dùng.
- Value giảm trực tiếp với % adoption.
- Pilot fail → có thể NO-GO ở tier này.

PHẦN 4 — Scenario 4 (Quality Failure):
AI output kém hơn dự đoán.

Define drop:
- New quality: ___% (vs base ___%)
- Lý do: [vd: edge case nhiều / KB outdated / model thiếu domain / fine-tune chưa kịp]

Tính lại:
- Rework cost tăng: + $___ /month (extra time fix bad outputs)
- New monthly value: gross × adoption × new quality − rework
- New monthly cost: có thể tăng nhẹ (retry / regen attempts)
- New ROI: ?

PHẦN 5 — Scenario 5 (Provider Shock):
Provider đổi giá hoặc deprecate model.

Define shock:
- Multiplier: × ___ (2x / 3x)
- Lý do: [vd: Anthropic deprecate Claude 3.5 → buộc Claude 4 đắt 60%; Salesforce đổi pricing AI 3 lần / 18 tháng]

Tính lại:
- New API cost: old API × multiplier
- Tooling, review, setup: giữ nguyên
- New monthly cost: ?
- Monthly value: giữ nguyên (cost tăng không làm value đổi ngay)
- New ROI: ?

INSIGHT: Provider shock test xem economics có "rented land" risk không.
- Nếu API cost là % nhỏ (vd: <10%) → shock 2× chỉ tăng cost <10%. Robust.
- Nếu API cost dominate (vd: >50%) → shock 2× làm cost gần 1.5×. Risky.

PHẦN 6 — Combined Worst Case:
Chọn 2 scenarios xấu nhất từ 4 (2-5).

Apply 2 thay đổi đồng thời:
- Change 1: ___
- Change 2: ___

Tính:
- Combined cost: áp cả 2 thay đổi lên cost
- Combined value: áp cả 2 thay đổi lên value
- Combined ROI: ___:1

Interpretation:
| Combined ROI | Verdict tendency |
|---|---|
| > 3:1 | Robust |
| 1.5-3:1 | Survivable |
| 1-1.5:1 | Break-even, cần mitigation |
| 0.5-1:1 | Risky, redesign |
| < 0.5:1 | Critical, NO-GO |

YÊU CẦU FORMAT:
- Mỗi scenario có cost + value + ROI cụ thể.
- Mỗi scenario có lý do shock (không "random shock").
- Trả lời tiếng Việt thoát nghĩa.

YÊU CẦU PHẢN BIỆN:
- Multiplier có realistic không (2-3× phổ biến, > 5× hiếm)?
- Combined worst có 2 scenarios chọn lý do gì?
- Có scenario nào ROI mạnh hơn base (counter-intuitive)?
```

---

## Iterate — đẩy AI sâu hơn nếu output chưa đủ

### Khi tất cả scenarios đều > 3:1 (không có hurt)

```text
5 scenarios của tôi đều có ROI > 3:1 — có vẻ economics quá robust.

Verify:
1. Heavy usage × 3 mà ROI vẫn > 3? Check cost có scale linear không (có thể step jump bị miss).
2. Low adoption 30% mà ROI vẫn > 3? Check cost có fixed component không (setup, tooling).
3. Quality 50% mà ROI vẫn > 3? Check rework cost (typical 0.5-2 min × miss rate).
4. Provider × 2 mà ROI vẫn > 3? Check API cost share trong total cost.

Nếu sau verify vẫn robust → base case ROI quá đẹp (>10:1). Recheck base.

Hoặc thử shock cứng hơn:
- Heavy × 5 (extreme power user).
- Adoption 20% (pilot failure mode).
- Quality 40% (model collapse).
- Provider × 4 (full deprecation + replacement).

Combined worst case ở những extreme này — vẫn > 1:1 không?
```

### Khi có scenario lý do mơ hồ

```text
Scenario 4 (Quality failure) bạn đề xuất quality = 60% — vì sao 60% specifically?

Cần lý do CỤ THỂ:
- KB outdated 30% → drafts dựa KB sai 30%? → quality drop 60-65%.
- Domain narrow (specialized legal) → model general không cover edge case → quality 50-65%.
- Fine-tune chưa hoàn thiện trong pilot 90 ngày → quality 60-70% (chưa stable).
- POC data chỉ 75% → pessimistic = drop 10pt → 65%.

Pick 1 lý do realistic. Quality drop bao nhiêu phụ thuộc lý do:
- Cause 1 (KB): drop nhỏ vì RAG có thể partial work.
- Cause 2 (domain): drop trung bình, narrow domain.
- Cause 3 (fine-tune): drop lớn, pilot không có fine-tune.

Recommend: pick cause realistic nhất cho brief tôi + define quality drop tương ứng.
```

### Khi muốn xem real-world stress

```text
Tìm 2 real-world example AI product gặp stress tương tự:

1. **Heavy usage failure**:
   - Replit Ghostwriter: margin âm trong 2 tháng vì 20% user dùng 80% AI capacity.
   - Insight: cost/user vượt revenue/user → pricing redesign (add credits cap).

2. **Provider shock**:
   - Microsoft Copilot M365: Anthropic deprecate Claude 2 → buộc upgrade Claude 3 (đắt hơn 40%).
   - Salesforce Einstein: đổi pricing AI 3 lần trong 18 tháng (2024).
   - Insight: lock contract 1 năm hoặc đa provider.

3. **Quality failure**:
   - Air Canada chatbot: AI bịa policy → kiện $812. Quality drop 1 case nhưng cost legal lớn.
   - Insight: quality failure có thể có "tail risk" — 1 vụ lớn > tổng saving.

Map vào brief tôi: scenario nào giống real example nhất → boost realism.
```

---

## Phản biện sau khi có output — 5 câu nhóm tự hỏi

1. **Scenario coverage**: đủ 5 scenarios + combined?
2. **Multiplier realistic**: 2-3× cho phần lớn, không > 5×?
3. **Lý do specific**: mỗi shock có lý do brief-specific?
4. **Combined chọn đúng 2 xấu nhất**: không tùy ý?
5. **Insight per scenario**: rút ra "scenario nào hurt nhất, tại sao"?

---

## Ví dụ tốt vs ví dụ chưa tốt

### Chưa tốt

> "Scenario 2 (heavy): volume × 2, ROI giảm 50%."

Vấn đề: không có cost/value mới, không lý do, không insight.

### Tốt

> **Brief #1 — Stress Scenarios**
>
> **Base case** (control):
> - Cost $2,803, Value $5,797, ROI **2.07:1**.
>
> **Scenario 2 — Heavy Usage**:
> - Change: Volume × 2 (3,520 → 7,040 task/month). Lý do: 20% agent power-use AI cho mọi ticket (kể cả simple).
> - New cost: API $30→$60 + tooling $120 + human review $1,320→$2,640 + setup $1,333 = **$4,153**.
> - New value: Gross $11,147→$22,294 × 65% × 80% = **$11,593**.
> - **New ROI: $11,593 / $4,153 = 2.79:1** ✓.
> - Insight: cost + value cùng scale linear với volume → ROI base ≈ ROI heavy. Unit economics OK.
>
> **Scenario 3 — Low Adoption**:
> - Change: Adoption 65% → 30%. Lý do: agent senior chưa quen UX, lười click "Draft AI".
> - Cost: GIỮ NGUYÊN $2,803 (infrastructure fixed).
> - New value: $11,147 × 30% × 80% = **$2,675**.
> - **New ROI: $2,675 / $2,803 = 0.95:1** ✗ Negative.
> - Insight: low adoption hurt nhất. Cost fixed nhưng value collapse theo % adoption.
>
> **Scenario 4 — Quality Failure**:
> - Change: Quality 80% → 50%. Lý do: KB outdated 30% + edge case mới (new product launch).
> - Rework: + 1.5 min/task = + $___ /month.
> - New value: $11,147 × 65% × 50% − rework = **$3,323**.
> - Cost: $2,803.
> - **New ROI: $3,323 / $2,803 = 1.19:1** Marginal.
> - Insight: quality fail vẫn break-even nhờ adoption ok.
>
> **Scenario 5 — Provider Shock**:
> - Change: API cost × 3 ($0.0084 → $0.025/task). Lý do: Anthropic deprecate Claude 3.5 Q1 2027, buộc upgrade Claude 4 với pricing × 3.
> - New API: $30 → $90.
> - New cost: $90 + $120 + $1,320 + $1,333 = **$2,863**.
> - Value: $5,797.
> - **New ROI: $5,797 / $2,863 = 2.02:1** ✓ Robust.
> - Insight: API cost chỉ 3% of total cost — shock 3× không hurt nhiều. Human review dominate cost.
>
> **Combined Worst** (Scenario 3 + Scenario 4: Low Adoption + Quality Fail):
> - Adoption 30%, Quality 50%.
> - Cost: $2,803 (fixed).
> - Value: $11,147 × 30% × 50% − rework = **$1,672**.
> - **Combined ROI: $1,672 / $2,803 = 0.60:1** ✗ Risky.
> - Interpretation: pilot KHÔNG sống nếu cả adoption + quality cùng fail. Cần mitigation cho cả 2.
>
> **Pattern**: low adoption + quality fail là combo nguy hiểm nhất. Cost insensitive đến API/heavy. Human review dominate.

---

## Anti-pattern khi prompt — tránh

| Đừng làm | Nên làm |
|---|---|
| Scenario không có lý do | Mỗi shock có lý do brief-specific |
| Multiplier × 1.1 (quá nhẹ) | Stress = 2-3× hoặc 30-50% drop |
| Combined = 1 scenario thôi | Combined = 2 scenarios đồng thời |
| Quên rework cost trong Quality fail | Rework cost tăng đáng kể |
| Cost giảm khi adoption thấp | Cost fixed phần lớn (subscription, setup) |
| Real-world example không có | Match với Replit / Salesforce / Air Canada |

---

## Format save vào `1-scenario-table.md` và Section D.1, D.2

```markdown
## Phần B — 5 Scenarios Table
[Paste scenario 1-5 với cost + value + ROI mới]

## Phần C — Combined Worst Case
[Paste]
```

---

## Câu hỏi mở rộng — nâng cao phản biện (optional)

```text
Sau khi stress test, giúp tôi suy nghĩ 3 angle:

1. **Recovery scenario**: nếu Combined Worst xảy ra, mất bao lâu để recovery?
   - Adoption phục hồi: 3-6 tháng training intensive.
   - Quality phục hồi: 1-2 tháng prompt iteration + KB update.
   - Cost phục hồi: phụ thuộc provider, 0-12 tháng.

2. **Mitigation cost**:
   - Lock provider contract 1 năm: cost premium 10-20%?
   - Backup model setup: setup cost $5-10K thêm.
   - Adoption training program: $X budget per quarter.
   - Mitigation cost có defendable so với risk avoided?

3. **Cascading failure**:
   - Low adoption → low data feedback → quality không cải thiện → adoption càng giảm.
   - Có cascading risk nào trong brief tôi không?
   - Stop trigger: monitor variable nào để break cascading sớm?

3 câu này chuẩn bị cho verdict CONDITIONAL với conditions chặt — buyer sẽ hỏi.
```
