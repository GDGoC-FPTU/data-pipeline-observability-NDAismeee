**Student ID:** 2A202600146
**Name:** Nguyen Duc Anh
**Date:** 2026-04-15

---

## 1. Kết quả thí nghiệm

Chạy `agent_simulation.py` với 2 bộ dữ liệu và ghi lại kết quả:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Agent: Based on my data, the best choice is Laptop at $1200.0. | 9 | Dữ liệu sạch: `category` và `price` đúng, truy vấn “electronic” khớp đúng với Electronics. |
| Garbage Data (`garbage_data.csv`) | Agent: Based on my data, the best choice is Nuclear Reactor at $999999. | 3 | Dữ liệu rác: outlier giá quá lớn làm agent chọn kết quả bất thường; các lỗi như sai kiểu/null/trùng lặp làm tăng rủi ro sai. |

---

## 2. Phân tích & nhận xét (phan tich & nhan xet)

### Tại sao Agent trả lời sai khi dùng Garbage Data? (tai sao)

Dữ liệu “rác” làm agent trả lời kém chính xác vì logic truy vấn rất đơn giản: lọc theo `category` (Electronics) rồi chọn sản phẩm có `price` cao nhất. Khi dữ liệu bị “poisoned”, chỉ cần một outlier cực lớn (ví dụ `price = 999999`) là agent sẽ chọn kết quả bất thường (Nuclear Reactor) thay vì sản phẩm hợp lý trong bối cảnh thực tế. Ngoài outlier, các vấn đề khác như **ID trùng lặp** làm thông tin mâu thuẫn/không nhất quán, **giá trị null** ở `category`/`price` làm bước lọc dữ liệu không ổn định, và **sai kiểu dữ liệu** (chuỗi trong cột giá) có thể gây sai lệch khi tính toán hoặc phân tích. Tóm lại, chất lượng dữ liệu kém không chỉ khiến agent có thể “crash” mà còn có thể dẫn đến kết luận sai một cách rất tự tin, vì agent không có cơ chế phát hiện bất thường hay kiểm tra ràng buộc dữ liệu.

---

## 3. Kết luận

**Quality Data > Quality Prompt?** (Đồng ý hay không? Giải thích ngắn gọn.)

Đồng ý. Prompt tốt chỉ giúp agent hiểu câu hỏi, nhưng nếu dữ liệu đầu vào bị lỗi (sai kiểu, null, outlier, trùng lặp) thì các bước truy vấn/tính toán sẽ trả về kết quả sai hoặc gặp lỗi. Vì vậy, chất lượng dữ liệu là điều kiện tiên quyết để prompt phát huy hiệu quả.
