---
artifact: 3 — FINAL Cost Model (Section A của Economics Sheet)
buoc: 1 — Cost Model
phase: Chốt Section A
time: 10 phút (xem deck slide 4 để biết khung giờ chính xác trong buổi)
input: 1-usage-unit.md + 2-cost-research.md
nop-cuoi: Có — section A nộp trong 04-FINAL-economics-sheet.md
---

# 3 — FINAL Cost Model — Section A của Economics Sheet

Đây là file cuối của Step 1 Lab. Người chấm sẽ xem section này cùng với 3 section còn lại trong `04-FINAL-economics-sheet.md`.

Mục tiêu: chốt Section A của Economics Sheet với 10-15 trường rõ ràng + công thức tính monthly cost.

Quy tắc khi viết:

- Mỗi số phải có công thức / nguồn / lý do.
- Không dùng "khoảng", "tầm", "đại loại" — phải số cụ thể.
- Tham chiếu `1-usage-unit.md` và `2-cost-research.md` cho công thức chi tiết.

---

## Thông tin nhóm

- **Brief**: # ___ — [tên brief]
- **Cặp**: [tên + mã học viên × 2]
- **Ngày tính**: [YYYY-MM-DD]
- **Phiên bản**: v1

---

## Section A — Cost Model

### A.1 — Usage Unit

| Trường | Giá trị |
|---|---|
| Usage unit (tên ngắn) | [vd: "1 ticket reply draft"] |
| Mô tả (1-2 câu) | [...] |
| 3-part test pass | ☐ Đếm được ☐ Tốn token ☐ Có giá trị |

### A.2 — Volume

| Trường | Giá trị | Công thức / Nguồn |
|---|---|---|
| Pilot users | ___ | Brief field #8 |
| Total team | ___ | Brief field #1 |
| Team daily volume | ___ /day | Brief field #1 |
| Pilot daily volume | ___ /day | (pilot/total) × team daily |
| Monthly volume | ___ /month | daily × 22 working days |

### A.3 — Model + API Cost

| Trường | Giá trị | Nguồn |
|---|---|---|
| Provider chính | ___ | [URL pricing page] |
| Model chọn | ___ | [URL pricing page] |
| Input price ($/1M tokens) | $___ | [URL] |
| Output price ($/1M tokens) | $___ | [URL] |
| Input tokens/task | ___ | Ước tính từ task type |
| Output tokens/task | ___ | Ước tính từ task type |
| API cost/task | $___ | (in × in_price + out × out_price) / 1M |

### A.4 — Tooling Cost

| Trường | Giá trị | Nguồn / Lý do |
|---|---|---|
| Vector DB | $___ /month | [Pinecone / Qdrant / pgvector / không cần] |
| Monitoring | $___ /month | [Langfuse / Helicone / không cần] |
| Orchestration | $___ /month | [n8n / Zapier / custom / không cần] |
| Other tooling | $___ /month | [Specify] |
| **Tổng tooling/tháng** | **$___** | Sum |

### A.5 — Human Review Cost

| Trường | Giá trị | Công thức / Lý do |
|---|---|---|
| Reviewer hourly rate | $___ /hr | [Brief hoặc loaded rate = 1.3-1.5× lương cơ bản] |
| Review time/task | ___ phút | [Ước tính từ brief constraint] |
| Cost/review | $___ /task | (phút / 60) × hourly |
| Monthly review cost | $___ /month | Monthly volume × cost/review |

### A.6 — Setup Cost (amortize)

| Trường | Giá trị | Lý do |
|---|---|---|
| One-time setup | $___ | [Integration + security review + prompt engineering] |
| Pilot duration | ___ months | [Brief field #8 chia 30] |
| Amortized setup/month | $___ /month | Setup / pilot duration |

### A.7 — Monthly Cost Formula

```text
Monthly AI Cost
  = (Monthly volume × API cost/task)            [API]
  + Tooling monthly                              [Vector DB + monitoring + ...]
  + (Monthly volume × Human review cost/task)    [Human review]
  + Amortized setup/month                        [Setup amortize]
```

Tính cho nhóm:

```text
Monthly AI Cost
  = (___ × $___)         = $___      [API]
  + $___                  = $___      [Tooling]
  + (___ × $___)         = $___      [Human review]
  + $___                  = $___      [Setup amortize]
                          ──────────
                          = $___ /month TOTAL
```

### A.8 — Budget Check

| Trường | Giá trị |
|---|---|
| Total monthly cost | $___ |
| Pilot budget | $___ (brief field #8) |
| % of budget | ___% |
| Status | ☐ Within budget ☐ Over budget |

**Nếu Over budget — hành động đề xuất**:

- [vd: dùng model rẻ hơn cho phần FAQ tier-1 / giảm volume pilot / negotiate enterprise pricing]
- [...]

---

## Section A — Insight ban đầu

Sau khi tính xong, ghi 2-3 insight đáng chú ý nhất về cost structure:

1. **Cost driver chính**: [vd: "Human review chiếm 89% cost, API chỉ 2%" — đây là pattern phổ biến với pilot có constraint 100% human review]
2. **Surprise cost** (chi phí nào ngoài dự đoán): [vd: "Vector DB rẻ hơn dự đoán; setup cost cao hơn dự đoán"]
3. **Sensitivity**: [Cost nhạy nhất với biến nào? Volume / model / human review time?]

---

## Checklist nộp Section A

- [ ] Usage unit pass 3-part test, có mô tả 1-2 câu rõ ràng.
- [ ] Pilot daily + monthly volume tính theo công thức (không khoảng).
- [ ] Có URL pricing source cho provider + model.
- [ ] Cost/task tính theo công thức tokens (không "estimate").
- [ ] Tooling cost có ghi rõ tên tool + giá tháng.
- [ ] Human review cost tính theo phút × rate (nếu brief có constraint review).
- [ ] Setup cost được amortize theo tháng pilot.
- [ ] Monthly cost formula có 4 component cộng lại bằng total.
- [ ] Budget check so với brief field #8.

Đếm số trường đã điền: ___ / 30+ trường

Yêu cầu tối thiểu: 25 trường có số cụ thể.

---

## Anti-pattern (lỗi hay mắc — kiểm tra trước khi nộp)

| Đừng làm | Nên làm |
|---|---|
| "Cost/task khoảng $0.01" | "$0.0084 (in 800 × $3 + out 400 × $15 / 1M)" |
| Quên human review cost | Nếu brief có 100% review → cost này thường là phần lớn nhất |
| Dùng full-team volume | Dùng PILOT volume (5/25 × 800 = 160/day, không phải 800/day) |
| Tooling = $0 | Ít nhất có monitoring (Langfuse free tier vẫn ghi $0) |
| Setup = $0 | Integration + prompt engineering luôn có cost (developer time) |
| Cost/task < $0.0001 | Kiểm tra lại — model classify rẻ nhất GPT-4o-mini cũng $0.000135/task |
| Cost/task > $50 cho 1 simple task | Model chọn quá to — thử model rẻ hơn |
| Không ghi URL pricing | Mỗi giá API phải có URL pricing page |

---

## Next: Section B + C

Sau khi chốt Section A, chuyển sang `worksheet/02-pricing-value/` để dựng Section B (Pricing/Access) và Section C (Value/ROI).

Cost model một mình không trả lời được "có nên build không" — cần ghép với Value để tính ROI.
