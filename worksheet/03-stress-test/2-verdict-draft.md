---
artifact: 2 — Verdict Draft
buoc: 3 — Stress Test + Verdict
phase: Viết verdict draft + conditions
time: 10 phút (xem deck slide 4 để biết khung giờ chính xác trong buổi)
input: 1-scenario-table.md + prompts/08-verdict-writing.md
nop-cuoi: Không — file trung gian
---

# 2 — Verdict Draft

Mục tiêu: viết verdict draft (GO / CONDITIONAL / NO-GO) dựa trên 5 scenarios + combined worst case + break-even analysis.

Quy tắc:

- Verdict phải có lý do cụ thể (không chỉ "feeling").
- CONDITIONAL phải có 3-5 điều kiện rõ ràng + monitoring metrics + stop trigger.
- NO-GO phải nói rõ "cần thay đổi gì để khả thi" — không từ chối khô khan.

## Quy trình 10 phút

```text
3 phút  — Apply criteria → pick verdict
4 phút  — Viết draft verdict + conditions / change
3 phút  — Reality check (cặp tự challenge verdict mình)
```

---

## Phần A — Verdict Decision Framework

### Criteria mapping

| Criteria | GO | CONDITIONAL | NO-GO |
|---|---|---|---|
| Base ROI | > 3:1 | 1.5-3:1 | < 1.5:1 |
| Survives ___ /5 individual scenarios | 4-5 | 2-3 | 0-1 |
| Combined worst case ROI | > 1.5:1 | 1-1.5:1 | < 1:1 |

### Apply criteria cho nhóm

| Criteria | Giá trị nhóm | Quadrant |
|---|---|---|
| Base ROI | ___ : 1 | [GO / CONDITIONAL / NO-GO] |
| Survives X/5 scenarios | ___ / 5 | [GO / CONDITIONAL / NO-GO] |
| Combined worst case | ___ : 1 | [GO / CONDITIONAL / NO-GO] |

**Verdict tổng hợp**: ___

Nếu 3 row chỉ vào 1 verdict đồng nhất → verdict rõ ràng.

Nếu lệch (vd: base GO, combined NO-GO) → thường nghiêng về **CONDITIONAL** với điều kiện chặt.

---

## Phần B — Draft Verdict Statement

### Nếu GO

**Verdict draft**:

> "Proceed with pilot as scoped. Brief # ___ — [tên]. Pilot scope: ___ user × ___ ngày, budget $___."
>
> "Base ROI là ___ : 1. Sống được cả khi: [list 4-5 scenarios sống]. Combined worst case [scenarios xấu nhất] cho ROI ___ : 1, vẫn trên ngưỡng 1.5:1."

### Nếu CONDITIONAL (phổ biến nhất)

**Verdict draft**:

> "CONDITIONAL GO. Brief # ___ — [tên]. Tiến hành pilot **với các điều kiện**:"
>
> Điều kiện 1: [vd: Adoption phải đạt ≥ ___% trong tháng 1, nếu không → pause review]
>
> Điều kiện 2: [vd: Lock API pricing với provider trong 6 tháng pilot, hoặc setup fallback model]
>
> Điều kiện 3: [vd: Monthly cost review gate ở $___, không vượt budget pilot]
>
> Điều kiện 4: [vd: Quality factor đo theo random sampling 50 tasks/tuần, target ≥ ___%]
>
> "Monitoring metrics tracked weekly: adoption rate, cost/task, quality factor."
>
> "Stop/pivot trigger: nếu trong 30 ngày liên tiếp adoption < ___% HOẶC quality < ___% HOẶC cost-per-task > $___ → pause và re-evaluate."

### Nếu NO-GO

**Verdict draft**:

> "NO-GO at current scope. Brief # ___ — [tên]."
>
> "Base ROI ___ : 1 < 1, hoặc combined worst case ___ : 1 < 0.5."
>
> "Cần thay đổi để khả thi:"
>
> Change 1: [vd: Đổi cost model — dùng GPT-4o-mini thay vì Claude 3.5 Sonnet → cost/task giảm 80%]
>
> Change 2: [vd: Mở rộng scope pilot từ 5 lên 15 agent → cost amortize tốt hơn]
>
> Change 3: [vd: Loại bỏ constraint 100% review cho task đơn giản → giảm human review cost]
>
> "Loại NO-GO: [Not now — có thể quay lại khi A, B / Not ever — fundamentally không phù hợp]"

---

## Phần C — Verdict của nhóm

**Verdict CHỌN**: [GO / CONDITIONAL / NO-GO]

