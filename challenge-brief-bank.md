# Challenge Brief Bank — Day 27 Lab

Mỗi cặp nhận **một** brief trong danh sách dưới đây. Brief là toàn bộ ngữ cảnh kinh tế nhóm cần để dựng AI Economics Sheet (Cost → Pricing → Value → Stress Test → Verdict).

**Quy tắc dùng brief**:

- Đọc kỹ cả 9 trường trước khi tính bất kỳ con số nào.
- Mọi số liệu trong Economics Sheet phải truy ngược về brief hoặc về nguồn pricing thực tế nhóm tự tra.
- Nếu thấy ngữ cảnh chưa đủ chi tiết (vd: domain quá lạ với cả nhóm), giảng viên có thể cho phép thay thế brief — nhưng phải báo trước 10:10.

**Brief #1 (AI Support Copilot)** được viết chi tiết nhất để làm ví dụ mẫu — các brief sau viết cô đọng hơn nhưng vẫn đủ 9 trường.

---

## Brief #1 — AI Support Copilot

> **Domain**: B2B SaaS customer support
> **Pilot type**: AI hỗ trợ nhân viên (copilot), không tự gửi mail

### 1. Bối cảnh doanh nghiệp (Business context)

Công ty SaaS B2B, 200 nhân viên, ~15,000 khách hàng doanh nghiệp đang trả phí. Đội hỗ trợ khách hàng có 25 agent, xử lý khoảng 800 ticket mỗi ngày. CSAT hiện ở mức 72%, mục tiêu CEO đặt ra cho năm là 85%. Tỉ lệ churn liên quan đến trải nghiệm hỗ trợ kém: 18% (khảo sát exit survey, Q1).

### 2. Quy trình hiện tại (Current workflow)

Ticket đến → vào hàng đợi Zendesk → agent đọc → tìm tài liệu trong knowledge base (KB) → tự viết câu trả lời → agent senior review → gửi cho khách. Thời gian xử lý trung bình: 12 phút/ticket. First response time: 4 giờ.

### 3. Điểm đau (Pain points)

- 40% thời gian của agent dành cho việc tìm trong KB.
- KB cũ 30% — lần audit toàn bộ gần nhất cách đây 8 tháng.
- Câu hỏi FAQ tier-1 chiếm 45% tổng lượng ticket.
- Agent mới mất 3 tuần để đạt năng suất chuẩn.

### 4. Dữ liệu sẵn có (Available data)

- 50,000 ticket đã giải quyết kèm rating của khách (2 năm gần đây).
- 800 bài KB + tài liệu nội bộ.
- CSAT theo từng ticket.

### 5. Ràng buộc (Constraints)

- KHÔNG được auto-send cho khách hàng (yêu cầu pháp lý/compliance).
- PII (Personal Identifiable Information) phải được mask trước khi đưa vào AI.
- Cần phê duyệt IT security (quy trình 2 tuần).

### 6. Quyết định cần đưa ra (Decision needed)

CTO hỏi: "Có nên build AI copilot hỗ trợ agent viết bản nháp trả lời, hay xây auto-responder xử lý tự động FAQ tier-1?"

### 7. Chỉ số nền (Baseline metrics)

- Handle time: 12 phút/ticket.
- First response: 4 giờ.
- CSAT: 72%.

### 8. Ngân sách / Thời gian pilot (Pilot budget / time)

- Budget: $5,000/tháng.
- Thời gian: 90 ngày.
- Phạm vi: 5 agent (trên tổng 25).

### 9. Ranh giới rủi ro (Risk boundary)

- Gợi ý sai policy → vi phạm compliance.
- Auto-respond sai → mất niềm tin của khách.
- Agent lệ thuộc AI quá mức → kỹ năng suy giảm.

---

## Brief #2 — AI Content Moderator

> **Domain**: Social platform trust & safety
> **Pilot type**: AI pre-filter, người vẫn review 100%

### 1. Bối cảnh doanh nghiệp

Nền tảng mạng xã hội với 2 triệu bài đăng mỗi ngày. Đội Trust & Safety: 15 reviewer.

### 2. Quy trình hiện tại

Reviewer phải review thủ công 20,000 flag/ngày (do user báo cáo + hệ thống auto-detect). Mỗi flag mất khoảng 5 phút để đọc + đối chiếu policy + ra quyết định.

