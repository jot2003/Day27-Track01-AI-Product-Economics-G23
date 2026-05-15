# 05 · Recommendation + Justification

> **Mục tiêu**: Chọn config nhóm recommend deploy, viết justification, và chuẩn bị 5 phút present.

---

## 4 Câu hỏi PM

### 1. Recommend config nào?

Nhóm recommend **Smart Mix** cho cả 2 scenarios. Monthly cost chỉ $143 (Scenario A) và $702 (Scenario B) — tiết kiệm 96.8% và 96.1% so với human baseline, trong khi Quality estimate đạt Med-High đủ phục vụ khách quốc tế đòi hỏi thông tin chính xác về Visa và điểm đến. So với Budget Bot ($9/$43/tháng nhưng Quality Low và thiếu web), Smart Mix đáng đầu tư thêm ~$660/tháng để giữ thông tin Visa và thời tiết luôn cập nhật. Nếu chỉ deploy 1 config duy nhất quanh năm, Smart Mix là lựa chọn duy nhất không cần đổi config theo mùa.

### 2. So với human baseline $0.50/conv → tiết kiệm bao nhiêu?

Smart Mix tiết kiệm 96.8% ở Scenario A ($4,357/tháng so với human) và 96.1% ở Scenario B ($17,298/tháng). Không có config nào đắt hơn human — ngay cả Premium Concierge đắt nhất cũng chỉ $2,490/tháng, rẻ hơn human 7.22×. AI không thể replace nhân viên Sales hoàn toàn — Booking vẫn cần 1 agent để convert; AI thắng ở khả năng serve 24/7, tiếng Anh chuẩn, và handle đồng thời nhiều khách trong peak season mà không tăng headcount.

### 3. Khi nào nên upgrade / downgrade config?

Nên upgrade lên Premium Concierge khi: (1) quality complaint rate vượt 5% — dấu hiệu Smart Mix không đủ chính xác cho khách VIP; (2) approaching Tết hoặc mùa lễ hội lớn với booking value cao (revenue per booking > $500) — chi phí thêm $1,788/tháng (từ $702 lên $2,490) justify được nếu conversion tăng chỉ 4 booking/tháng. Nên downgrade về Budget Bot khi: volume < 100 conv/ngày kéo dài > 2 tuần, và 80%+ câu hỏi là Guide/FAQ đơn giản không cần web search.

### 4. Rủi ro lớn nhất của config được chọn?

Rủi ro chính: intent classifier nhận sai loại → bot dùng Flash-Lite thay vì Haiku 4.5 cho câu hỏi Visa phức tạp, dẫn đến câu trả lời thiếu chính xác và tiềm năng tạo bad review. Mitigation: thêm confidence threshold — nếu keyword classifier không chắc chắn (score < 0.8), fallback sang human agent. Rủi ro phụ: Anthropic hoặc Google tăng giá API → monthly cost tăng; mitigation: theo dõi cost hàng tuần, có sẵn phương án chuyển Visa intent sang DeepSeek V4 Pro (rẻ hơn ~43%) mà không cần thay đổi toàn bộ kiến trúc.

---

## Final Answer

Nhóm G23 recommend deploy **Smart Mix** cho travel agency chatbot phục vụ khách quốc tế quanh năm. Config này định tuyến câu hỏi Visa sang Claude Haiku 4.5 (chính xác, có web search cập nhật) trong khi FAQ điểm đến dùng Gemini Flash-Lite giá rẻ — chi phí $143/tháng mùa thấp điểm và $702/tháng mùa cao điểm, tiết kiệm lần lượt 96.8% và 96.1% so với chi phí nhân viên $4,500/$18,000/tháng. Không có config nào đắt hơn human baseline; AI thắng trên 3 chiều: hoạt động 24/7, phục vụ đa ngôn ngữ, và scale không giới hạn mà không tăng headcount. Rủi ro lớn nhất là nhầm intent → dùng sai model, giải quyết bằng confidence threshold và human fallback. Nếu complaint rate vượt 5% hoặc approaching peak season với booking value cao, nên upgrade lên Premium Concierge; nếu volume thấp kéo dài, downgrade về Budget Bot để tối ưu chi phí.

---

## Chuẩn bị Present (5 phút)

### Nhịp 0:00 – 0:30 — Base flow + 3 knobs

**Người trình bày:** Hoàng Kim Trí Thành

