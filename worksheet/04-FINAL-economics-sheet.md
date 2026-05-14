---
artifact: 04 — FINAL Economics Sheet (master file)
buoc: Tất cả 3 bước Lab
phase: Gộp 4 sections, nộp LMS
time: 5 phút gộp (xem deck slide 4 để biết khung giờ chính xác trong buổi)
input: 01-cost-model/3-FINAL + 02-pricing-value/3-FINAL + 03-stress-test/3-FINAL
nop-cuoi: Có — file MASTER nộp lên LMS Day 27
---

# 04 — FINAL Economics Sheet — Master File

Đây là **deliverable cuối cùng** của Day 27 Lab. Người chấm sẽ xem file này TRƯỚC tất cả các file khác.

> **Tham chiếu mẫu**: xem `00-worked-example.md` — bản Economics Sheet đã điền hoàn chỉnh cho Brief #1 (AI Support Copilot). Đọc trước khi gộp để biết mức chi tiết và format cuối.

Cấu trúc 4 Sections theo đúng thứ tự:

```text
Section A — Cost Model         (từ 01-cost-model/3-FINAL-cost-model.md)
Section B — Pricing / Access   (từ 02-pricing-value/3-FINAL-pricing-value-roi.md, phần B)
Section C — Value / ROI        (từ 02-pricing-value/3-FINAL-pricing-value-roi.md, phần C)
Section D — Stress Test + Verdict  (từ 03-stress-test/3-FINAL-stress-test-verdict.md)
```

**Cách sử dụng**: copy nội dung Section A, B, C, D từ các file intermediate vào đây. Không sửa, không bịa thêm.

---

## Thông tin nhóm

- **Brief**: # ___ — [tên brief]
- **Cặp**: [tên + mã học viên × 2]
- **Ngày tính**: [YYYY-MM-DD]
- **Phiên bản**: v1

---

## Tóm tắt 1 câu cho buyer (Executive summary)

Viết 1-2 câu tổng kết cho buyer trong brief field #6 đọc nhanh:

> "[Verdict: GO / CONDITIONAL / NO-GO] cho [Brief # ___]. Base ROI ___:1, combined worst case ___:1. [1 câu key condition hoặc change]."

Ví dụ:

> "CONDITIONAL GO cho Brief #1 AI Support Copilot. Base ROI 2.07:1, combined worst case (Low adoption + Provider shock) 1.20:1 — biên mỏng. Pilot tiếp tục với 3 điều kiện: adoption ≥ 50% trước cuối tháng 1, khoá giá API 6 tháng, cổng chi phí $3,000/tháng."

**Tóm tắt nhóm**:

[...]

---

## Section A — Cost Model

> Copy từ `01-cost-model/3-FINAL-cost-model.md`. Bao gồm các sub-section A.1 (Usage Unit) → A.8 (Budget Check).

### A.1 — Usage Unit

[paste nội dung]

### A.2 — Volume

[paste]

### A.3 — Model + API Cost

[paste]

### A.4 — Tooling Cost

[paste]

### A.5 — Human Review Cost

[paste]

### A.6 — Setup Cost (amortize)

[paste]

### A.7 — Monthly Cost Formula

[paste công thức + tính cụ thể]

### A.8 — Budget Check

[paste]

---

## Section B — Pricing / Access Model

> Copy từ `02-pricing-value/3-FINAL-pricing-value-roi.md`, phần Section B.

### B.1 — Attribution × Autonomy positioning

[paste]

### B.2 — Pricing Model

[paste]

### B.3 — Real-world analog

[paste]

### B.4 — Usage Anxiety check

[paste]

---

## Section C — Value / ROI

> Copy từ `02-pricing-value/3-FINAL-pricing-value-roi.md`, phần Section C.

### C.1 — Time Saved per Task

[paste bảng NET time saved]

### C.2 — Loaded Hourly Rate

[paste]

### C.3 — Adoption + Quality

[paste với justification]

### C.4 — Monthly Volume

[paste]

### C.5 — Monthly Value Formula

[paste công thức + tính cụ thể]

### C.6 — ROI

[paste ROI số cụ thể]

### C.7 — ROI Interpretation

[paste]

---

## Section D — Stress Test + Verdict

> Copy từ `03-stress-test/3-FINAL-stress-test-verdict.md`.

### D.1 — Stress Test Table

[paste bảng 5 scenarios]

