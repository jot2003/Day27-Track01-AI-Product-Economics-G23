# 05 · Recommendation + Justification — Kết luận & Chuẩn bị Present

> **Mục tiêu**: Chọn 1 config (hoặc combo) nhóm recommend deploy, viết justification ngắn gọn, và chuẩn bị 5 phút present.
>
> **Thời gian**: 10 phút (cuối phần Final) — Pens down lúc 12:00

---

## Bảng số ai cũng tính được. PM giỏi phải **recommend** và **justify**.

Đây là phần quan trọng nhất — phần phân biệt nhóm chỉ làm xong với nhóm thực sự hiểu sản phẩm.

---

## 4 câu hỏi nhóm phải trả lời

Mỗi câu trả lời 2–4 câu. Không lan man, không clichés. Mỗi câu phải justify được bằng số trong bảng so sánh.

### Câu 1 — Recommend config nào?

Trước khi viết, thảo luận 1 phút:

- Recommend 1 config duy nhất chạy quanh năm? Hay 2 configs khác nhau cho mùa thấp / mùa cao?
- Có nên recommend "Smart Mix model theo intent" thay vì pick 1 config cố định không?
- Nếu sếp nói "chỉ deploy 1 config thôi" — chọn cái nào?

```text
Nhóm recommend Smart Mix cho cả 2 scenarios. Monthly cost chỉ $143 (Scenario A) và $702 (Scenario B) — tiết kiệm 96.8% và 96.1% so với human baseline, trong khi Quality estimate đạt Med-High đủ phục vụ khách quốc tế đòi hỏi thông tin chính xác về Visa và điểm đến. So với Budget Bot (chỉ $9/$43/tháng nhưng Quality Low và thiếu web), Smart Mix đáng đầu tư thêm ~$660/tháng để giữ thông tin Visa và thời tiết luôn cập nhật. Nếu sếp ép chọn 1 config duy nhất, Smart Mix là lựa chọn duy nhất có thể deploy quanh năm mà không cần đổi config theo mùa.
```

### Câu 2 — So với human baseline $0.50/conv → tiết kiệm bao nhiêu? Có đắt hơn human ở chỗ nào không?

```text
Smart Mix tiết kiệm 96.8% ở Scenario A ($4,357/tháng so với human) và 96.1% ở Scenario B ($17,298/tháng). Không có config nào đắt hơn human — ngay cả Premium Concierge đắt nhất cũng chỉ tốn $2,490/tháng, rẻ hơn human 7.22×. Điểm cần justify thêm: AI không thể replace nhân viên Sales hoàn toàn — Booking vẫn cần 1 agent để convert; AI thắng ở khả năng serve 24/7, tiếng Anh chuẩn, và handle đồng thời nhiều khách trong peak season mà không tăng headcount.
```

### Câu 3 — Khi nào nên upgrade / downgrade config?

Trước khi viết, tự hỏi:

- Volume bao nhiêu thì cost AI scale lớn hơn benefit?
- Quality complaint rate bao nhiêu thì biết Budget Bot không đủ?
- Có signal nào báo nên chuyển sang Premium? (mùa cao điểm bắt đầu? customer feedback?)

```text
Nên upgrade lên Premium Concierge khi: (1) quality complaint rate vượt 5% — dấu hiệu Smart Mix không đủ chính xác cho khách VIP; (2) approaching Tết hoặc mùa lễ hội lớn với booking value cao (revenue per booking > $500) — chi phí thêm $1,788/tháng (từ $702 lên $2,490) justify được nếu conversion tăng chỉ 4 booking/tháng. Nên downgrade về Budget Bot khi: volume < 100 conv/ngày kéo dài > 2 tuần liên tiếp, và 80%+ câu hỏi là Guide/FAQ đơn giản không cần web search — lúc đó $9/tháng hoàn toàn đủ.
```

### Câu 4 — Rủi ro lớn nhất của config được chọn?

Trước khi viết, tự hỏi:

- Rủi ro về quality? (visa info outdated? language mismatch?)
- Rủi ro về cost? (provider tăng giá? volume spike?)
- Rủi ro về business? (khách bị bot trả lời sai → bad review → mất khách?)
- Có mitigation plan không?

```text
Rủi ro chính: intent classifier nhận sai loại → bot dùng Flash-Lite thay vì Haiku 4.5 cho câu hỏi Visa phức tạp, dẫn đến câu trả lời thiếu chính xác và tiềm năng tạo bad review. Mitigation: thêm confidence threshold — nếu keyword classifier không chắc chắn (score < 0.8), fallback sang human agent thay vì đoán intent. Rủi ro phụ: Anthropic hoặc Google tăng giá API → monthly cost tăng; mitigation: theo dõi cost dashboard hàng tuần và có sẵn phương án chuyển Visa intent sang DeepSeek V4 Pro (giá thấp hơn ~43%) mà không cần thay đổi toàn bộ kiến trúc.
```