### 3. Điểm đau

- Backlog 6 giờ — nội dung nguy hiểm tồn tại trên platform lâu trước khi gỡ.
- 3% nội dung có hại nằm trên platform hơn 4 giờ trước khi bị xử lý.
- Reviewer burnout cao vì phải xem nội dung độc trong nhiều giờ liền.

### 4. Dữ liệu sẵn có

- 5 triệu flag đã được phân loại trong 12 tháng qua, có label rõ ràng.
- Policy nội bộ dài 80 trang, có 5 category chính.

### 5. Ràng buộc

- 100% quyết định gỡ bài phải có người review (yêu cầu pháp lý).
- AI chỉ được pre-filter và xếp ưu tiên, không tự gỡ.
- Phải log audit trail cho mỗi quyết định.

### 6. Quyết định cần đưa ra

VP Trust & Safety hỏi: "AI pre-filter cho 5 content categories có giúp giảm backlog 6 giờ xuống dưới 2 giờ không, đồng thời giữ chất lượng review?"

### 7. Chỉ số nền

- Backlog hiện tại: 6 giờ.
- Mục tiêu: dưới 2 giờ.
- Tỉ lệ false negative (bỏ sót nội dung độc): 3%.

### 8. Ngân sách / Thời gian pilot

- Budget: $8,000/tháng.
- Thời gian: 60 ngày.
- Phạm vi: 5 reviewer (trên 15).

### 9. Ranh giới rủi ro

- AI bỏ sót nội dung nguy hiểm (false negative) → tổn thương user, rủi ro pháp lý.
- AI flag nhầm nội dung lành (false positive) → reviewer tốn thời gian xử lý nhiễu.
- Sai sót lan rộng do volume cao (146K flag/tháng pilot) → cần monitoring chặt.

---

## Brief #3 — AI Medical Triage Assistant

> **Domain**: Bệnh viện cấp cứu (ER)
> **Pilot type**: AI pre-assessment, nurse luôn quyết định cuối

### 1. Bối cảnh doanh nghiệp

Bệnh viện đa khoa, khoa Cấp cứu (ER) tiếp nhận 300 bệnh nhân/ngày. Đội triage có 8 y tá, mỗi ca làm việc khoảng 6 y tá.

### 2. Quy trình hiện tại

Y tá phỏng vấn bệnh nhân khi tiếp nhận → chấm điểm bằng thang ESI (Emergency Severity Index) thủ công → xếp ưu tiên. Thời gian trung bình: 8 phút/bệnh nhân.

### 3. Điểm đau

- Thời gian chờ triage trung bình 15 phút, nhiều ca cấp cứu nặng chờ quá lâu.
- 12% bệnh nhân bị xếp sai mức ban đầu (phải triage lại).
- Thời điểm cao điểm: 1 y tá xử lý 2-3 bệnh nhân cùng lúc, dễ sai sót.

### 4. Dữ liệu sẵn có

- 200,000 hồ sơ triage trong 3 năm (intake form + ESI score + outcome thực tế).
- Quy trình ESI chuẩn của bệnh viện (60 trang).

### 5. Ràng buộc

- Y tá LUÔN là người ra quyết định triage cuối — AI chỉ gợi ý.
- Tuân thủ HIPAA (Mỹ) hoặc tương đương về bảo mật bệnh nhân.
- Không được trì hoãn quy trình triage hiện tại — AI phải chạy < 30 giây.

### 6. Quyết định cần đưa ra

Trưởng khoa hỏi: "AI pre-assessment từ intake form có giảm thời gian chờ xuống dưới 8 phút và giảm mis-triage rate xuống dưới 5%?"

### 7. Chỉ số nền

- Triage time: 8 phút/bệnh nhân.
- Wait time: 15 phút.
- Mis-triage: 12%.

### 8. Ngân sách / Thời gian pilot

- Budget: $3,000/tháng.
- Thời gian: 90 ngày.
- Phạm vi: 3 y tá (trong 8).

### 9. Ranh giới rủi ro

- AI gợi ý sai mức triage → bệnh nhân nặng chờ lâu, có thể tử vong.
- Y tá quá tin AI → bỏ qua tín hiệu thực tế.
- Privacy leak từ intake data → vi phạm pháp lý nghiêm trọng.

