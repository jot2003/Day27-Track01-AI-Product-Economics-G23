# Glossary — Day 27 (AI Product Economics)

Bảng thuật ngữ Day 27. Mỗi thuật ngữ có dạng tiếng Anh (giữ nguyên) + dịch tiếng Việt mượt + ví dụ ngắn.

Cách dùng: tham chiếu khi đọc skeleton / prompt / worksheet. Một số thuật ngữ học viên đã quen từ Day 25-26, một số mới ở Day 27.

---

## Khái niệm cốt lõi

| Thuật ngữ | Nghĩa | Ví dụ trong Day 27 |
|---|---|---|
| **Usage Unit** | Đơn vị nguyên tử kinh tế của AI product — "AI làm GÌ trong MỘT lần chạy". Cần pass 3-part test: đếm được, tốn token, có giá trị user. | "1 ticket reply draft" cho Brief #1, "1 content flag pre-screen" cho Brief #2 |
| **Cost-Capability-Speed Triangle** | Tam giác đánh đổi 3 chiều: rẻ / mạnh / nhanh. Mỗi quyết định AI product nằm trong tam giác này — tối ưu 2 thì hy sinh 1. | GitHub Copilot tiered: speed model cho autocomplete, capable model cho chat |
| **Monetization Triad** | 3 trục cần align cho AI monetization: Customer Value + Growth Loop + Cost of Revenue. Pricing model phải khớp với 3 trục. | Intercom Fin align 3 trục: per-resolution = clear value + adoption loop + variable cost match revenue |
| **Value Metric Spectrum** | Phổ value metric từ trừu tượng đến cụ thể: Seat → Usage → Outcome → Hybrid. Mỗi điểm trong phổ có ưu/nhược. | Grammarly seat (trừu tượng), OpenAI API usage (concrete), Intercom Fin outcome (concrete + tied to value) |
| **Attribution × Autonomy Matrix** | Ma trận 2×2 quyết định pricing model phù hợp: Autonomy (AI tự làm / hỗ trợ) × Attribution (AI là cause rõ / mờ). | Low Auto + Low Attrib → Seat (Grammarly); High Auto + High Attrib → Outcome (Intercom Fin) |

## Pricing models

| Thuật ngữ | Nghĩa | Ví dụ |
|---|---|---|
| **Seat / Flat pricing** | $X cố định / user / tháng. Predictable. Phù hợp Low Autonomy + Low Attribution. | Grammarly $12/seat, Slack AI $7/seat, ChatGPT Team $25/seat |
| **Usage-based pricing** | $X / unit volume (per token, per call, per request). Variable. Phù hợp High Autonomy + Low Attribution. | OpenAI API $3/1M input tokens, AWS pay-per-call, Pinecone per-query |
| **Outcome-based pricing** | $X / outcome thực tế (per ticket resolved, per dispute won). Phù hợp High Autonomy + High Attribution. | Intercom Fin $0.99/resolution, Chargeflow per chargeback won, Zendesk $1.50/resolution |
| **CAMP test** | 4 chuẩn để outcome-based pricing khả thi: **C**ountable (đếm được), **A**ligned (cùng hướng với khách + nhà cung cấp), **M**eaningful (có ý nghĩa với buyer), **P**redictable (dự báo được volume). Fail 1 trong 4 → outcome-based không bán được. | "1 resolution" pass CAMP; "1 conversation" fail Meaningful (buyer không quan tâm số lượt chat) |
| **Hybrid pricing** | Mix Seat base + Usage credits, hoặc Tier outcome. Phù hợp medium autonomy + attribution. | Cursor $20/seat + AI credits, Canva $15/seat + 500 credits, Clay $149/$349/$800 tier |
| **Pay-for-output** | Pricing dựa trên kết quả AI tạo ra. Một dạng outcome-based. | Intercom Fin $0.99/resolution (pay for resolved ticket) |
| **Value metric** | Đơn vị khách hàng trả tiền cho. Phải countable + meaningful to buyer + tied to AI value. | "1 ticket resolved" (Intercom), "1 lawyer seat" (Harvey), "1 image generated" (DALL-E) |
| **Usage Anxiety** | User self-limit usage vì sợ bill tăng → AI không được dùng thật → value bị suppress. Risk chính của Usage-based + Hybrid. | Cursor credit alert làm user ngại dùng → AI value drop |

## Cost components