---

## Final answer — Recommendation in 1 paragraph

Tổng hợp 4 câu trên thành 1 paragraph 5–7 câu — đây là phần nhóm sẽ đọc / chiếu khi present.

```text
Nhóm G23 recommend deploy Smart Mix cho travel agency chatbot phục vụ khách quốc tế quanh năm. Config này định tuyến câu hỏi Visa sang Claude Haiku 4.5 (chính xác, có web search cập nhật) trong khi FAQ điểm đến dùng Gemini Flash-Lite giá rẻ — chi phí $143/tháng mùa thấp điểm và $702/tháng mùa cao điểm, tiết kiệm lần lượt 96.8% và 96.1% so với chi phí nhân viên $4,500/$18,000/tháng. Không có config nào đắt hơn human baseline; AI thắng trên 3 chiều: hoạt động 24/7, phục vụ đa ngôn ngữ, và scale không giới hạn mà không tăng headcount. Rủi ro lớn nhất là nhầm intent → dùng sai model, giải quyết bằng confidence threshold và human fallback. Nếu complaint rate vượt 5% hoặc approaching peak season với booking value cao, nên upgrade lên Premium Concierge; nếu volume thấp kéo dài, downgrade về Budget Bot để tối ưu chi phí.
```

---

## Chuẩn bị Present (5 phút)

Chia 5 phút thành 5 nhịp. 1 người trong nhóm chính phụ trách 1 nhịp. Người còn lại trả lời Q&A.

### Nhịp 0:00 – 0:30 — Base flow + 3 knobs đã chọn

Ai trình bày: Hoàng Kim Trí Thành

Nói gì:

```text
Chatbot của chúng tôi xử lý 5 intents: Visa, Guide, Weather (đều dùng RAG/Web rồi generate bằng LLM), còn Booking và Complaint thì handoff thẳng cho nhân viên (zero LLM cost). Ba knobs quyết định chi phí là: Model Tier, Web Search (ON/OFF theo intent), và History length — và đây là 3 thứ chúng tôi đã tweak để tạo ra 3 configs hoàn toàn khác nhau.
```

### Nhịp 0:30 – 1:00 — Config overview

Ai trình bày: Nguyễn Thành Nam

Nói gì (đọc nhanh tên + knobs 3 configs):

```text
Chúng tôi đã thiết kế các config với các định hướng khác nhau. Config 1 'Budget Bot' tối ưu chi phí (model siêu rẻ, tắt web, history ngắn). Config 2 'Premium Concierge' ưu tiên trải nghiệm 5 sao (model xịn, bật web chọn lọc, full history). Config 3 'Smart Mix' cân bằng chất lượng/chi phí bằng cách linh hoạt tuỳ biến theo từng loại intent.
```

### Nhịp 1:00 – 2:00 — Cost comparison

Ai trình bày: Quách Gia Được

Nói gì (chiếu bảng so sánh, highlight rẻ nhất / đắt nhất):

```text
Nhìn vào bảng so sánh, ta thấy Budget Bot là lựa chọn rẻ nhất với chi phí chỉ $43/tháng cho Scenario B, rẻ gấp 57.8 lần so với Premium Concierge ($2490/tháng). Mức chênh lệch lớn này phản ánh rõ chất lượng dịch vụ: Budget Bot siêu tiết kiệm nhưng thiếu thông tin cập nhật (tắt Web) và dễ mất ngữ cảnh. Quyết định đầu tư sẽ phụ thuộc vào việc chúng ta ưu tiên kiểm soát budget (mùa thấp điểm) hay trải nghiệm VIP (khách sạn/tour cao cấp).
```

### Nhịp 2:00 – 3:00 — Key insight

Ai trình bày: Nguyễn Thành Nam

Nói gì (knob nào ảnh hưởng cost nhiều nhất + tại sao):

```text
Qua phân tích số liệu, chúng tôi nhận thấy 'Model Tier' là yếu tố ảnh hưởng mạnh nhất đến chi phí, việc dùng model đắt hơn đẩy base cost lên hàng chục lần. Tiếp theo là 'History Management', ở những hội thoại dài như Scenario B, việc dùng Full History khiến số lượng token phải xử lý bị đội lên theo cấp số cộng qua từng lượt, gây tốn kém đáng kể so với việc cắt ngắn lịch sử (Last 3).
```

### Nhịp 3:00 – 4:30 — Recommendation + justification

