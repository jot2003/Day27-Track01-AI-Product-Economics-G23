---
artifact: 1 — Attribution × Autonomy positioning
buoc: 2 — Pricing/Access + Value/ROI
phase: Đặt vị trí trên ma trận 2×2
time: 15 phút (xem deck slide 4 để biết khung giờ chính xác trong buổi)
input: 00-context.md + brief + 01-cost-model/3-FINAL-cost-model.md + prompts/03-attribution-autonomy.md
nop-cuoi: Không — file trung gian
---

# 1 — Attribution × Autonomy: đặt sản phẩm trên ma trận 2×2

Mục tiêu: định vị AI product trên ma trận **Attribution × Autonomy** để xác định pricing model phù hợp tự nhiên.

Lý do làm bước này: pricing model không tự nhiên xuất hiện — nó được quyết định bởi 2 đặc tính của AI (autonomy + attribution). Vị trí trên ma trận → pricing model. Vd: low autonomy + low attribution → seat-based; high autonomy + high attribution → outcome-based.

Quy tắc: **không có vị trí trên ma trận = không có pricing model justify được**.

## Quy trình 15 phút

```text
5 phút  — Trả lời 2 câu hỏi: autonomy + attribution
5 phút  — Vẽ vị trí trên ma trận + chọn quadrant
5 phút  — Validate với real-world analog
```

---

## Phần A — Hiểu 2 trục

### Trục Autonomy (dọc)

**Câu hỏi**: AI tự làm xong việc, hay chỉ hỗ trợ người làm việc đó?

- **Low Autonomy** = AI hỗ trợ, người quyết định cuối.
  - Vd: Grammarly suggest, người chọn accept/reject.
  - Vd: Copilot draft code, dev chỉnh sửa và commit.
  - Vd: Support copilot suggest reply, agent edit và send.

- **High Autonomy** = AI làm xong xuôi, người review sau (hoặc không review).
  - Vd: OpenAI API auto-classify content.
  - Vd: Intercom Fin auto-reply user.
  - Vd: AWS Auto Scaling tự quyết scaling.

### Trục Attribution (ngang)

**Câu hỏi**: Có thể nói rõ AI tạo ra giá trị cụ thể nào không?

- **Low Attribution** = khó tách phần đóng góp của AI khỏi phần của team.
  - Vd: AI giúp team viết tài liệu nhanh hơn — kết quả là "team viết tốt" chứ không "AI viết tốt".
  - Vd: Slack AI hỗ trợ communication — khó nói "AI gây ra deal close".

- **High Attribution** = thấy rõ AI là cause của outcome.
  - Vd: Intercom Fin resolve 1 ticket → rõ AI giải quyết.
  - Vd: Chargeflow win 1 chargeback dispute → rõ AI thắng.
  - Vd: DALL-E sinh 1 ảnh → rõ AI tạo.

---

## Phần B — Trả lời 2 câu hỏi cho brief của nhóm

### Câu hỏi 1: Autonomy

**Brief của nhóm thuộc Low hay High Autonomy?**

- AI làm gì độc lập? [...]
- Người làm gì cuối cùng? [...]
- Có ràng buộc "100% human review" không? [Có → Low Autonomy]
- AI tự gửi cho khách / push thay đổi production không? [Có → High Autonomy]

**Kết luận Autonomy**: [Low / High]

**Justification**: [1-2 câu giải thích vì sao]

### Câu hỏi 2: Attribution

**Brief của nhóm thuộc Low hay High Attribution?**

- Nếu AI resolve 1 unit (1 ticket / 1 flag / 1 contract), có thể attribute hoàn toàn cho AI không? [Có → High]
- Hay AI chỉ là 1 phần trong workflow, khó tách phần đóng góp? [→ Low]
- Khách hàng có "thấy" rõ AI tạo giá trị không?

**Kết luận Attribution**: [Low / High]

**Justification**: [1-2 câu]

---

## Phần C — Đặt vị trí trên ma trận

