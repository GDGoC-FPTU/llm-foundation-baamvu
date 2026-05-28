# Ngày 1 — Bài Tập & Phản Ánh
## Nền Tảng LLM API | Phiếu Thực Hành

**Thời lượng:** 1:30 giờ  
**Cấu trúc:** Lập trình cốt lõi (60 phút) → Bài tập mở rộng (30 phút)

---

## Phần 1 — Lập Trình Cốt Lõi (0:00–1:00)

Chạy các ví dụ trong Google Colab tại: https://colab.research.google.com/drive/172zCiXpLr1FEXMRCAbmZoqTrKiSkUERm?usp=sharing

Triển khai tất cả TODO trong `template.py`. Chạy `pytest tests/` để kiểm tra tiến độ.

**Điểm kiểm tra:** Sau khi hoàn thành 4 nhiệm vụ, chạy:
```bash
python template.py
```
Bạn sẽ thấy output so sánh phản hồi của GPT-4o và GPT-4o-mini.

---

## Phần 2 — Bài Tập Mở Rộng (1:00–1:30)

### Bài tập 2.1 — Độ Nhạy Của Temperature
Gọi `call_openai` với các giá trị temperature 0.0, 0.5, 1.0 và 1.5 sử dụng prompt **"Hãy kể cho tôi một sự thật thú vị về Việt Nam."**

**Bạn nhận thấy quy luật gì qua bốn phản hồi?** (2–3 câu)
> Khi temperature thấp (0.0), câu trả lời thường ổn định, ít biến thể và “an toàn” hơn (ít sáng tạo, ít chi tiết lạ). Khi tăng temperature lên 0.5–1.0, phản hồi đa dạng hơn về cách diễn đạt và ví dụ. Ở 1.5, mức ngẫu nhiên cao dễ dẫn tới thêm thắt chi tiết mang tính suy đoán hoặc dài dòng hơn.

**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**
> Mình chọn khoảng **0.2–0.5**: đủ linh hoạt để diễn đạt tự nhiên, nhưng vẫn ưu tiên độ nhất quán và giảm rủi ro “bịa” thông tin. Với các câu trả lời cần chính xác (chính sách/giá/điều khoản), có thể hạ xuống gần 0.0.

---

### Bài tập 2.2 — Đánh Đổi Chi Phí
Xem xét kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người thực hiện 3 lần gọi API, mỗi lần trung bình ~350 token.

**Ước tính xem GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này:**
> Nếu chỉ xét **output token** theo đề: GPT-4o là **$0.010/1K**, GPT-4o-mini là **$0.0006/1K** ⇒ GPT-4o đắt hơn khoảng \(0.010 / 0.0006 \approx 16.67\) lần. Workload/ngày: \(10{,}000 \times 3 \times 350 = 10{,}500{,}000\) tokens ⇒ chi phí ước tính: GPT-4o \(\approx 10{,}500 \times 0.010 = \$105\)/ngày, mini \(\approx 10{,}500 \times 0.0006 = \$6.3\)/ngày.

**Mô tả một trường hợp mà chi phí cao hơn của GPT-4o là xứng đáng, và một trường hợp GPT-4o-mini là lựa chọn tốt hơn:**
> **GPT-4o đáng tiền** khi bài toán cần chất lượng lập luận, tuân thủ hướng dẫn, xử lý ngữ cảnh phức tạp (ví dụ: trợ lý kỹ thuật, phân tích tài liệu, suy luận nhiều bước, trả lời có cấu trúc). **GPT-4o-mini phù hợp** cho tác vụ khối lượng lớn, yêu cầu phản hồi nhanh và “đủ tốt” (FAQ, phân loại, tóm tắt ngắn, gợi ý câu trả lời, triage ticket) để tối ưu chi phí.

---

### Bài tập 2.3 — Trải Nghiệm Người Dùng với Streaming
**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì non-streaming lại phù hợp hơn?** (1 đoạn văn)
> Streaming quan trọng nhất khi câu trả lời dài hoặc độ trễ không ổn định, vì nó tạo cảm giác “đang xử lý” và cho người dùng thấy tiến trình ngay lập tức (đặc biệt với chat, hỗ trợ khách hàng, hoặc các tác vụ sinh nội dung dài). Non-streaming phù hợp hơn khi phản hồi ngắn, cần atomic result (ví dụ trả về JSON/định dạng chặt), hoặc khi UI/logic phía client đơn giản và không muốn xử lý dòng token, cũng như trong các workflow mà kết quả chỉ hữu ích khi đã hoàn chỉnh (ví dụ chạy tool và trả về output cuối).


## Danh Sách Kiểm Tra Nộp Bài
- [x] Tất cả tests pass: `pytest tests/ -v`
- [x] `call_openai` đã triển khai và kiểm thử
- [x] `call_openai_mini` đã triển khai và kiểm thử
- [x] `compare_models` đã triển khai và kiểm thử
- [x] `streaming_chatbot` đã triển khai và kiểm thử
- [x] `retry_with_backoff` đã triển khai và kiểm thử
- [x] `batch_compare` đã triển khai và kiểm thử
- [x] `format_comparison_table` đã triển khai và kiểm thử
- [x] `exercises.md` đã điền đầy đủ
- [x] Sao chép bài làm vào folder `solution` và đặt tên theo quy định 
