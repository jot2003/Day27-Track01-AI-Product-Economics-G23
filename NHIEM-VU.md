# Phân công nhiệm vụ — Nhóm G23

> Lab D27 · AI Conversation Cost Simulator · VinUni A20 AI Thực Chiến

| Thành viên | MSSV | Vai trò |
|---|---|---|
| Hoàng Kim Trí Thành | 2A202600372 | PM / Lead — Recommendation & Base Flow |
| Quách Gia Được | 2A202600423 | Cost Analyst — Budget Config & Comparison Table |
| Nguyễn Thành Nam | 2A202600205 | Config Designer — Premium & Smart Mix |

---

## Phần 1 — Setup (10:10 → 10:25, 15 phút)

### Làm cùng nhau (5 phút đầu)
Cả nhóm mở `worksheet/00-user-journey.md`, mỗi người viết tourist questions của mình song song.

| Việc | Ai làm | File |
|---|---|---|
| Tourist #1 — viết 5–7 câu hỏi tiếng Anh | **Hoàng Kim Trí Thành** | `worksheet/00-user-journey.md` |
| Tourist #2 — viết 5–7 câu hỏi tiếng Anh | **Quách Gia Được** | `worksheet/00-user-journey.md` |
| Tourist #3 — viết 5–7 câu hỏi tiếng Anh | **Nguyễn Thành Nam** | `worksheet/00-user-journey.md` |
| Gom câu hỏi + phân loại intent (bảng 10 dòng) | **Nguyễn Thành Nam** điền, cả nhóm góp ý | `worksheet/00-user-journey.md` |
| Vẽ base flow (ASCII) + chốt 3 knobs | **Hoàng Kim Trí Thành** vẽ, cả nhóm duyệt | `worksheet/01-base-flow.md` |

---

## Phần 2 — Main (10:25 → 11:40, 75 phút)

### Config Design — `worksheet/02-config-design.md`

| Config | Tên gợi ý | Người thiết kế | Định hướng |
|---|---|---|---|
| Config 1 | **"Budget Bot"** | **Quách Gia Được** | Cheap model, web OFF, Last 3 — tối thiểu chi phí |
| Config 2 | **"Premium Concierge"** | **Nguyễn Thành Nam** | Strong model, web ON selective, Full history — chất lượng cao |
| Config 3 | **"Smart Mix"** | **Hoàng Kim Trí Thành** | Mix model theo intent, web ON selective, Last 5 — cân bằng |

Mỗi người điền phần config của mình vào `02-config-design.md` (tên + 3 knobs + lý do + rủi ro).

### Cost Calculation — `worksheet/03-cost-calculation.md`

| Việc | Ai làm | Deadline nội bộ |
|---|---|---|
| Tính cost Config 1 (Scenario A + B) | **Quách Gia Được** | ⚑ 11:00 |
| Tính cost Config 2 (Scenario A + B) | **Nguyễn Thành Nam** | ⚑ 11:00 |
| Tính cost Config 3 (Scenario A + B) | **Hoàng Kim Trí Thành** | ⚑ 11:20 |
| Điền quality + speed estimate (3 configs) | Cả nhóm chốt cùng nhau | ⚑ 11:20 |

**Cách tính**: Dùng prompt template ở `prompts/01-cost-calc.md`, dán vào Claude/ChatGPT. Không tính tay.

---

## Phần 3 — Final (11:40 → 12:00, 20 phút)

| Việc | Ai làm | File |
|---|---|---|
| Điền bảng so sánh đầy đủ (copy số từ file 03) | **Quách Gia Được** | `worksheet/04-comparison-table.md` |
| Trả lời 4 câu quan sát (câu 1–4 cuối file 04) | **Nguyễn Thành Nam** | `worksheet/04-comparison-table.md` |
| Viết 4 câu PM + Final paragraph recommendation | **Hoàng Kim Trí Thành** | `worksheet/05-recommendation.md` |
| Phân công 5 nhịp present (điền tên vào file 05) | Cả nhóm chốt | `worksheet/05-recommendation.md` |

---

## Phân công Present (5 phút)

| Nhịp | Thời gian | Nội dung | Người trình bày |
|---|---|---|---|
| 0 | 0:00 – 0:30 | Base flow + 3 knobs đã chọn | **Hoàng Kim Trí Thành** |
| 1 | 0:30 – 1:00 | Config overview (tên + knobs 3 configs) | **Nguyễn Thành Nam** |
| 2 | 1:00 – 2:00 | Cost comparison (chiếu bảng, highlight rẻ/đắt nhất) | **Quách Gia Được** |
| 3 | 2:00 – 3:00 | Key insight (knob nào ảnh hưởng cost nhất) | **Nguyễn Thành Nam** |
| 4 | 3:00 – 4:30 | Recommendation + justification (đọc Final paragraph) | **Hoàng Kim Trí Thành** |
| 5 | 4:30 – 5:00 | Hardest Q&A prep | **Quách Gia Được** |

---

## Checklist nộp bài

- [ ] `worksheet/00-user-journey.md` — 3 tourist đã viết câu hỏi, bảng intent đã điền
- [ ] `worksheet/01-base-flow.md` — flow vẽ xong, 3 knobs đã chốt
- [ ] `worksheet/02-config-design.md` — 3 configs đặt tên + knobs + lý do
- [ ] `worksheet/03-cost-calculation.md` — cost/conv + monthly cho 3 configs × 2 scenarios
- [ ] `worksheet/04-comparison-table.md` — bảng đầy đủ, 4 câu quan sát
- [ ] `worksheet/05-recommendation.md` — 4 câu PM + Final paragraph + phân công present
- [ ] Commit + push lên GitHub trước **23:59 hôm nay**
- [ ] Dán link repo vào Discord `#day27-evidence-boards`

---

*Nhóm G23 · D27 · VinUni A20 AI Thực Chiến*