| Thuật ngữ | Nghĩa | Ví dụ |
|---|---|---|
| **Cost per task** | Chi phí 1 lần AI chạy = (input tokens × input price + output tokens × output price) / 1M. | Claude 3.5 Sonnet: 800 in × $3 + 400 out × $15 / 1M = $0.0084 |
| **API cost** | Chi phí gọi LLM API (per token / per call). Thường là 1-30% total cost trong pilot. | OpenAI GPT-4o $2.50/1M input, Anthropic Claude 3.5 $3/1M input |
| **Tooling cost** | Chi phí infrastructure ngoài LLM: vector DB, monitoring, orchestration. Thường flat (subscription). | Pinecone $70/mo, Langfuse $50/mo, Helicone $50/mo |
| **Human review cost** | Time × hourly rate cho người review AI output. Thường dominate cost khi brief có 100% review constraint. | 3 min review × $25/hr / 60 = $1.25/review × 1,000 reviews = $1,250/month |
| **Setup cost** | Chi phí 1 lần: integration, security review, prompt engineering, training. Amortize theo pilot duration. | 1 engineer × 2 tuần × $2,000 = $4,000 / 3 tháng pilot = $1,333/month |
| **Loaded hourly rate** | Hourly rate đầy đủ = base salary × 1.3-1.5 (benefit + tax + overhead + office). Dùng chung cho cả cost (review) và value (time saved). | $20/hr base × 1.25 multiplier = $25/hr loaded |
| **Monthly volume** | Số task AI chạy / tháng = Pilot daily volume × 22 working days. | 160 task/ngày × 22 = 3,520 task/month |

## Value components

| Thuật ngữ | Nghĩa | Ví dụ |
|---|---|---|
| **Gross time saved** | Thời gian tiết kiệm raw (chưa trừ overhead). | AI saves search KB 5 min + draft 4 min = 9 min gross |
| **NET time saved** | Thời gian tiết kiệm thực tế = Gross − AI wait − human review − context switch − rework. Typical 40-60% of Gross. | 9 min gross − 0.3 wait − 3 review − 0.5 switch − 0.6 rework = 4.6 min NET |
| **Adoption rate** | % user pilot thực sự dùng AI feature. Realistic 50-80% pilot mandatory, 20-50% optional. | 5 agent pilot × 65% adoption = 3.25 agent active = 65% × value potential |
| **Quality factor** | % AI output usable without major rework. Theo task type: 80-95% classify, 60-80% draft, 70-85% summarize, 50-70% creative, 40-65% complex. | Draft generation Claude 3.5: typical 75-85% |
| **Rework cost** | Time fix bad AI outputs khi quality fail. Tăng khi quality giảm. | 20% drafts cần full rewrite × 3 min/rewrite = 0.6 min rework / task average |

## ROI + verdict

| Thuật ngữ | Nghĩa | Ví dụ |
|---|---|---|
| **ROI ratio** | Return on Investment = Monthly Value / Monthly Cost. Số:1 (vd: 2.07:1). | $5,797 value / $2,803 cost = 2.07:1 |
| **Break-even** | Ngưỡng adoption hoặc quality mà ROI = 1:1. Pilot fail nếu dưới ngưỡng. | Break-even adoption: cost / (gross value × quality%) = 31% |
| **Sensitivity analysis** | Bảng ROI khi thay đổi 1-2 biến (adoption, quality, cost). Cho thấy "sweet spot" và "ngưỡng sống chết". | ROI matrix adoption × quality: 4×4 cells, identify ROI > 3:1 cells |

## Stress Test

| Thuật ngữ | Nghĩa | Ví dụ |
|---|---|---|
| **Stress test** | Mô phỏng scenarios xấu để test xem economics có sống không. Khác sensitivity (thay đổi nhỏ) — stress là thay đổi lớn (2-3× hoặc 30-50%). | 5 scenarios: base, heavy, low adopt, quality fail, provider shock |
| **Heavy usage** | Scenario volume tăng nhiều (power user pattern, 20% user dùng 80% capacity). | Volume × 2-3, test cost có blow up nhanh hơn value |
| **Power user pattern** | Một nhóm nhỏ user (10-20%) dùng AI cực kỳ nhiều (có thể 5-100× trung bình), kéo lệch chi phí lên trong khi value không tăng tương ứng. Là nguyên nhân chính khiến Heavy usage scenario phá vỡ kinh tế. | Replit pilot 2024: 20% user dùng 80% capacity → margins âm; Cursor phải áp credit cap |
| **Cost Variance Problem** | Chi phí biến động lớn giữa các user (vì power user kéo lệch), khiến PM khó dự báo budget tháng tới — phương sai cost cao hơn nhiều so với SaaS truyền thống. | Pilot: 5 user, average cost $300/user nhưng range $50-$1,500/user → CFO khó approve scale-up |
| **Low adoption** | Scenario chỉ 30-40% user pilot adopt. | Adoption 65% → 30%, value collapse, cost fixed |
| **Quality failure** | Scenario AI quality drop nhiều (50-60% thay vì 80%). | KB outdated, edge case, model thiếu domain — quality 50% |
| **Provider shock** | Scenario provider đổi giá hoặc deprecate model. | Anthropic deprecate Claude 3.5 → Claude 4 đắt × 3 |
| **Combined worst case** | 2 scenarios xấu nhất xảy ra đồng thời. Test resilience cao nhất. | Low adoption (30%) + Quality fail (50%) → ROI 0.6:1 |
| **"Survives X/5"** | Số scenario (trên 5) mà ROI vẫn ≥ 1.5:1 (ngưỡng marginal). Tiêu chí cho verdict: GO cần survive 4-5/5, CONDITIONAL 2-3/5, NO-GO <2/5. | Base 2.07 + Heavy 2.17 + Provider 1.95 ≥ 1.5 → 3/5 sống → CONDITIONAL |

