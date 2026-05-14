---
title: 00 — Bối cảnh nhóm cho Day 27
section: Day 27 — dùng lại cho mọi cuộc trò chuyện với AI trong cả 3 bước Lab
format: Nhóm (pair)
time: Điền 5 phút đầu buổi
---

# 00-context.md — Bối cảnh nhóm

Điền file này một lần ở đầu buổi. Sau đó, mỗi lần dùng AI hỗ trợ (cho Step 1 / 2 / 3), hãy đưa toàn bộ nội dung file này vào đầu cuộc trò chuyện.

Lý do: AI không tự nhớ bối cảnh giữa các cuộc trò chuyện. Nếu mỗi lần đưa bối cảnh khác nhau, công thức tính cũng sẽ lệch.

Khác với Day 26 (chọn 2 sản phẩm AI để thử nghiệm), Day 27 cần bối cảnh **kinh tế của 1 use case cụ thể**: cặp nhận 1 challenge brief, tính cost / value / ROI / stress test cho brief đó.

---

## 1. Brief được giao

Mỗi cặp được giao **1 brief duy nhất** trong `challenge-brief-bank.md`. Brief gồm 9 trường:

1. Bối cảnh doanh nghiệp.
2. Quy trình hiện tại.
3. Điểm đau.
4. Dữ liệu sẵn có.
5. Ràng buộc.
6. Quyết định cần đưa ra.
7. Chỉ số nền.
8. Ngân sách / thời gian pilot.
9. Ranh giới rủi ro.

**Brief được giao**: # [...] — [tên brief, vd: AI Support Copilot]

**Lý do brief này phù hợp với nhóm** (nếu giảng viên chỉ định ngẫu nhiên, ghi "ngẫu nhiên"):

- [...]

---

## 2. Tóm tắt brief (1-2 câu)

Viết 1-2 câu mô tả brief để nhanh chóng paste vào prompt AI. Bao gồm: domain, use case, scale (số user, volume/ngày), budget, constraint chính.

**Tóm tắt brief**:

[Ví dụ: B2B SaaS support team 25 agent, 800 ticket/ngày. Pilot 5 agent x 90 ngày, ngân sách $5,000/tháng. AI copilot draft reply, agent senior review, không auto-send (compliance constraint).]

---

## 3. Bối cảnh nhóm

- **Thành viên cặp**: [tên + mã học viên × 2 người]
- **Background nhóm với domain brief**:
  - Ai có kinh nghiệm trong ngành brief: [...]
  - Mức độ rành: [mới nghe / có đọc / có làm việc qua / chuyên gia trong ngành]
- **Background nhóm với AI cost calculation**:
  - Đã từng tính cost cho AI product trước đây chưa: [chưa / có, ở dự án ___]
  - Đã từng dùng AI provider pricing pages chưa: [...]
- **Công cụ nhóm sẽ dùng cho lab**:
  - AI assistant cho prompt: [Claude / ChatGPT / Gemini / Perplexity — chọn 1 chính]
  - Spreadsheet: [Google Sheets / Excel / chỉ markdown tay]

---

## 4. Driving question của nhóm

Câu hỏi chính buổi này dành cho brief của nhóm:

> "Nếu thật sự deploy AI solution cho brief [#__], **kinh tế và rủi ro có sống nổi không** ở pilot scale?"

**Câu trả lời sơ bộ trước khi tính** (intuition của nhóm, 1-2 câu):

[Ví dụ: "Nhóm đoán ROI sẽ marginal vì human review chiếm phần lớn cost, nhưng có thể survive ở pilot scale do volume thấp."]

Mục đích ghi câu intuition: sau khi tính xong sẽ so sánh thực tế với dự đoán → rút bài học về độ chính xác của intuition.

---

## 5. Các con số chính sẽ cần (kéo từ brief)

Pre-fill những con số có sẵn trong brief để tránh phải đọc lại:

- **Pilot users**: [số agent / nurse / lawyer / SDR pilot]
- **Total team**: [tổng đội]
- **Volume/day (toàn team)**: [800 ticket / 20K flag / 300 patient / ...]
- **Pilot duration**: [60 / 90 ngày / 1 học kỳ]
- **Budget/month**: [$2K / $3K / $5K / $8K / $10K / $12K]
- **Original task time**: [phút/đơn vị work]
- **Key constraint**: [vd: 100% human review / không auto-send / explainable]

Nếu brief thiếu trường nào → ghi `[không có trong brief — cần giả định]`.

---

## 6. Provider AI nhóm dự định dùng

Trước khi vào Step 1, nhóm chọn sơ bộ provider để biết hướng tra pricing:

- **Provider chính**: [OpenAI / Anthropic / Google / Azure / Open source via Replicate]
- **Model dự kiến**: [GPT-4o / Claude 3.5 Sonnet / Gemini 1.5 Pro / Mistral / Llama 3]
- **Lý do chọn provider này** (chất lượng / giá / latency / dữ liệu staying region):
  - [...]

Lưu ý: có thể đổi provider sau khi tra pricing — đây chỉ là dự đoán ban đầu.

---

## 7. Ghi chú thêm

[Điền bất kỳ thông tin nào giúp AI hiểu bối cảnh: tỉ giá USD/VND nhóm dùng, language test (Anh/Việt), assumption đặc biệt về domain.]

---

## Cách dùng

```text
1. Mở AI assistant phù hợp với bước đang làm.
2. Đưa toàn bộ nội dung file này vào đầu cuộc trò chuyện.
3. Chọn prompt tham khảo từ thư mục ../prompts/ và chỉnh lại nếu cần.
4. Đọc lại bản nháp AI tạo ra.
5. Sửa lại cho đúng bối cảnh nhóm.
6. Lưu kết quả vào đúng file trong worksheet/.
```

Ghi chú: nội dung trong `[...]` là chỗ cần điền. Sau khi điền xong, xóa dấu ngoặc nếu không cần giữ.

---

## Lưu ý đặc thù Day 27

Day 27 khác với Day 25 / Day 26 ở 3 điểm:

1. **Fixed input** — brief là dữ kiện cho sẵn, không tự thay đổi. Nhóm chỉ thêm assumption (model dùng, adoption rate) và justify.
2. **Quy tắc số** — mỗi con số phải có công thức truy ngược về brief + provider pricing thực tế. **Không có công thức = không có số**.
3. **Verdict cuối** — output không phải bài phân tích, mà là **quyết định**: GO / CONDITIONAL / NO-GO. Quyết định này cần được defend bằng 5 scenario stress test, không phải bằng "feeling".

Cho Step 1 (Cost Model), cần phần 1, 2, 5, 6. Cho Step 2 (Pricing/Value), cần thêm phần 4. Cho Step 3 (Stress Test), cần đọc lại phần 9 trong brief (Risk boundary) để chọn scenario tệ nhất.
