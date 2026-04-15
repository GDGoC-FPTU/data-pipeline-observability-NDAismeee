**Student Email:** 26i.anhnd@vinuni.edu.vn
**Name:** Nguyen Duc Anh

---

## Mô tả

Bài lab này xây dựng một ETL pipeline đơn giản (Extract, Validate, Transform, Load) từ dữ liệu JSON sang CSV và bổ sung các yếu tố quan sát (observability). Pipeline thực hiện:
- Đọc dữ liệu từ `raw_data.json`
- Loại bỏ record không hợp lệ (giá \(<= 0\) hoặc `category` rỗng)
- Chuẩn hoá `category` (Title Case), tính `discounted_price` (giảm 10%), và thêm cột `processed_at`
- Lưu kết quả ra `processed_data.csv`

Ngoài ra, phần stress test minh hoạ tác động của dữ liệu “rác” lên agent (mô phỏng RAG) trong `agent_simulation.py` và được ghi lại trong `experiment_report.md`.

---

## Cách chạy (How to Run)

### Prerequisites
```bash
pip install pandas
```

### Chạy ETL Pipeline
```bash
python solution.py
```

### Chạy Agent Simulation (Stress Test)
```bash
python generate_garbage.py
python agent_simulation.py
```

---

## Cấu trúc thư mục

```
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output của pipeline
├── experiment_report.md     # Báo cáo thí nghiệm
└── README.md                # File này
```

---

## Kết quả

Sau khi chạy `python solution.py`, pipeline sẽ in ra thống kê số record đã extract/giữ lại/bị loại và tạo file `processed_data.csv`. Với bộ dữ liệu mẫu, các record có `price <= 0` hoặc `category` rỗng sẽ bị loại bỏ; các record hợp lệ sẽ được tính thêm `discounted_price` và gắn `processed_at`.