Ai trình bày: Hoàng Kim Trí Thành

Nói gì (đọc paragraph "Final answer" ở trên):

```text
Nhóm G23 recommend deploy Smart Mix cho travel agency chatbot phục vụ khách quốc tế quanh năm. Config này định tuyến câu hỏi Visa sang Claude Haiku 4.5 (chính xác, có web search cập nhật) trong khi FAQ điểm đến dùng Gemini Flash-Lite giá rẻ — chi phí $143/tháng mùa thấp điểm và $702/tháng mùa cao điểm, tiết kiệm lần lượt 96.8% và 96.1% so với chi phí nhân viên $4,500/$18,000/tháng. Không có config nào đắt hơn human baseline; AI thắng trên 3 chiều: hoạt động 24/7, phục vụ đa ngôn ngữ, và scale không giới hạn mà không tăng headcount. Rủi ro lớn nhất là nhầm intent → dùng sai model, giải quyết bằng confidence threshold và human fallback. Nếu complaint rate vượt 5% hoặc approaching peak season với booking value cao, nên upgrade lên Premium Concierge; nếu volume thấp kéo dài, downgrade về Budget Bot để tối ưu chi phí.
```

### Nhịp 4:30 – 5:00 — Hardest question prep

Ai trình bày: Quách Gia Được

Nhóm dự đoán câu hỏi khó nhất sẽ bị hỏi là gì?

```text
Tại sao chi phí của Premium Concierge ở Scenario B lại tăng vọt lên tới $2490/tháng, mặc dù volume chỉ gấp 4 lần so với Scenario A ($513/tháng)? Có cách nào tối ưu không?
```

Câu trả lời sẵn:

```text
Chi phí tăng vọt một phần do Scenario B yêu cầu hội thoại dài hơn (7 lượt so với 4 lượt). Vì Premium dùng Full History, lượng token input ở các lượt sau sẽ phình to rất nhanh, cộng hưởng với giá đắt đỏ của model Claude Sonnet 4.6. Để tối ưu, chúng ta có thể chuyển sang Summarize history thay vì giữ Full History nguyên bản, hoặc dùng Strong Model giá rẻ hơn như DeepSeek V4 Pro.
```

---

## Q&A — 2 phút sau khi present xong

Sẵn sàng cho 1 câu từ class + 1 câu từ instructor. Không cần lo lắng — nếu chưa biết câu trả lời, nói "đây là điểm nhóm chưa nghĩ đến — sẽ tính lại sau buổi".

**3 câu instructor thường hỏi**:

1. *"Knob nào ảnh hưởng cost nhiều nhất trong config của nhóm? Tại sao?"*
2. *"Nếu provider tăng giá API ×2 → config của nhóm còn sống được không?"*
3. *"So với nhóm X (vừa present trước) — tại sao nhóm bạn chọn khác?"*

Suy nghĩ trước câu trả lời ngắn:

```text
1. Model Tier ảnh hưởng nhiều nhất — Flash-Lite vs Sonnet chênh nhau ~20-50× base cost. History là knob thứ 2 ảnh hưởng tới Scenario B (7 turns): Full history đội token theo cấp số cộng, còn Last 5 cắt ngưỡng hợp lý.
2. Nếu API tăng giá ×2 thì Smart Mix monthly B tăng từ $702 lên khoảng $1,404 — vẫn rẻ hơn human $18,000 gấp ~12.8×, hoàn toàn sống được. Budget Bot cũng sống được (~$86/tháng). Chỉ Premium Concierge mới đáng lo ($4,980) nhưng vẫn rẻ hơn human ~3.6×.
3. (Tùy nhóm X present — chuẩn bị sau khi nghe họ xong)
```

---

## Bảng kiểm cuối cùng — trước 12:00 Pens Down

- [x] Đã trả lời 4 câu PM (Recommend / Savings / Threshold / Risk)
- [x] Final answer paragraph viết gọn (5–7 câu)
- [x] Phân công 5 nhịp present cho mỗi thành viên
- [x] Có sẵn câu trả lời cho 3 câu Q&A dự đoán
- [x] Comparison table có sẵn để chiếu / chuyền tay khi present
- [x] Repo đã commit + push (sẽ nộp link sau buổi học)

---

## Sau buổi học

1. **Commit + push repo** với tất cả file đã điền.
2. **Dán link repo** vào Discord `#day27-evidence-boards` trước 23:59.
3. **Chuẩn bị cho D28**: peer review giữa các nhóm — sẽ bị hỏi câu chất vấn khó hơn instructor. Polish thêm bảng + recommendation tối nay.

*Hôm nay bạn chứng minh bằng số. Ngày mai bạn bảo vệ bằng logic.*
