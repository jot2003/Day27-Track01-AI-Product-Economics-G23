# Prompt tham khảo 5 — Tính Value Formula (Monthly Value)

**Dùng khi**: nhóm đã có pricing model + cost, cần tính Monthly Value cụ thể (giá trị tháng AI mang lại) → input cho ROI.
**Công cụ gợi ý**: Claude Sonnet/Opus, ChatGPT-4o.
**Lưu kết quả vào**: Section C.1-C.5 trong `worksheet/02-pricing-value/3-FINAL-pricing-value-roi.md`
**Thời gian**: 15 phút

---

## Trước khi vào prompt — 5 câu hỏi nhóm tự trả lời

1. **Original task time** (không AI): bao nhiêu phút/đơn vị work? (Từ brief field #2).
2. **NET time saved** = Gross − wait − review − switch − rework. Đã estimate từng phần chưa?
3. **Loaded hourly rate**: $___/hr (base × 1.3-1.5).
4. **Adoption rate**: realistic? (60-85% mandatory tool / 30-60% optional / 20-50% new behavior / 50-80% pilot incentive).
5. **Quality factor**: realistic? (80-95% classify / 60-80% draft / 70-85% summarize / 50-70% creative / 40-65% complex).

> **Cảnh báo**: 90% nhóm overestimate Value vì dùng GROSS thay vì NET, hoặc giả adoption 100% / quality 95%. Đây là sai lầm khiến ROI quá đẹp ở base case.

---

## Prompt chính (paste sau pricing model output)

```text
Bạn là Product Manager AI tính ROI cho AI products.
Dựa trên BỐI CẢNH ở trên (brief + cost model + pricing model),
giúp nhóm tôi tính MONTHLY VALUE realistic — không overestimate.

YÊU CẦU:

PHẦN 1 — Time Saved Breakdown:
Tính NET time saved/task (không phải Gross):

| Component | Phút | Lý do |
|---|---|---|
| Original task time (no AI) | ___ | Từ brief field #2 |
| − AI processing wait | ___ | Latency Claude/GPT call (typical 5-30s = 0.1-0.5 min) |
| − Human review time | ___ | Nếu brief có review constraint (typical 1-5 min per task) |
| − Context switching | ___ | User mở tab AI tool, copy/paste back (typical 0.5-1 min) |
| − Rework time (avg) | ___ | Khi quality fail, time fix (= rework × quality miss rate) |
| **= NET time saved** | ___ | sum |

CẢNH BÁO:
- NET typical = 40-60% of Gross. Nếu nhóm tôi tính NET > 80% Gross → đã quên overhead nào đó.
- Đừng bỏ qua context switching — đây là cost ẩn quan trọng.

PHẦN 2 — Loaded Hourly Rate:
Tính rate đầy đủ:
- Base hourly: $___/hr (lương cơ bản, từ brief hoặc industry benchmark)
- Multiplier: × 1.3-1.5 (benefit + tax + overhead + office)
- = Loaded hourly: $___/hr

Brief có cho lương cụ thể không? Nếu không, dùng:
- US: support agent $20-30/hr, lawyer $80-150/hr, nurse $40-60/hr.
- VN: support agent $5-10/hr, lawyer $30-50/hr, nurse $15-25/hr.

PHẦN 3 — Adoption Rate Justification:
Realistic adoption cho brief tôi:
- Range typical: ___% (xem benchmark)
- Brief context: brief có mandatory không? Có incentive không?
- Adoption tháng 1 (initial): ___%
- Adoption tháng 3 (stable): ___%
- Adoption pilot average: ___%

Recommend % với 1-2 câu justification.

PHẦN 4 — Quality Factor Justification:
Realistic quality cho task type:
- Task type: classify / draft / summarize / creative / complex (chọn 1)
- Range typical: ___%
- Brief context: dữ liệu sẵn có (50K ticket history → tốt cho draft), KB outdated (xấu cho draft), domain narrow (xấu vì model chưa fine-tuned)
- Realistic estimate cho brief tôi: ___%

PHẦN 5 — Monthly Value Formula:
Tính step-by-step:

Step 1: Gross Monthly Value
= Monthly volume × NET time saved (min) × (Loaded hourly / 60)
= ___ × ___ × ($___ / 60)
= $___

Step 2: Adjusted for adoption + quality
= Gross × Adoption × Quality
= $___ × ___% × ___%
= $___

Step 3: Minus rework cost (nếu rework time chưa trừ trong NET)
− $___

= NET Monthly Value: $___

PHẦN 6 — Sensitivity Note:
Nếu adoption thay đổi ±20%, NET Value thay đổi bao nhiêu?
Nếu quality thay đổi ±20%, NET Value thay đổi bao nhiêu?

Identify variable nào nhạy nhất với NET Value — đó là metric cần track chặt nhất.

YÊU CẦU FORMAT:
- Mỗi số có công thức rõ.
- Mỗi % có justification 1-2 câu.
- Trả lời tiếng Việt thoát nghĩa.

YÊU CẦU PHẢN BIỆN:
- NET time saved có > 80% Gross không? (Nếu có → check lại overhead).
- Adoption > 80%? (Cần data hard support).
- Quality > 85%? (Cần POC data).
- Có double-count: rework đã trừ trong NET rồi mà còn trừ trong Step 3?
```

---

## Iterate — đẩy AI sâu hơn nếu output chưa đủ

### Khi nhóm muốn challenge mức adoption

```text
Nhóm tôi đặt adoption = 70% cho pilot. Justify:

Hỏi 5 câu:
1. Pilot có mandatory không (mgmt push) hay voluntary?
2. User có experience với AI tool trước không?
3. UX của AI có integrate sẵn với workflow (vd: trong Zendesk) hay phải mở tab khác?
4. Có incentive (vd: free credits, bonus cho user adopt) không?
5. Có training session không? Số session?

Dựa trên trả lời, adoption realistic là:
- Voluntary + no UX integration + no incentive → 20-40%.
- Voluntary + UX integrated + light incentive → 40-60%.
- Mandatory + UX integrated + training → 60-85%.

70% nhóm tôi đặt thuộc tier 3 — cần justify mandatory + UX + training cụ thể trong brief.
```

### Khi muốn benchmark quality realistic

```text
Quality nhóm tôi đặt = 80%. Validate qua benchmark:

Task type: [draft generation cho support reply].

Benchmark:
- Anthropic Claude 3.5 trên domain general: 75-85% (theo eval public).
- Anthropic Claude 3.5 fine-tuned trên domain support: 85-92%.
- Brief tôi: dùng base Claude 3.5 + RAG vector search → expect 70-82% (vì KB outdated 30%).

Adjust quality cho brief tôi:
- Initial month 1: 70% (RAG context chưa optimize).
- Stable month 3: 80% (sau prompt iteration).
- Pilot average: 75%.

Nhóm tôi nên dùng 75% thay vì 80% — bảo thủ hơn, realistic hơn.
```

### Khi NET time saved > 80% Gross (suspicious)

```text
Nhóm tôi tính NET = 10 min, Gross = 12 min → NET/Gross = 83%.

Suspicious vì typical 40-60%. Re-check:

1. Human review time đã trừ chưa?
   - Nếu brief có "agent review trước khi send" → review thường 2-4 min.
2. Context switching đã trừ chưa?
   - Agent phải mở Zendesk → mở AI tool → copy back? Hay AI tích hợp inline?
3. Rework đã trừ chưa?
   - Quality 80% → 20% drafts không dùng được, agent phải viết tay → time fix.

Re-calculate NET với 3 overhead trên:
- Gross: 12 min (search KB 5 + draft 4 + send 3).
- AI saves: search 5 + draft 4 = 9 min potential.
- Wait AI: 0.3 min.
- Review draft: 2 min (agent đọc + edit nhẹ).
- Switch: 0.3 min (AI tích hợp inline, nhẹ).
- Rework: 0.5 min average (= 2 min fix × 20% miss rate / 80% used rate).

NET = 9 − 0.3 − 2 − 0.3 − 0.5 = 5.9 min.
NET/Gross = 5.9/12 = 49%. Match benchmark 40-60% ✓.
```

---

## Phản biện sau khi có output — 5 câu nhóm tự hỏi

1. **NET vs Gross check**: NET có rơi vào 40-60% Gross không?
2. **Adoption realistic**: < 80% không có data hard?
3. **Quality realistic**: < 85% không có POC data?
4. **Justification check**: mỗi % có 1-2 câu lý do?
5. **Double-count check**: rework có double-count giữa NET và Step 3?

---

## Ví dụ tốt vs ví dụ chưa tốt

### Chưa tốt

> "Monthly Value: $5,000. Adoption 90%, quality 95%, gross saving 10 min/task."

Vấn đề: adoption + quality quá lạc quan, không justify, không có công thức.

### Tốt

> **Brief #1 — Monthly Value Calculation**
>
> **Time Saved Breakdown**:
> | Component | Phút | Lý do |
> |---|---|---|
> | Original task time | 12 | Brief field #7 |
> | − AI wait | − 0.3 | Claude 3.5 latency ~20s = 0.3 min |
> | − Review draft | − 3 | Brief constraint: agent senior review (typical 2-4 min) |
> | − Context switch | − 0.5 | Zendesk side panel inline, nhẹ |
> | − Rework | − 0.6 | 3 min fix × 20% miss rate = 0.6 min average |
> | **NET saved** | **7.6** | 12 − 0.3 − 3 − 0.5 − 0.6 = 7.6 min |
>
> NET/Gross = 7.6 / 12 = 63% — slightly upper bound of 40-60% (justify: AI tích hợp inline Zendesk → switch cost thấp).
>
> **Loaded Rate**: $20 base × 1.25 multiplier = **$25/hr**.
>
> **Adoption**: 65%. Pilot 5 agent. Mandatory: medium (encouraged, không bắt buộc). UX: tích hợp Zendesk. Training: 1 session. Range 60-85% mandatory → 65% bảo thủ.
>
> **Quality**: 80%. Task: draft generation. Range 60-80% draft. Brief có 50K ticket history + RAG → upper bound 80%. Justify: KB outdated 30% có thể drop quality về 75% ở month 1.
>
> **Monthly Value Formula**:
>
> Gross: 3,520 task × 7.6 min × ($25 / 60) = **$11,147/month**.
>
> Adjusted: $11,147 × 65% × 80% = **$5,797/month**.
>
> Rework already in NET (đã trừ 0.6 min) → không trừ lần 2.
>
> NET Monthly Value: **$5,797/month**.

---

## Anti-pattern khi prompt — tránh

| Đừng làm | Nên làm |
|---|---|
| Adoption 100% | Realistic 50-80%, justify từ context |
| Quality 95% | Realistic theo task type benchmark |
| Dùng Gross time saved | NET = Gross − overhead 4 component |
| Double-count rework | Hoặc trong NET hoặc Step 3, không cả 2 |
| Loaded rate = base | Loaded = base × 1.3-1.5 |
| Bỏ context switching | Mỗi lần đổi tool = thời gian thực |
| Round number ($5,000) | Số chính xác từ công thức ($5,797) |

---

## Format save vào Section C.1-C.5

```markdown
### C.1 — Time Saved per Task
[Paste bảng]

### C.2 — Loaded Hourly Rate
[Paste]

### C.3 — Adoption + Quality
[Paste với justification]

### C.4 — Monthly Volume
[Paste]

### C.5 — Monthly Value Formula
[Paste công thức 3 step + số cụ thể]
```

---

## Câu hỏi mở rộng — nâng cao phản biện (optional)

```text
Sau khi tính Value, giúp tôi suy nghĩ 3 góc:

1. **Hidden value**: AI có tạo giá trị nào KHÔNG phải time saved không?
   - Quality consistent (giảm variance) → defend trong rubric mới.
   - Onboarding ngắn lại (3 tuần → 1 tuần) → onboarding cost saved.
   - 24/7 availability (AI không sleep) → after-hour service.
   - Scale capacity (10× volume mà không hire thêm) → hire deferred.

2. **Time saved vs Value created**: 2 khác nhau:
   - Time saved: agent dùng AI → save 7 min/ticket → AI value = 7 min × rate.
   - Value created: agent dùng time saved làm gì? Đón thêm ticket? Customer succ initiative? Đi café?
   - Nếu time saved chỉ dùng để "đi café" → value không materialize thực sự.

3. **Indirect value**: AI giảm churn (vì CSAT tăng), tăng deal close (vì respond nhanh):
   - Brief field #1 có "support-related churn 18%" → nếu AI giảm churn 2pt → save bao nhiêu LTV?
   - Indirect value có thể > direct time saved value.

Trả lời 3 câu này để hiểu Value đầy đủ — không chỉ "time saved × rate".
```