Chatbot xử lý 5 intents: Visa, Guide, Weather (dùng RAG/Web rồi generate bằng LLM), còn Booking và Complaint thì handoff thẳng cho nhân viên (zero LLM cost). Ba knobs quyết định chi phí là Model Tier, Web Search (ON/OFF theo intent), và History length — đây là 3 thứ chúng tôi đã tweak để tạo ra 3 configs hoàn toàn khác nhau.

### Nhịp 0:30 – 1:00 — Config overview

**Người trình bày:** Nguyễn Thành Nam

Config 1 "Budget Bot" tối ưu chi phí (model siêu rẻ, tắt web, history ngắn). Config 2 "Premium Concierge" ưu tiên trải nghiệm 5 sao (model xịn, bật web chọn lọc, full history). Config 3 "Smart Mix" cân bằng chất lượng/chi phí bằng cách linh hoạt tuỳ biến theo từng loại intent.

### Nhịp 1:00 – 2:00 — Cost comparison

**Người trình bày:** Quách Gia Được

Budget Bot là lựa chọn rẻ nhất với chi phí chỉ $43/tháng (Scenario B), rẻ gấp 57.8× so với Premium Concierge ($2,490/tháng). Mức chênh lệch lớn này phản ánh rõ tradeoff chất lượng: Budget Bot siêu tiết kiệm nhưng thiếu thông tin cập nhật và dễ mất ngữ cảnh. Quyết định đầu tư phụ thuộc vào việc ưu tiên kiểm soát budget (mùa thấp điểm) hay trải nghiệm VIP.

### Nhịp 2:00 – 3:00 — Key insight

**Người trình bày:** Nguyễn Thành Nam

Model Tier là yếu tố ảnh hưởng mạnh nhất đến chi phí — dùng model đắt hơn đẩy base cost lên hàng chục lần. Tiếp theo là History Management: ở Scenario B (7 turns), Full History khiến token input đội lên theo cấp số cộng qua từng lượt, trong khi Last 5 cắt ngưỡng hợp lý mà không mất ngữ cảnh.

### Nhịp 3:00 – 4:30 — Recommendation + justification

**Người trình bày:** Hoàng Kim Trí Thành

*(Đọc Final Answer ở trên)*

### Nhịp 4:30 – 5:00 — Hardest Q&A

**Người trình bày:** Quách Gia Được

**Câu hỏi dự đoán:** Tại sao chi phí Premium Concierge ở Scenario B tăng vọt lên $2,490/tháng dù volume chỉ ×4 so với Scenario A ($514/tháng)?

**Trả lời:** Scenario B yêu cầu hội thoại dài hơn (7 lượt vs 4 lượt). Vì Premium dùng Full History, token input ở các lượt sau phình to rất nhanh, cộng hưởng với giá đắt đỏ của Sonnet 4.6. Để tối ưu, có thể chuyển sang Summarize history hoặc dùng DeepSeek V4 Pro thay Sonnet (rẻ hơn ~43%) mà không đổi toàn bộ kiến trúc.

---

## Q&A — 3 câu instructor thường hỏi

**1. Knob nào ảnh hưởng cost nhiều nhất?**
Model Tier — Flash-Lite vs Sonnet chênh ~20-50× base cost. History là knob thứ 2 ở Scenario B: Full history đội token theo cấp số cộng, Last 5 cắt ngưỡng hợp lý.

**2. Nếu provider tăng giá API ×2 → config còn sống được không?**
Smart Mix monthly B tăng từ $702 lên ~$1,404 — vẫn rẻ hơn human $18,000 gấp ~12.8×, hoàn toàn sống được. Budget Bot cũng sống được (~$86/tháng). Chỉ Premium Concierge mới đáng lo (~$4,980) nhưng vẫn rẻ hơn human ~3.6×.

**3. So với nhóm khác — tại sao chọn khác?**
*(Chuẩn bị sau khi nghe nhóm kia present)*

---

## Bảng kiểm

- [x] Đã trả lời 4 câu PM (Recommend / Savings / Threshold / Risk)
- [x] Final answer paragraph viết gọn (5–7 câu)
- [x] Phân công 5 nhịp present cho mỗi thành viên
- [x] Có sẵn câu trả lời cho 3 câu Q&A dự đoán
- [x] Comparison table có sẵn để chiếu / chuyền tay khi present
- [x] Repo đã commit + push