---

## Brief #4 — AI Legal Contract Reviewer

> **Domain**: Văn phòng luật M&A
> **Pilot type**: AI highlight điều khoản bất thường, luật sư verify

### 1. Bối cảnh doanh nghiệp

Văn phòng luật chuyên M&A, đội 8 luật sư xử lý 200 hợp đồng/tháng. Phần lớn là MSA (Master Service Agreement), NDA, share purchase agreement.

### 2. Quy trình hiện tại

Luật sư junior đọc toàn bộ hợp đồng → highlight các điều khoản cần lưu ý → tạo issue list → luật sư senior review. Trung bình 3 giờ/hợp đồng cho junior, 1 giờ cho senior.

### 3. Điểm đau

- Luật sư junior dành 60% thời gian cho phần review thường lệ (boilerplate clauses) — không học được gì mới.
- Bỏ sót nuance trong các điều khoản phức tạp (vd: indemnification, IP transfer) — phát hiện muộn ở giai đoạn negotiation.
- Tốc độ review chậm so với deadline khách hàng.

### 4. Dữ liệu sẵn có

- 5,000 hợp đồng M&A đã review trong 5 năm, có issue list đính kèm.
- Playbook nội bộ: 200 điều khoản chuẩn + 50 điều khoản red flag.

### 5. Ràng buộc

- Mọi điều khoản AI flag phải có luật sư verify trước khi đưa vào issue list chính thức.
- Hợp đồng có thể chứa thông tin client-privileged — không gửi ra cloud public.
- Phải có audit trail cho mỗi gợi ý AI.

### 6. Quyết định cần đưa ra

Managing partner hỏi: "AI highlight non-standard clauses có rút thời gian review xuống 40% và tăng độ chính xác phát hiện red flag không?"

### 7. Chỉ số nền

- Junior review time: 3 giờ/hợp đồng.
- Total cycle time: 4 giờ (junior + senior).
- Red flag miss rate: ~8% (theo hồi cứu 6 tháng qua).

### 8. Ngân sách / Thời gian pilot

- Budget: $10,000/tháng.
- Thời gian: 60 ngày.
- Phạm vi: 3 luật sư (1 senior + 2 junior).

### 9. Ranh giới rủi ro

- AI bỏ sót điều khoản nguy hiểm → khách hàng chịu rủi ro pháp lý lớn.
- AI flag nhầm quá nhiều → luật sư mất thời gian filter.
- Data leak hợp đồng → vi phạm attorney-client privilege.

---

## Brief #5 — AI Sales Email Generator

> **Domain**: E-commerce B2B sales
> **Pilot type**: AI draft personalized email, SDR review trước khi gửi

### 1. Bối cảnh doanh nghiệp

Công ty e-commerce nền tảng B2B, có 5,000 lead mới mỗi tuần. Đội SDR (Sales Development Rep) 12 người.

### 2. Quy trình hiện tại

SDR đọc thông tin về prospect (LinkedIn + website công ty) → viết email cá nhân hóa → gửi → follow-up nếu chưa reply. Trung bình 25 phút/lead.

### 3. Điểm đau

- Chỉ tiếp cận được 800 lead/tuần (16% coverage) — bỏ lỡ 4,200 lead/tuần.
- Reply rate 4% — không cao vì email cá nhân hóa nông.
- SDR nói "nghiên cứu prospect" mất quá nhiều thời gian so với "thực sự bán hàng".

### 4. Dữ liệu sẵn có

- 80,000 email đã gửi trong 12 tháng + tỉ lệ open/reply/meeting.
- Database 5,000 prospect/tuần với firmographic + tech stack.

### 5. Ràng buộc

- SDR phải review và approve email trước khi gửi (không auto-send).
- Email phải tuân thủ CAN-SPAM + GDPR — không spam cold list không opt-in.
- Phải personalize cụ thể (tên công ty + ngành + pain point) — không phải email mass.

### 6. Quyết định cần đưa ra

VP Sales hỏi: "AI draft email có giúp tăng coverage lên 60% (3,000 lead/tuần) và giữ reply rate ≥ 4%?"

### 7. Chỉ số nền

- Coverage: 800 lead/tuần (16%).
- Reply rate: 4%.
- Meeting booked rate: 0.8%.

