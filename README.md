# 📱 Phone Price & Specification Analysis Project

## 🧾 Mục tiêu

Dự án nhằm thu thập, xử lý và phân tích dữ liệu sản phẩm điện thoại từ các nguồn online, để khám phá những yếu tố ảnh hưởng đến giá bán như RAM, chip, bộ nhớ, thương hiệu,... Dự án cũng minh họa quy trình crawl dữ liệu, làm sạch, phân tích thống kê và trực quan hóa thông tin.

---

```
├── phone_data.xlsx                   # File gốc chứa dữ liệu thu thập từ website
├── phone_data <date>.xlsx           # File dữ liệu đã xử lý
├── 03_completed_web_crawl.ipynb     # Notebook crawl dữ liệu sản phẩm
├── phan tich và bieu do.ipynb       # Notebook phân tích và trực quan dữ liệu
├── File.sql                         # Tập lệnh tạo CSDL và nhập dữ liệu
└── README.md                        # Tài liệu mô tả dự án
```


## 🧪 Công nghệ sử dụng

- **Ngôn ngữ**: Python, SQL
- **Thư viện Python**: `pandas`, `matplotlib`, `seaborn`, `re`, `openpyxl`
- **Notebook**: Jupyter (`.ipynb`)
- **Cơ sở dữ liệu**: MySQL
- **Công cụ crawl**: Requests, BeautifulSoup / JSON endpoint
- **Trực quan hóa**: Biểu đồ thanh, biểu đồ phân bố, biểu đồ hộp

---

## 📊 Các bước thực hiện

### 1. Thu thập dữ liệu
- Sử dụng `Selenium` hoặc API `/products/<handle>.js` của website
- Trích xuất các trường: `name`, `brand`, `price`, `chip`, `ram`, `storage`, `img_link`, `description`

### 2. Tiền xử lý và chuẩn hóa
- Chuẩn hóa RAM, Chip, Storage từ cột `utility`
- Làm sạch văn bản mô tả, loại bỏ stop words tiếng Việt
- Chuyển đổi định dạng dữ liệu phù hợp để phân tích

### 3. Phân tích dữ liệu

#### 🔹 Tổng quan:
- Dataset gồm nhiều dòng máy như iPhone, Samsung Galaxy (S, A, M, Z), Xiaomi Redmi...
- Phân bố giá bị lệch phải (nhiều máy giá rẻ, ít máy giá cao)

#### 🔹 Phân tích kỹ thuật:
- RAM cao thường đi kèm mức giá cao hơn
- Chip cao cấp như A17, Snapdragon 8 Gen2 → giá cao hơn
- Text analysis trên mô tả sản phẩm cần làm sạch để khai thác thêm đặc điểm nổi bật

### 4. Trực quan hóa dữ liệu
- Biểu đồ phân phối giá theo RAM và Chip
- Biểu đồ hộp so sánh mức giá giữa các thương hiệu
- Heatmap thể hiện tương quan giữa RAM, Storage và Price

---

## 🧠 Một số phát hiện chính

- RAM và Chip là hai yếu tố ảnh hưởng mạnh đến giá bán
- Thương hiệu cũng là yếu tố chi phối mạnh mẽ (ví dụ: iPhone đắt hơn Xiaomi dù cấu hình tương đương)
- Một số sản phẩm có mô tả marketing dài → cần xử lý ngôn ngữ tự nhiên để trích xuất giá trị thật sự

---

## 🔁 Cơ sở dữ liệu

```sql
CREATE DATABASE dienthoai;

USE dienthoai;

CREATE TABLE phone_data (
    id INTEGER PRIMARY KEY AUTO_INCREMENT,
    name TEXT,
    brand TEXT,
    price INT,
    chip TEXT,
    ram TEXT,
    storage TEXT,
    img_link TEXT,
    description TEXT
);