### D.2 — Combined Worst Case

[paste]

### D.3 — Break-even Analysis

[paste]

### D.4 — Verdict

**Verdict**: ☐ GO  ☐ CONDITIONAL  ☐ NO-GO

[paste verdict statement]

### D.5 — Conditions / Changes

[paste]

### D.6 — Monitoring Metrics

[paste]

### D.7 — Stop / Pivot Trigger

[paste]

### D.8 — Changes Needed (nếu NO-GO)

[paste]

---

## Cross-section insights

3 insight tổng hợp từ cả 4 sections (gộp các insight ở từng section):

1. **Cost structure insight**: [vd: "Human review chiếm 89% cost — đây là pattern phổ biến với pilot có constraint 100% review"]
2. **Value insight**: [vd: "Adoption là biến nhạy nhất — adoption 50% → ROI giảm 30%, cần đầu tư training"]
3. **Verdict insight**: [vd: "Combined worst case break-even chính xác ở mức adoption 60% — đó là threshold cốt lõi cần monitor"]

---

## Comparison với brief D26 (nếu có)

Day 27 economics có khớp với strategic analysis ở Day 26 không?

- Lens 1 (Customer Expectation) ở D26 → Value metric ở D27: [Có match / Lệch chỗ nào]
- Lens 4 (Defensibility) ở D26 → Provider risk ở D27 scenario 5: [Match / Lệch]
- Cost structure phù hợp với "Cost-Capability-Speed Triangle" trong D26?

---

## Comparison với cặp khác brief (nếu có thời gian)

So sánh kết quả với 1-2 cặp khác brief (thường làm sau buổi):

| Brief | Cost/month | Value/month | ROI | Verdict |
|---|---|---|---|---|
| Brief # ___ (nhóm chúng tôi) | $___ | $___ | ___:1 | ___ |
| Brief # ___ (cặp khác) | $___ | $___ | ___:1 | ___ |
| Brief # ___ (cặp khác) | $___ | $___ | ___:1 | ___ |

**Pattern across briefs**:

- [vd: "Brief có constraint 100% review (1, 2, 3, 4) đều có cost dominated bởi human review, không phải API"]
- [vd: "Brief có high attribution (4, 7, 9) dễ đi sang outcome-based pricing"]
- [vd: "Brief có low volume (3, 4) cần model expensive (high cost/task) — ROI nhạy hơn với quality"]

---

## Checklist Master File nộp LMS

- [ ] Executive summary 1-2 câu paste được copy.
- [ ] Section A đủ 8 sub-sections (A.1 → A.8).
- [ ] Section B đủ 4 sub-sections (B.1 → B.4).
- [ ] Section C đủ 7 sub-sections (C.1 → C.7).
- [ ] Section D đủ 8 sub-sections (D.1 → D.8).
- [ ] Đã chọn 1 trong 3 verdicts.
- [ ] Nếu CONDITIONAL: có ≥ 3 điều kiện.
- [ ] Nếu NO-GO: có ≥ 2 changes.
- [ ] Có 3 cross-section insights.
- [ ] Comparison D26 đã ghi (nếu nhóm có brief overlap).

---

## Cách render bảng cho slide trình bày 6 phút

Khi trình bày, nhóm trích từ Master File theo cấu trúc:

```text
Slide 1 (30s) — Brief + usage unit
Slide 2 (30s) — Cost model: $___ /month (breakdown 4 component)
Slide 3 (30s) — Value/ROI: $___ value, ___ ROI
Slide 4 (30s) — Worst scenario: ___ → ROI ___
Slide 5 (1m) — Verdict + conditions
Slide 6 (3.5m) — Q&A
```

Lưu ý: deliverable nộp LMS = file Master này. Slide trình bày là tóm tắt — tạo riêng (PDF / Google Slides / Keynote), không trong worksheet.

---

## Nộp lên LMS

1. Đảm bảo file `04-FINAL-economics-sheet.md` này có đầy đủ 4 Sections.
2. Đảm bảo các file trung gian (`01-`, `02-`, `03-`) cũng đã được commit vào repo `Day27-MãNhóm`.
3. README đầu repo có link tới file FINAL này.
4. Push repo lên GitHub (công khai).
5. Nộp link repo lên LMS Day 27 trước **23:59 hôm nay**.

Một thành viên đại diện nộp link — không trùng lặp.
