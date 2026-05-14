---
artifact: 1 — Xác định Usage Unit + khung Cost Model
buoc: 1 — Cost Model
phase: Define usage unit + ước tính volume
time: 15 phút (xem deck slide 4 để biết khung giờ chính xác trong buổi)
input: 00-context.md + brief được giao + prompts/01-define-usage-unit.md
nop-cuoi: Không — file trung gian
---

# 1 — Xác định Usage Unit + ước tính volume

Mục tiêu: trước khi tính bất kỳ con số chi phí nào, nhóm phải định nghĩa rõ **AI làm GÌ trong MỘT lần chạy** (usage unit) và **MỖI tháng AI chạy bao nhiêu lần** (volume).

Lý do làm bước này: nếu không có usage unit, mọi con số sau (cost/task, value/task, monthly cost) đều không có nền tảng. Đây là "đơn vị nguyên tử kinh tế" của AI product.

Quy tắc: **không có usage unit = không có cost model**.

## Quy trình 15 phút

```text
5 phút  — Mỗi người tự đề xuất 1 usage unit
5 phút  — Cặp chọn 1, kiểm tra qua 3-part test
5 phút  — Ước tính volume từ brief
```

---

## Phần A — Đề xuất Usage Unit

### 3-part test (phải pass cả 3)

Để đảm bảo usage unit hợp lệ, kiểm tra 3 điều:

1. **Đếm được không?** — Có thể đếm số lần AI làm việc này (không phải "AI giúp đỡ" mà cụ thể: "AI sinh 1 reply", "AI flag 1 post").
2. **Có tốn token không?** — Mỗi lần chạy đều gọi API → tốn chi phí.
3. **Người dùng có thấy giá trị không?** — Một lần chạy có rút ngắn thời gian / cải thiện chất lượng cho user?

Cả 3 = Có → usage unit hợp lệ.

### Đề xuất của nhóm

Mỗi thành viên tự đề xuất 1 usage unit. Sau đó cặp thảo luận chọn 1.

**Đề xuất 1**: [...]

- Đếm được? [Có / Không / chưa rõ]
- Tốn token? [Có / Không / chưa rõ]
- Có giá trị? [Có / Không / chưa rõ]

**Đề xuất 2**: [...]

- Đếm được?
- Tốn token?
- Có giá trị?

**Usage unit cặp CHỌN**: [...]

**Lý do chọn**: [vì sao usage unit này phù hợp với brief hơn các đề xuất khác]

---

## Phần B — Common mistakes (đối chiếu)

Kiểm tra usage unit của nhóm KHÔNG rơi vào các bẫy sau:

| Bẫy | Ví dụ sai | Lý do sai |
|---|---|---|
| Quá rộng | "AI hỗ trợ support" | Không đếm được — không biết "hỗ trợ" tính 1 lần hay nhiều lần |
| Quá hẹp | "1 token AI sinh ra" | Đếm được nhưng không có giá trị user — user không trả tiền theo token |
| Không phải atomic | "1 ticket được giải quyết" | Trong copilot, 1 ticket có thể gọi AI nhiều lần (search KB, draft, refine). Atomic phải là "1 lần AI chạy" |
| Mix workflow vs AI | "1 buổi support shift" | Bao gồm cả công việc human không liên quan AI |
| Đúng kỹ thuật, sai business | "1 API call" | Đúng technical nhưng không nối được với giá trị user |

**Usage unit của nhóm có rơi vào bẫy nào không?**

- [Có / Không. Nếu có, sửa lại trước khi tiếp tục]

---

## Phần C — Mô tả chi tiết Usage Unit

Mở rộng usage unit thành mô tả đầy đủ:

**Tên usage unit**: [vd: "1 ticket reply draft"]

**Mô tả 2-3 câu**: AI nhận input gì, sinh output gì, output đi đâu?

[Ví dụ: "AI nhận nội dung ticket + 3 KB articles liên quan (từ vector search), sinh ra 1 bản nháp trả lời dài 80-200 từ. Bản nháp được hiển thị trong Zendesk side panel để agent edit/copy/send."]

**Trigger** (khi nào AI chạy):

- [Ví dụ: agent click "Draft with AI" → AI chạy 1 lần]
- [Auto trigger khi ticket vào queue?]
- [Manual trigger?]

**Input dự kiến** (1 lần chạy):

- [Ví dụ: ticket subject + body + 3 KB articles + customer history (5 ticket gần nhất)]

**Output dự kiến** (1 lần chạy):

- [Ví dụ: 1 bản nháp 80-200 từ]

---

## Phần D — Ước tính Volume

### Pull từ brief

Đọc lại brief, kéo các con số sau:

- **Pilot users**: ___ (số người dùng AI trong pilot)
- **Total team**: ___ (tổng đội)
- **Team daily volume**: ___ (tổng số task team xử lý mỗi ngày)

### Tính pilot daily volume

Công thức:

```text
Pilot daily volume = (Pilot users / Total team) × Team daily volume
```

Tính cho nhóm:

```text
Pilot daily volume = (___ / ___) × ___ = ___ task/ngày
```

### Tính monthly volume

Công thức:

```text
Monthly volume = Pilot daily volume × 22 working days
```

Tính cho nhóm:

```text
Monthly volume = ___ × 22 = ___ task/tháng
```

**Lưu ý**: dùng PILOT volume, không phải full-team volume. Đây là sai lầm phổ biến.

---

## Phần E — Kiểm tra tính hợp lý

Trước khi chuyển sang Phase 2 (cost research), kiểm tra:

- [ ] Usage unit pass 3-part test (đếm, tốn token, có giá trị).
- [ ] Usage unit không quá rộng / quá hẹp.
- [ ] Volume tính từ pilot scope (không phải full team).
- [ ] Số ngày làm việc dùng = 22 (chuẩn 1 tháng).
- [ ] Volume cuối tính được số cụ thể (vd: 3,520 task/tháng), không phải "khoảng vài nghìn".

### Cảm giác (sanity check)

- Volume nhóm tính có khớp với scale brief không?
  - Vd: brief 800 ticket/ngày toàn team, pilot 5/25 → 160 ticket/ngày pilot là hợp lý.
  - Vd: brief 2M post/ngày → pilot 5/15 reviewer × 20K flag/ngày = 6,667 flag/ngày pilot.

---

## Phần F — Hint cho Phase 2 (Cost Research)

Trước khi vào phase 2, suy nghĩ trước:

- Model nào nhóm dự định dùng (đọc lại 00-context.md phần 6)?
- Input tokens dự kiến mỗi lần chạy bao nhiêu?
  - Ví dụ ngắn (classify): 200-500 tokens.
  - Ví dụ trung bình (draft reply): 800-1,500 tokens.
  - Ví dụ dài (legal contract review): 5K-20K tokens.
- Output tokens dự kiến bao nhiêu?
  - Ví dụ ngắn (label/classification): 50-100 tokens.
  - Ví dụ trung bình (reply draft): 300-500 tokens.
  - Ví dụ dài (analysis report): 1K-3K tokens.

Lưu lại ước tính này cho phase 2 — sẽ dùng để tính cost/task.

---

## Câu hỏi mở (cho Phase 2)

- Câu hỏi 1: [vd: "Vector DB cho KB search có cần không, giá bao nhiêu?"]
- Câu hỏi 2: [vd: "Có cần monitoring tool (Langfuse, Langsmith)?"]
- Câu hỏi 3: [...]

Sau bước này, chuyển sang `2-cost-research.md` để tra pricing và tính cost/task.