**Tóm tắt verdict trong 3-4 câu** (paste này vào FINAL):

[...]

[...]

[...]

[...]

### Conditions / Changes (chi tiết)

Nếu CONDITIONAL — viết 3-5 conditions:

1. **Điều kiện 1**: [Cụ thể, đo được, có timeline]
2. **Điều kiện 2**: [Cụ thể, đo được, có timeline]
3. **Điều kiện 3**: [Cụ thể, đo được, có timeline]
4. **Điều kiện 4** (nếu cần): [...]
5. **Điều kiện 5** (nếu cần): [...]

### Monitoring metrics

Liệt kê 3-5 metrics nhóm sẽ track hàng tuần:

- Metric 1: [vd: Adoption rate (= users active that week / pilot total)]
- Metric 2: [vd: Cost per task ($)]
- Metric 3: [vd: Quality factor (random 50 tasks sample / week)]
- Metric 4: [vd: User satisfaction (CSAT survey monthly)]

### Stop/pivot trigger

Trigger cụ thể: "Nếu trong [thời gian], [metric] vượt ngưỡng [số], thì [action]."

- Trigger 1: [...]
- Trigger 2: [...]

---

## Phần D — Reality Check (challenge verdict của chính mình)

Trước khi finalize, cặp tự challenge:

### Câu hỏi 1: Tại sao không CONDITIONAL nếu chọn GO?

Hầu hết AI pilot thực tế nên CONDITIONAL. Nếu nhóm chọn GO:

- Có data hard nào support adoption > 80% không?
- Có data hard nào support quality > 85% không?
- Combined worst case có thực sự > 1.5:1 không, hoặc nhóm đang lạc quan?

Nếu không có data cứng → consider CONDITIONAL.

### Câu hỏi 2: Tại sao không NO-GO nếu chọn CONDITIONAL?

Một CONDITIONAL với điều kiện không khả thi cũng = NO-GO trá hình:

- Điều kiện 1 có thực sự đạt được không?
- Adoption phải > 80% mới sống → khó đạt → thực tế là NO-GO.
- Cost phải giảm 50% mới sống → khó negotiate → thực tế là NO-GO.

Nếu CONDITIONAL phụ thuộc vào điều kiện không khả thi → CONDITIONAL biến thành NO-GO. Honest hơn nói NO-GO ngay.

### Câu hỏi 3: Buyer (CTO/VP) sẽ phản ứng thế nào?

Đặt mình vào vai buyer trong brief field #6:

- Buyer thấy GO chắc chắn không có stress test → có tin được không?
- Buyer thấy CONDITIONAL có 3 điều kiện cụ thể → có actionable không?
- Buyer thấy NO-GO có lý do rõ → có giúp tiết kiệm cost không?

Buyer tốt **thích CONDITIONAL với điều kiện rõ** hơn là **GO chắc chắn không stress test**.

---

## Phần E — Kiểm tra Verdict Draft

Trước khi chuyển sang `3-FINAL-stress-test-verdict.md`, rà soát:

- [ ] Verdict CHỌN rõ ràng (GO / CONDITIONAL / NO-GO).
- [ ] Verdict statement 3-4 câu paste được vào FINAL.
- [ ] Nếu CONDITIONAL: có 3-5 điều kiện cụ thể, đo được, có timeline.
- [ ] Có monitoring metrics list 3-5 items.
- [ ] Có stop/pivot trigger cụ thể (số + thời gian + action).
- [ ] Đã reality check tại sao không CONDITIONAL (nếu GO) hoặc tại sao không NO-GO (nếu CONDITIONAL).
- [ ] Đã đặt mình vào vai buyer để kiểm tra verdict có defendable không.

---

## Anti-pattern

| Đừng làm | Nên làm |
|---|---|
| Verdict = "Có vẻ ok" | Cụ thể GO/CONDITIONAL/NO-GO với criteria |
| GO chắc chắn (không stress test) | CONDITIONAL với điều kiện rõ — defendable hơn |
| CONDITIONAL không có điều kiện cụ thể | 3-5 điều kiện đo được + timeline |
| CONDITIONAL với điều kiện không khả thi | Honest hơn nói NO-GO |
| NO-GO không nói "cần đổi gì" | Liệt kê 2-3 changes để khả thi |
| Quên buyer perspective | Đặt mình vào vai buyer, defendable? |

---

## Next: FINAL Section D

Sau khi có verdict draft, chuyển sang `3-FINAL-stress-test-verdict.md` để gộp Section D (Stress Test + Verdict) hoàn chỉnh.
