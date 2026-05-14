---
artifact: 2 — Pricing Model Choice + Value Metric
buoc: 2 — Pricing/Access + Value/ROI
phase: Chốt pricing model + value metric
time: 10 phút (xem deck slide 4 để biết khung giờ chính xác trong buổi)
input: 1-attribution-autonomy.md + prompts/04-pricing-model-choice.md
nop-cuoi: Không — file trung gian
---

# 2 — Pricing Model Choice + Value Metric

Mục tiêu: chốt pricing model cụ thể cho brief, định nghĩa value metric (khách trả tiền cho cái gì), kiểm tra Usage Anxiety risk.

Quy tắc: pricing model phải pass 3 test — countable, meaningful to buyer, tied to AI value.

## Quy trình 10 phút

```text
3 phút  — Chọn pricing model (từ ma trận trong file 1)
4 phút  — Định nghĩa value metric + 3-part test
3 phút  — Check Usage Anxiety + mitigation
```

---

## Phần A — Pricing Model Choice

### Pricing model options

Có 4 nhóm chính:

| Model | Mô tả | Khi nào dùng | Ví dụ thật |
|---|---|---|---|
| **Seat / Flat** | $X/user/tháng cố định | Low Auto + Low Attrib | Grammarly $12/seat, Slack AI $7/seat |
| **Usage-based** | $X / unit volume | High Auto + Low Attrib | OpenAI API $0.50/1M tokens, AWS pay-per-call |
| **Outcome-based** | $X / outcome thực tế | High Auto + High Attrib | Intercom Fin $0.99/resolution, Chargeflow per dispute won |
| **Hybrid** | Seat base + Usage credits (hoặc Tier outcome) | Mix (medium autonomy + attribution) | Cursor $20 + credits, Clay $149/$349/$800 tier |

### Pricing model nhóm CHỌN

**Pricing model**: ___

**Giá đề xuất** (đơn vị): $___

- Vd: "$25/seat/month, bundle 1,000 credit/seat"
- Vd: "$1.50/resolution"
- Vd: "$15/seat + $0.02/extra task"

**Lý do chọn** (so với 3 model khác):

- [1-3 câu]

---

## Phần B — Value Metric

Value metric = đơn vị khách hàng trả tiền cho.

**Value metric của nhóm**: ___

### 3-part test cho value metric

| Test | Có pass không? | Bằng chứng |
|---|---|---|
| **Countable** — khách đo được unit này | [Có / Không] | [vd: "Resolution count" đếm được từ logs] |
| **Meaningful to buyer** — buyer hiểu unit này quan trọng | [Có / Không] | [vd: "Resolution" là KPI của support team] |
| **Tied to AI value** — giá trị AI tạo ra link trực tiếp với unit này | [Có / Không] | [vd: "AI resolve = AI tạo giá trị, không phải team"] |

Cả 3 = Có → value metric hợp lệ.

### Common mistakes

- **Value metric quá technical**: "API call" — buyer không quan tâm, họ quan tâm "ticket resolved" hoặc "lead contacted".
- **Value metric không countable**: "Quality improvement" — không có unit, không thể bill.
- **Value metric không tied to AI**: "Số agent trong team" → nhưng AI không phải nguyên nhân team to/nhỏ.

---

## Phần C — Buyer + Buying Trigger

### Buyer

**Ai là người quyết định mua AI product này?**

- Buyer role: [vd: CTO / Director Support / VP T&S / Managing Partner / Director Supply Chain]
- Brief field #6 (Decision needed) cho biết ai hỏi → đó là buyer của nhóm.
- Buyer cụ thể từ brief: ___

### Buying trigger

**Vì sao buyer quyết định mua HÔM NAY (không phải năm sau)?**

- Pain point từ brief: [field #3]
- Mức độ urgent: [Bắt buộc / Nên có / Sẽ tốt nếu có]
- Alternative buyer đang cân nhắc: [hire thêm người / outsource / chấp nhận pain]

### Pricing có align với buyer?

Pricing model nhóm chọn → buyer có dễ approve không?

- Seat-based → dễ predict cost → CFO thường thích.
- Usage-based → cost bị biến động → CFO cần cap.
- Outcome-based → ROI dễ defend → executive thường thích.
- Hybrid → phức tạp hơn để bán → cần sale education.

**Pricing alignment với buyer**: [Tốt / Trung bình / Yếu]

**Lý do**: [...]

---

## Phần D — Usage Anxiety Check

Khi pricing có yếu tố Usage hoặc Outcome → khách có thể sợ dùng nhiều vì sợ bill tăng.

### Usage Anxiety là gì?

User self-limit usage vì sợ cost → AI không được dùng thật → không tạo giá trị → ROI thực tế thấp hơn ROI tính toán.

Ví dụ: Cursor có credit system, user gặp dialog "credit thấp → upgrade?" → user ngại dùng → AI value bị suppress.

### Brief của nhóm có Usage Anxiety risk không?

| Risk | Đánh giá |
|---|---|
| Pricing có usage element? | [Có / Không] |
| User cuối có thấy cost mỗi lần dùng? | [Có / Không] |
| User có khả năng kiểm soát limit? | [Có / Không] |
| Có alternative miễn phí mà user có thể switch? | [Có / Không] |

**Usage Anxiety level**: [Low / Medium / High]

**Mitigation đề xuất** (nếu Medium / High):

- Option 1: [vd: Cap monthly usage và include trong tier — như Cursor]
- Option 2: [vd: Hide individual cost — chỉ show "credit balance"]
- Option 3: [vd: Free exploration tier (10 free tasks/month) → reduce friction]

---

## Phần E — Bảng tổng hợp Section B

Pre-fill các trường để paste vào FINAL:

| Field | Giá trị |
|---|---|
| Autonomy | [Low / High] |
| Attribution | [Low / High] |
| Quadrant | ___ |
| Pricing model | ___ |
| Giá đề xuất | $___ (đơn vị) |
| Value metric | ___ |
| Buyer | ___ |
| Real-world analog | ___ |
| Usage Anxiety risk | [Low / Medium / High] |
| Mitigation | [...] |

---

## Phần F — Kiểm tra

Trước khi chuyển sang `3-FINAL-pricing-value-roi.md`, rà soát:

- [ ] Pricing model rõ ràng (1 trong 4 nhóm) + giá cụ thể.
- [ ] Value metric pass 3-part test.
- [ ] Buyer cụ thể (role + tên from brief).
- [ ] Real-world analog đã chọn (1 sản phẩm thật cùng pricing).
- [ ] Usage Anxiety đánh giá Low/Med/High với mitigation nếu cần.

---

## Anti-pattern

| Đừng làm | Nên làm |
|---|---|
| "Pricing tùy theo demand" | Chọn 1 model cụ thể + giá đề xuất |
| Value metric = "AI usage" | Cụ thể: "1 ticket resolved", "1 contract reviewed" |
| Quên buyer | Mọi pricing có buyer cụ thể (từ brief field #6) |
| Pricing không link với cost ở Section A | Giá đề xuất phải > cost/unit + margin |
| Bỏ Usage Anxiety | Mọi pricing có usage element đều cần check anxiety |

---

## Next: tính Monthly Value + ROI

Sau khi chốt pricing model, chuyển sang `3-FINAL-pricing-value-roi.md` để tính giá trị tháng và ROI. ROI = Value / Cost.