```text
                Low Attribution        High Attribution

Low Autonomy    Seat / Flat            Hybrid (seat + credits)
(human          Grammarly base         Cursor $20+credits
controls)       Slack AI               Canva $15+500 credits
                                       Clay $149-$800 tiers

High Autonomy   Usage-based            Outcome-based
(AI acts)       OpenAI API             Intercom Fin $0.99/res
                AWS AI services        Chargeflow per dispute
                Pinecone               Zendesk $1.50/resolution
```

**Vị trí của brief nhóm**:

- Autonomy: ___
- Attribution: ___
- → Quadrant: ___

**Pricing model TỰ NHIÊN** (theo ma trận): ___

---

## Phần D — Validate với real-world analog

Tìm 1 sản phẩm thật trong quadrant nhóm chọn để validate vị trí:

| Sản phẩm tương tự | Quadrant của họ | Pricing model | Note |
|---|---|---|---|
| [...] | Low/High Auto + Low/High Attrib | [Seat / Usage / Hybrid / Outcome] | [...] |

**Câu hỏi validate**:

- Sản phẩm này có giống brief của nhóm không (cùng quadrant)?
- Họ pricing theo cách nào? Có hợp với economics nhóm tính ra ở Section A không?

Ví dụ analog:

- Brief #1 (Support Copilot, low autonomy + medium attribution) → analog: Cursor, GitHub Copilot ($20-$30/seat + tiered credit).
- Brief #2 (Content Moderator, high autonomy + low attribution, vì còn 100% review) → analog: AWS Rekognition (usage-based).
- Brief #3 (Medical Triage, low autonomy + medium attribution) → analog: Epic AI in EHR (seat-based, bundle với EHR license).
- Brief #4 (Legal Contract Reviewer, low autonomy + high attribution per flagged clause) → analog: Harvey AI, Kira (seat + tiered).
- Brief #5 (Sales Email Generator, low autonomy + medium attribution) → analog: Clay, Lavender, Apollo.io.
- Brief #6 (Code Review Assistant, low autonomy + high attribution per PR) → analog: Codium AI, Sourcegraph Cody.
- Brief #7 (Inventory Forecaster, low autonomy + high attribution per forecast) → analog: Blue Yonder, o9.
- Brief #8 (Essay Grader, low autonomy + high attribution per grade) → analog: GradeScope AI, Turnitin.
- Brief #9 (Claim Processor, low autonomy + high attribution per claim) → analog: Tractable, Lemonade AI.
- Brief #10 (Listing Generator, low autonomy + high attribution per listing) → analog: HouseSigma AI, ListingDojo.

---

## Phần E — Edge case: brief nằm "giữa"

Một số brief khó dứt khoát Low/High. Trong trường hợp đó:

- **Brief có autonomy "medium"** (vd: AI làm draft nhưng cần human review cho 80% case) → coi là Low Autonomy nếu human review là constraint cứng.
- **Brief có attribution "medium"** (vd: AI flag clause, nhưng lawyer là người quyết định final issue list) → vẫn coi là High Attribution vì AI có output rõ ràng cho 1 contract.

Nếu brief nhóm rơi vào "medium" → chọn hướng nghiêng theo nhận định:

- "Low Autonomy + Medium Attribution → Hybrid leaning Seat" (Cursor style: $20 base + credit).
- "Low Autonomy + High Attribution → Hybrid (Seat + Outcome credit)" (Clay style: tier dựa trên outcome volume).

---

## Phần F — Kiểm tra

Trước khi chuyển sang `2-pricing-model-choice.md`, rà soát:

- [ ] Đã trả lời rõ Low/High cho Autonomy với justification.
- [ ] Đã trả lời rõ Low/High cho Attribution với justification.
- [ ] Vị trí quadrant rõ ràng (không "ở giữa cả 4 quadrant").
- [ ] Pricing model tự nhiên theo ma trận đã ghi.
- [ ] Có 1 real-world analog cùng quadrant để validate.

---

## Câu hỏi mở (cho `2-pricing-model-choice.md`)

- Câu hỏi 1: Pricing model tự nhiên có phù hợp với buyer (CTO của brief) hay không?
- Câu hỏi 2: Có Usage Anxiety rủi ro không (nếu chọn Usage-based)?
- Câu hỏi 3: [...]

Sau bước này, chuyển sang `2-pricing-model-choice.md` để chốt pricing model + value metric.