### 8. Ngân sách / Thời gian pilot

- Budget: $4,000/tháng.
- Thời gian: 90 ngày.
- Phạm vi: 4 SDR (trong 12).

### 9. Ranh giới rủi ro

- AI viết sai brand voice → khách phản ánh tiêu cực.
- AI bịa thông tin về prospect → mất uy tín.
- Spam complaint tăng → domain bị block, ảnh hưởng toàn đội.

---

## Brief #6 — AI Code Review Assistant

> **Domain**: Fintech engineering
> **Pilot type**: AI pre-review PR, senior engineer approve cuối

### 1. Bối cảnh doanh nghiệp

Công ty fintech, đội kỹ thuật 40 người, phát hành 150 pull request (PR) mỗi ngày. Tuân thủ PCI-DSS + SOC 2.

### 2. Quy trình hiện tại

Engineer mở PR → senior engineer review (security + style + test coverage) → comment → engineer fix → merge. Trung bình 30 phút/PR cho senior, queue chờ trung bình 2 ngày.

### 3. Điểm đau

- Bottleneck review chậm deployment cycle — release chậm 3 ngày so với target.
- 8% bug lọt qua review (phát hiện ở staging hoặc production).
- Senior engineer phải review nhiều PR đơn giản → ít thời gian cho design.

### 4. Dữ liệu sẵn có

- 30,000 PR đã merge + comment + outcome (bug found / clean) trong 2 năm.
- Coding standards nội bộ (50 trang) + security checklist (30 mục).

### 5. Ràng buộc

- Senior engineer LUÔN approve cuối — AI chỉ pre-review.
- Code không được upload ra cloud public (code có thể chứa secret).
- AI phải chạy trong CI pipeline — không được delay merge quá 5 phút.

### 6. Quyết định cần đưa ra

VP Engineering hỏi: "AI pre-review có giảm review queue từ 2 ngày xuống nửa ngày và giữ bug-leak < 5%?"

### 7. Chỉ số nền

- Review queue: 2 ngày.
- Review time: 30 phút/PR.
- Bug leak: 8%.

### 8. Ngân sách / Thời gian pilot

- Budget: $6,000/tháng.
- Thời gian: 90 ngày.
- Phạm vi: 10 engineer (trong 40).

### 9. Ranh giới rủi ro

- AI bỏ sót security vulnerability → rò rỉ dữ liệu fintech, chịu phạt PCI-DSS.
- AI flag false positive → engineer mất thời gian justify.
- Data leak code base → vi phạm IP nội bộ.

---

## Brief #7 — AI Inventory Forecaster

> **Domain**: Retail chain supply chain
> **Pilot type**: AI daily forecast, analyst approve reorder

### 1. Bối cảnh doanh nghiệp

Chuỗi bán lẻ 50 cửa hàng, 500 SKU đang bán. Đội supply chain 5 analyst.

### 2. Quy trình hiện tại

Analyst chạy mô hình Excel (Excel + Moving Average + Seasonality factor) hằng tuần → tạo forecast cho 500 SKU → đề xuất reorder. Trung bình 2 ngày/tuần để generate forecast.

### 3. Điểm đau

- Sai số forecast: 22% (cao đối với chuẩn ngành 8-12%).
- $2 triệu/năm chi phí cho overstock (mua dư) và stockout (thiếu hàng).
- Forecast hằng tuần → không kịp phản ứng với promotion, weather, hoặc sự kiện đặc biệt.

### 4. Dữ liệu sẵn có

- 5 năm sales data cho 500 SKU theo cửa hàng + ngày.
- Promotion calendar + weather data API + holiday calendar.

### 5. Ràng buộc

- Analyst PHẢI approve mọi reorder recommendation — AI chỉ gợi ý.
- Không integrate trực tiếp với ERP (Oracle) — output qua CSV/Excel để analyst kiểm tra.
- Phải explainable — analyst cần biết "vì sao AI gợi ý reorder 200 đơn vị?".

### 6. Quyết định cần đưa ra

Director Supply Chain hỏi: "AI daily forecast cho top 100 SKU có giảm forecast error xuống dưới 12% và giảm $2M chi phí xuống còn $1M?"

### 7. Chỉ số nền

- Forecast error: 22%.
- Annual loss (overstock + stockout): $2,000,000.
- Forecast frequency: weekly (mục tiêu: daily).

