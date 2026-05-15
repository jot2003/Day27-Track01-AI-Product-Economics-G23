# 00 · User Journey Simulation — Đóng vai Tourist

> **Mục tiêu**: Trước khi tính chi phí, nhóm phải hình dung được khách hàng thật sự hỏi gì, hỏi như thế nào, và 1 conversation thực tế trông ra sao.
>
> **Thời gian**: 8 phút (trong 15 phút phần Setup)

---

## Tại sao phải làm bước này?

Nếu nhóm bắt đầu tính cost mà chưa biết tourist hỏi gì → mọi con số chỉ là lý thuyết. Bước này buộc nhóm "chạm" sản phẩm trước khi mở Excel.

---

## Bước 1 — Mỗi người đóng vai 1 tourist (4 phút)

Tưởng tượng mình là 1 khách du lịch nước ngoài đang plan trip Việt Nam. Bạn vừa mở website công ty du lịch, thấy có chatbot ở góc màn hình. Bạn sẽ hỏi gì?

Trước khi viết, tự hỏi:

- Mình từ đâu đến? Mỹ, Anh, Hàn, Nhật, Úc?
- Đi 1 mình hay đi nhóm? Budget khoảng bao nhiêu?
- Đã biết gì về Việt Nam? Lần đầu đến hay đã đến rồi?
- Mình lo lắng điều gì nhất? (visa, an toàn, ngôn ngữ, thời tiết, ẩm thực, lừa đảo...)

Viết **5–7 câu hỏi bằng tiếng Anh** mình sẽ thật sự gửi cho chatbot. Viết câu hỏi tự nhiên, đúng giọng tourist — không phải đặt câu hỏi "nghe có vẻ technical".

→ Mỗi người viết vào ô dưới (chưa có gì sẵn — đừng nhìn người bên cạnh):

### Tourist #1 (Tên thành viên: _________)

```text
(điền 5–7 câu hỏi tiếng Anh vào đây)
```

### Tourist #2 (Tên thành viên: Quách Gia Được)

```text
1. Hi! I'm planning a 2-week trip to Vietnam with my family. What's the best itinerary starting from Ho Chi Minh City?
2. Do US citizens need a visa to enter Vietnam? How long does the process take?
3. What is the weather like in Sapa during December? Is it too cold for kids?
4. Can you recommend some must-try local street food in Hanoi that are safe for foreigners?
5. I would like to book a 2-day Ha Long Bay cruise. Can you help me with that?
6. Is it easy to use credit cards in Vietnam or should I bring a lot of cash?
```

### Tourist #3 (Tên thành viên: Nguyễn Thành Nam)

```text
1. Do I need to book domestic flights in advance, or can I buy tickets at the airport?
2. What are the top luxury hotels in Hoi An with a private beach?
3. What is the current visa policy for Australian passport holders?
4. Is it currently raining in Da Nang?
5. I want to book a private tour guide for my family in Hue, can you arrange that?
6. Are there any local cultural events happening next week in Hanoi?
```

---

## Bước 2 — Gom lại và phân loại (4 phút)

Cả nhóm chụm vào, gom tất cả câu hỏi lại. Trước khi điền bảng, thảo luận 1 phút:

- Có câu hỏi nào lặp lại giữa các tourist không?
- Có chủ đề nào không ai trong nhóm nghĩ tới ban đầu nhưng quan trọng?
- Câu nào chatbot có thể trả lời được? Câu nào cần chuyển sang nhân viên thật?

5 intent có sẵn (tham khảo `cost-reference-card.md` mục 2):

- **Visa/Policy** — chính sách, thủ tục nhập cảnh
- **Điểm đến/Guide** — gợi ý đi đâu, làm gì, ăn gì
- **Thời tiết/Sự kiện** — info real-time
- **Tour/Booking** — đặt vé, đặt tour, đặt phòng → chuyển sales
- **Khiếu nại** — phàn nàn → chuyển manager

Sau khi gom, điền bảng phân loại:

| # | Câu hỏi (1 dòng) | Intent thuộc loại nào | Cần bao nhiêu lượt chat để xong? | Bot trả lời hay chuyển người? |
|---|---|---|---|---|
| 1 | Best itinerary from Ho Chi Minh City? | Guide | 4 | ☑ Bot · □ Người |
| 2 | Do US citizens need a visa? | Visa | 3 | ☑ Bot · □ Người |
| 3 | Weather in Sapa in December? | Weather | 2 | ☑ Bot · □ Người |
| 4 | Safe street food in Hanoi? | Guide | 3 | ☑ Bot · □ Người |
| 5 | Book 2-day Ha Long Bay cruise? | Booking | 1 | □ Bot · ☑ Người |
| 6 | Easy to use credit cards in Vietnam? | Guide | 2 | ☑ Bot · □ Người |
| 7 | Top luxury hotels in Hoi An? | Guide | 3 | ☑ Bot · □ Người |
| 8 | Visa policy for Australian passport? | Visa | 3 | ☑ Bot · □ Người |
| 9 | Raining in Da Nang currently? | Weather | 2 | ☑ Bot · □ Người |
| 10 | Book a private tour guide in Hue? | Booking | 1 | □ Bot · ☑ Người |

---

## Bước 3 — Rút insight cho nhóm (cuối phần Setup)

Trả lời nhanh 4 câu — sẽ dùng lại ở các bước sau:

**Tổng số câu hỏi nhóm gom được**:

```text
12
```

**Phân bố intent thực tế của nhóm** (% mỗi intent):

```text
Guide: 40%
Visa: 20%
Weather: 20%
Booking: 20%
Khiếu nại: 0%
```

**Số lượt chat trung bình để xong 1 chủ đề**:

```text
~3 lượt cho info (Guide/Visa/Weather), 1 lượt cho booking
```

**Đối chiếu với đề bài** (Scenario A = 4 lượt, Scenario B = 7 lượt):

```text
Khá hợp lý vì một conversation có thể gộp nhiều chủ đề (VD: hỏi Visa xong hỏi luôn Weather, Guide). 4-7 lượt là mức trung bình để hoàn thành một hành trình thông tin đa dạng.
```

**Insight bất ngờ — điều gì nhóm chỉ hiểu sau khi đóng vai?**

```text
Tourist thường có nhu cầu hỏi rất đa dạng intent (từ thời tiết, visa đến guide) trong cùng một lượt chat. Hơn nữa, câu hỏi Booking thường kết thúc bot session rất nhanh do handoff.
```

---

## Bảng kiểm trước khi sang file tiếp theo

- [ ] Mỗi người trong nhóm đã viết ≥5 câu hỏi tourist
- [ ] Đã gom + phân loại intent cho ≥10 câu (bảng trên)
- [ ] Đã có phân bố intent % của nhóm (so với đề bài)
- [ ] Có ít nhất 1 insight về cách tourist thật sự dùng chatbot

Xong → mở `01-base-flow.md`.
