# Prompt tham khảo 1 — Tự định nghĩa Usage Unit

**Dùng khi**: nhóm bắt đầu Step 1 Lab, cần định nghĩa "AI làm GÌ trong MỘT lần chạy" từ brief — nền tảng cho toàn bộ Cost Model.
**Công cụ gợi ý**: Claude Sonnet/Opus, ChatGPT-4o, Gemini 1.5 Pro.
**Lưu kết quả vào**: `worksheet/01-cost-model/1-usage-unit.md` Phần A + C
**Thời gian**: 10-15 phút

---

## Trước khi vào prompt — 5 câu hỏi nhóm tự trả lời

Mục tiêu: trước khi nhờ AI, nhóm phải biết **mục đích cụ thể của usage unit** — không phải đặt 1 cái tên kêu mà phải link với cost + value.

1. **Brief # bao nhiêu** và domain là gì? (Trừ Brief #1 đã có ví dụ Support Copilot, các brief khác phải tự suy ra.)
2. **Workflow chính của brief** (đọc lại field #2): từ input đến output, AI chen vào khâu nào?
3. **Primary constraint** (đọc lại field #5): có bắt buộc 100% human review không? Có cấm auto-action không?
4. **AI thay vai trò ai**: tự làm việc của human (high autonomy), hay hỗ trợ human (low autonomy)?
5. **Output cuối của AI nhìn như thế nào**: là 1 label / 1 đoạn text / 1 quyết định / 1 bộ data?

> **Cảnh báo**: nếu nhóm chưa trả lời 5 câu này → AI sẽ đưa usage unit "kêu nhưng vô dụng" (vd: "AI capacity"). Đầu vào tệ → đầu ra tệ.

---

## Prompt chính (paste sau `00-context.md`)

```text
Bạn là Product Manager AI có kinh nghiệm tính economics cho AI products.
Dựa trên BỐI CẢNH ở trên (00-context.md + brief đã giao), giúp nhóm tôi định nghĩa
USAGE UNIT cho AI product trong brief.

Usage unit = đơn vị nguyên tử kinh tế của AI product = "AI làm GÌ trong MỘT lần chạy".

YÊU CẦU:

1. Đề xuất 3 usage unit candidate cho brief, mỗi cái có:
   - Tên ngắn (vd: "1 ticket reply draft", "1 content flag pre-screen")
   - Mô tả 2-3 câu (input là gì, output là gì, output đi đâu)
   - Trigger (khi nào AI chạy: auto / manual / scheduled)
   - Pass 3-part test:
     a. Đếm được? (countable, không phải "AI hỗ trợ")
     b. Tốn token? (mỗi lần = 1 API call có cost)
     c. Có giá trị cho user? (1 đơn vị này có rút thời gian / cải thiện chất lượng?)

2. Đánh giá 3 candidate theo 4 tiêu chí (1-5):
   - Atomic-ness (đủ atomic không?)
   - Countable (dễ đếm trong production không?)
   - Cost-linked (rõ ràng cost mỗi unit không?)
   - Value-linked (link rõ với giá trị user không?)

3. Recommend usage unit nào pick + lý do (2-3 câu).

4. Cảnh báo các common mistake cho brief này:
   - Quá rộng (vd: "AI hỗ trợ X")
   - Quá hẹp (vd: "1 token")
   - Không atomic (1 unit gọi AI nhiều lần)
   - Đúng technical, sai business (vd: "1 API call")

YÊU CẦU PHẢN BIỆN:
- Nếu brief có constraint 100% human review → usage unit có phải là "1 lần AI chạy" hay "1 lần AI + human review combined"?
- Nếu brief có multi-step workflow (vd: search + draft + refine = 3 AI call) → đếm 1 unit hay 3 unit?
- Nếu user có thể "regen" / "try again" → đếm 1 lần thử hay 1 outcome cuối?

YÊU CẦU FORMAT:
- Trả lời bằng tiếng Việt thoát nghĩa, không dịch nửa vời.
- Mỗi candidate trình bày trong format đồng nhất.
- Recommendation cuối ngắn gọn 2-3 câu.
```

---

## Iterate — đẩy AI sâu hơn nếu output chưa đủ

### Khi AI đề xuất usage unit quá rộng

Nếu AI trả lời "1 ticket handled" — quá rộng vì 1 ticket có thể qua nhiều AI call (search KB, draft, refine).

```text
Usage unit bạn đề xuất ("1 ticket handled") là OUTCOME, không phải ATOMIC AI call.

Trong workflow:
- Bước 1: AI search KB (1 API call)
- Bước 2: AI draft reply (1 API call)
- Bước 3: AI refine sau agent feedback (0 hoặc 1 API call)

Tách lại: usage unit nên là 1 trong 3 bước trên, hay là "1 ticket reply draft" (= bước 2 — bước có giá trị rõ nhất với user)?

Phân tích thêm: nếu chọn "1 ticket reply draft" thì bước 1 (search KB) tính vào đâu?
- Option A: include trong cost/task của bước 2 (multi-step cost).
- Option B: tách riêng "1 KB search" = usage unit phụ.

Recommend cái nào dễ measure + bill hơn trong thực tế?
```

### Khi AI đề xuất usage unit quá technical

Nếu AI trả lời "1 token consumed" hoặc "1 model inference" — đúng technical, sai business.

```text
Usage unit bạn đề xuất là technical-level, không tied với business value.

Vấn đề:
- Buyer (CTO/VP) không hiểu "1 inference" nghĩa là gì.
- User không trả tiền theo "inference count" — họ trả tiền theo outcome.

Đề xuất lại usage unit ở MIDDLE LAYER:
- KHÔNG quá technical (như "1 token")
- KHÔNG quá broad (như "1 ticket handled")
- Ở giữa: "1 unit of AI work mà buyer sẽ pay for" — vd: 1 draft, 1 flag pre-screen, 1 forecast, 1 contract review.

Tìm middle layer cho brief này, đề xuất 2 candidate cụ thể.
```

### Khi muốn validate qua real-world analog

```text
Tìm 2 sản phẩm AI tương tự (cùng domain hoặc cùng pattern) và xem họ define usage unit thế nào:

1. Sản phẩm: ___
   - Họ bill theo usage unit gì?
   - Pricing page URL: [...]
   - Có giống usage unit nhóm tôi đề xuất không?

2. Sản phẩm: ___
   - [tương tự]

Sau khi tham khảo, có nên revise usage unit cho brief tôi không?
```

---

## Phản biện sau khi có output — 5 câu nhóm tự hỏi

Trước khi paste vào `1-usage-unit.md`, nhóm rà soát:

1. **3-part test check**: usage unit pass cả 3? (countable, costs tokens, has value)
2. **Atomic check**: usage unit có thực sự là "1 lần AI chạy" hay là 1 outcome multi-call?
3. **Cost-linked check**: từ usage unit có dễ tính cost/task không?
4. **Value-linked check**: từ usage unit có dễ tính value/task không?
5. **Buyer view check**: buyer (CTO/VP) hiểu được usage unit này không, có defendable không?

---

## Ví dụ tốt vs ví dụ chưa tốt

### Chưa tốt

> "Usage unit: AI hỗ trợ agent."

Vấn đề: không atomic, không đếm được, không tied với cost.

> "Usage unit: 1 token tiêu thụ."

Vấn đề: quá technical, không tied với business value.

> "Usage unit: 1 ticket được giải quyết."

Vấn đề: là outcome multi-step, không phải atomic AI call.

### Tốt

> **Usage unit: 1 ticket reply draft**
>
> - **Mô tả**: AI nhận nội dung ticket + 3 KB articles liên quan (vector search trước đó), sinh ra 1 bản nháp trả lời dài 80-200 từ. Bản nháp hiển thị trong Zendesk side panel để agent edit/copy/send.
> - **Trigger**: agent click "Draft with AI" → AI chạy 1 lần. Không auto trigger.
> - **3-part test**:
>   - ✓ Đếm được: count số lần click "Draft" trong logs.
>   - ✓ Tốn token: input ~800 (ticket + KB) + output ~400 (draft) = ~1,200 tokens/call.
>   - ✓ Có giá trị: tiết kiệm 5 phút search KB + 4 phút viết = 9 phút saved (gross).
>
> **Recommendation**: chọn unit này vì atomic + measurable + maps to value cho agent.

---

## Anti-pattern khi prompt — tránh

| Đừng làm | Nên làm |
|---|---|
| Hỏi AI "Usage unit là gì cho brief tôi" | Đưa brief context + ràng buộc 3-part test |
| Chấp nhận usage unit đầu AI đưa | Đẩy AI đề xuất 3 candidates, so sánh |
| Bỏ qua phần phản biện | Chạy 3 câu phản biện (constraint review / multi-step / regen) |
| Không validate với real-world | Tìm 2 analog sản phẩm để cross-check |
| Quên buyer perspective | Buyer (CTO/VP) có defendable không? |

---

## Format save vào `1-usage-unit.md`

```markdown
## Phần A — Đề xuất Usage Unit

(Đã có đề xuất 1 + 2 từ thành viên cá nhân — bổ sung từ AI nếu cần)

**Usage unit cặp CHỌN**: ___
**Lý do chọn**: ___

## Phần C — Mô tả chi tiết Usage Unit

(Paste mô tả + trigger + input + output từ AI output)
```

---

## Câu hỏi mở rộng — nâng cao phản biện (optional)

```text
Sau khi chọn usage unit, giúp tôi suy nghĩ 3 câu hỏi STRESS:

1. Nếu brief tăng scope 10× (vd: 5 agent → 50 agent), usage unit này có scale được không?
   - Volume × 10 có gây issue gì (vd: rate limit API, vector DB throughput)?

2. Nếu provider deprecate model hiện tại, usage unit có cần redefine không?
   - Vd: model mới có context window khác → token estimate khác → unit cost khác.

3. Nếu compliance change (vd: bắt buộc on-premise), usage unit có khả thi không?
   - On-premise model thường có cost structure khác (GPU hourly thay vì per-token).

Đặt 3 câu này giúp nhóm test usage unit dưới các kịch bản dài hạn — quan trọng cho verdict CONDITIONAL/NO-GO.
```

3 câu hỏi này giúp nhóm nhìn usage unit **không chỉ ở pilot scale** — buyer thực tế sẽ hỏi về scale + deprecate + compliance.