### 8. Ngân sách / Thời gian pilot

- Budget: $5,000/tháng.
- Thời gian: 90 ngày.
- Phạm vi: 2 analyst, 100 SKU đầu (Top 100 theo doanh thu).

### 9. Ranh giới rủi ro

- AI underforecast → stockout → mất doanh số.
- AI overforecast → overstock → ôm hàng + waste (đặc biệt FMCG).
- Black box recommendation → analyst không tin → không adopt.

---

## Brief #8 — AI Student Essay Grader

> **Domain**: University grading
> **Pilot type**: AI pre-grade + draft feedback, TA review cuối

### 1. Bối cảnh doanh nghiệp

Đại học công lập, 3,000 bài luận/học kỳ trên 15 môn học khác nhau. Đội TA (Teaching Assistant): 20 người, sinh viên grad school làm partner-time.

### 2. Quy trình hiện tại

TA đọc từng bài luận → chấm điểm theo rubric (5 tiêu chí) → viết feedback 5-10 câu → trả bài. Trung bình 20 phút/bài.

### 3. Điểm đau

- Trả bài chậm 2 tuần — sinh viên hỏi tiếp môn sau khi chưa nhận feedback môn trước.
- Sai khác giữa các TA (cùng bài, TA khác chấm khác 1-2 điểm) — sinh viên khiếu nại.
- TA burnout vì grading nặng, ảnh hưởng nghiên cứu luận văn.

### 4. Dữ liệu sẵn có

- 30,000 bài luận đã chấm trong 5 năm + rubric chuẩn từng môn + feedback mẫu.

### 5. Ràng buộc

- TA review từng grade + feedback AI trước khi release cho sinh viên (không auto-publish).
- AI grade chỉ là gợi ý — TA có quyền điều chỉnh.
- Bài luận không được dùng để train model bên thứ ba (FERPA + privacy).

### 6. Quyết định cần đưa ra

Trưởng khoa hỏi: "AI pre-grade có rút thời gian trả bài xuống 3 ngày và giảm sai khác inter-TA xuống dưới 0.5 điểm?"

### 7. Chỉ số nền

- Grading turnaround: 2 tuần.
- TA grading time: 20 phút/bài.
- Inter-TA variance: ~1.5 điểm trên thang 10.

### 8. Ngân sách / Thời gian pilot

- Budget: $2,000/tháng.
- Thời gian: 1 học kỳ (15 tuần).
- Phạm vi: 5 TA, 3 môn học (~600 bài luận).

### 9. Ranh giới rủi ro

- AI bias chấm bài (vd: ngôn ngữ không native English bị chấm thấp) → công bằng học thuật.
- TA quá tin AI → không phát hiện được lỗi AI.
- Sinh viên phản đối "AI chấm bài" → khiếu nại lên ban giám hiệu.

---

## Brief #9 — AI Insurance Claim Processor

> **Domain**: Bảo hiểm phi nhân thọ
> **Pilot type**: AI pre-process document + match policy, adjuster approve

### 1. Bối cảnh doanh nghiệp

Công ty bảo hiểm phi nhân thọ, 1,000 claim/ngày (chủ yếu xe hơi + tài sản). Đội adjuster: 30 người.

### 2. Quy trình hiện tại

Adjuster nhận claim → review document (ảnh + giấy tờ + lời khai) → check policy phù hợp → estimate damage → quyết định payout. Trung bình 45 phút/claim.

### 3. Điểm đau

- Thời gian xử lý claim trung bình 5 ngày — khách phàn nàn.
- 15% claim phải re-review do thiếu thông tin hoặc sai policy match.
- Adjuster mới mất 6 tháng để đạt năng suất chuẩn.

### 4. Dữ liệu sẵn có

- 500,000 claim đã xử lý trong 3 năm + outcome (paid / denied / negotiated).
- 200 policy template + clause mapping nội bộ.

### 5. Ràng buộc

- Adjuster PHẢI approve mọi claim decision — AI chỉ pre-process.
- Tuân thủ regulatory: NAIC (Mỹ) hoặc luật bảo hiểm địa phương.
- Tránh bias trong claim approval (đặc biệt: giới tính, sắc tộc, vùng địa lý).

### 6. Quyết định cần đưa ra