## Verdict + decision

| Thuật ngữ | Nghĩa | Ví dụ |
|---|---|---|
| **Verdict** | Quyết định cuối về AI pilot: GO / CONDITIONAL / NO-GO. Phải defendable bằng data. | "CONDITIONAL GO với 3 conditions" |
| **GO** | Tiến hành pilot không điều kiện. Base ROI > 3:1, sống 4-5/5 scenarios, combined worst > 1.5:1. | Hiếm cho AI pilot small scale (thường > 5:1 mới chắc GO) |
| **CONDITIONAL** | Tiến hành với điều kiện rõ + monitoring + stop trigger. Base ROI 1.5-3:1, hoặc sống 2-3/5 scenarios, hoặc combined worst 1-1.5:1. Phổ biến nhất (70%+ AI pilot). | "CONDITIONAL: adoption ≥ 60% tháng 1, lock contract 6 tháng" |
| **NO-GO** | Không khả thi ở scope hiện tại. Base ROI < 1.5:1, hoặc sống <2/5 scenarios. Liệt kê 2-3 changes để khả thi (không từ chối khô khan). | "NO-GO at current scope. Cần: cheaper model + broader pilot + renegotiate constraint" |
| **Monitoring metrics** | 3-5 metrics track hàng tuần/tháng để biết pilot trên track hay không. | Adoption rate, Cost/task, Quality, CSAT, Budget burn rate |
| **Stop / Pivot trigger** | Ngưỡng cứng: nếu X xảy ra trong Y thời gian → pause / pivot. | "Adoption < 40% trong 30 ngày liên tiếp → pause review" |

## Roles & buyer

| Thuật ngữ | Nghĩa | Ví dụ |
|---|---|---|
| **Buyer** | Người quyết định mua AI product. Khác user. | Brief #1: CTO; Brief #4: Managing Partner; Brief #7: Director Supply Chain |
| **Buying trigger** | Vì sao buyer quyết định mua HÔM NAY (không phải năm sau). | Pain point (churn 18%) + alternative cost cao (hire 5 thêm agent $300K/year) |
| **Delegator vs Prosumer** | Delegator = user giao việc hết cho AI (high autonomy). Prosumer = user tham gia một phần (low autonomy). | Delegator: Intercom Fin auto-reply. Prosumer: GitHub Copilot suggest, dev decide. |

## AI-specific economics

| Thuật ngữ | Nghĩa | Ví dụ |
|---|---|---|
| **Variable cost** | Cost thay đổi theo usage (vs fixed cost). AI products có cost dominate by variable. | API cost = per call. Mỗi user × mỗi task = chi phí cộng dồn |
| **Marginal cost** | Cost thêm 1 user / 1 task. Với traditional SaaS gần 0; với AI = cost API + tooling. | Thêm 1 ticket = $0.0084 API + $0.50 review = $0.51 marginal cost |
| **Rented land** | Phụ thuộc platform/provider bên ngoài (OpenAI, Anthropic, Google). Risk nếu provider đổi giá hoặc deprecate. | Replit dùng Anthropic + OpenAI — provider risk hiện hữu |
| **Data flywheel** | AI cải thiện nhờ usage data (feedback loop). Value tăng dần. | Cursor học từ user accept/reject suggestions → quality tăng |
| **Worked example** | Ví dụ tính trực tiếp từ A-Z, có số cụ thể (không generic). | Skeleton Slide 7: Support Copilot từ usage unit → cost → value → ROI |

## Common mistakes (sai lầm thường gặp)

| Sai lầm | Đúng |
|---|---|
| "AI tự làm xong" mà brief có 100% review constraint | Low autonomy thực sự |
| "Quality 95%" | Theo benchmark: 60-85% là realistic |
| "Adoption 90%" | Realistic 50-80% pilot mandatory |
| Dùng Gross time saved | NET = Gross − wait − review − switch − rework |
| Cost/task = $0.001 (chỉ API) | Include human review + tooling + setup |
| Verdict GO chắc chắn | CONDITIONAL là default cho AI pilot |
| Conditions chung chung "track adoption" | Conditions cụ thể: "Adoption ≥ 60% tháng 1, weekly check" |
| Combined worst = 1 scenario | Combined = 2 scenarios đồng thời |

---

## Cách dùng Glossary trong worksheet

- Khi viết worksheet và gặp thuật ngữ → tham chiếu glossary để dùng đúng.
- Khi prompt AI → có thể paste 1 phần glossary để AI hiểu thuật ngữ AI20k.
- Khi present → dùng glossary để đảm bảo audience hiểu thuật ngữ.

Nếu thấy thuật ngữ chưa có trong glossary → ghi vào ghi chú nhóm, đóng góp cho future cohort.