Director Claims hỏi: "AI pre-process có rút thời gian từ 5 ngày xuống 1.5 ngày và giảm re-review xuống dưới 5%?"

### 7. Chỉ số nền

- Processing time: 5 ngày/claim.
- Adjuster effort: 45 phút/claim.
- Re-review rate: 15%.

### 8. Ngân sách / Thời gian pilot

- Budget: $12,000/tháng.
- Thời gian: 90 ngày.
- Phạm vi: 8 adjuster (trong 30).

### 9. Ranh giới rủi ro

- AI match sai policy → payout sai → fraud hoặc loss cho công ty.
- AI bias → khách bị từ chối oan → kiện tụng + regulatory penalty.
- Data leak claim documents → vi phạm PII của khách.

---

## Brief #10 — AI Real Estate Listing Generator

> **Domain**: Đại lý bất động sản
> **Pilot type**: AI generate listing description + caption, agent review

### 1. Bối cảnh doanh nghiệp

Đại lý bất động sản, 25 agent, đăng 200 listing mới mỗi tháng (nhà ở + thương mại).

### 2. Quy trình hiện tại

Agent đến xem nhà → chụp 20-30 ảnh → viết description (300-500 từ) → caption từng ảnh → đăng lên portal (MLS / công ty). Trung bình 90 phút/listing chỉ cho phần content.

### 3. Điểm đau

- Listing chất lượng không đều — agent kinh nghiệm viết tốt, agent mới viết kém.
- 40% listing phải manager edit lại trước khi public — chậm time-to-market.
- Agent than phiền writing chiếm quá nhiều thời gian, ít gặp khách.

### 4. Dữ liệu sẵn có

- 8,000 listing đã đăng trong 4 năm + engagement metrics (view, save, contact).
- Property data: diện tích, năm xây, tiện ích, location, comparables.

### 5. Ràng buộc

- Agent review + edit mọi content trước khi đăng — không auto-publish.
- Tuân thủ Fair Housing Act (Mỹ) hoặc tương đương — tránh discrimination trong language.
- Description phải có yếu tố cá nhân hóa cho từng property (không generic template).

### 6. Quyết định cần đưa ra

Broker-owner hỏi: "AI generate description + caption có rút thời gian xuống 30 phút/listing và giảm manager edit rate xuống dưới 15%?"

### 7. Chỉ số nền

- Content time: 90 phút/listing.
- Manager edit rate: 40%.
- Engagement (view trong tuần đầu): trung bình 250 view.

### 8. Ngân sách / Thời gian pilot

- Budget: $3,000/tháng.
- Thời gian: 60 ngày.
- Phạm vi: 8 agent (trong 25).

### 9. Ranh giới rủi ro

- AI bịa thông tin property (vd: thêm tiện ích không có) → khách kiện tụng.
- Language discriminatory (vd: gợi ý "khu yên tĩnh, ít người da màu") → vi phạm Fair Housing.
- Generic content → engagement thấp → agent từ bỏ tool.

---

## Cách giảng viên phân brief

- Brief #1 — pair đông kinh nghiệm B2B SaaS (làm benchmark vì có worked example).
- Brief #2 — pair có interest về T&S / moderation.
- Brief #3 — pair có background y tế / healthtech.
- Brief #4 — pair có legaltech / compliance interest.
- Brief #5 — pair có background bán hàng / marketing.
- Brief #6 — pair là developer / có engineering background.
- Brief #7 — pair quan tâm operations / supply chain.
- Brief #8 — pair có background giáo dục / academic.
- Brief #9 — pair có domain bảo hiểm / fintech.
- Brief #10 — pair có background BĐS / marketing.

Mỗi brief đều có thể stretch để áp dụng common framework — domain expertise chỉ là bonus, không bắt buộc.

---

## Ghi chú cho học viên

- Brief là **fixed input** — không tự ý thay đổi con số trong brief.
- Nếu thấy số liệu trong brief không khớp với assumption ngành (vd: SDR thực tế làm 35 phút/lead chứ không 25), được phép ghi chú trong worksheet "Brief nói X, nhưng ngành thực tế là Y; nhóm dùng X cho consistency."
- Mọi giả định mới (vd: model nào dùng, adoption rate bao nhiêu) phải tự thêm vào worksheet và justify.
