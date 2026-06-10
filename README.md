# 🚴 Adventure Works Sales Analysis
> **Hệ thống Dashboard phân tích doanh thu toàn diện tích hợp trên Microsoft Excel.**

Hệ thống Business Intelligence (BI) hoàn chỉnh chuyển hóa dữ liệu thô từ chu kỳ bán hàng **2005 - 2008** của Adventure Works thành các báo cáo trực quan, tương tác động (Interactive Dashboards). Dự án giúp nhà quản lý theo dõi hiệu suất tài chính, tối ưu hóa chiến lược kinh doanh và thấu hiểu hành vi khách hàng.

---

## 📌 Chỉ số Key Metrics (Tổng quan cấu trúc)
* **Tổng doanh thu (Total Revenue):** $95.22M (Toàn chu kỳ) / $31.43M (Năm mẫu 2007)
* **Tổng lợi nhuận (Total Profit):** $38.70M
* **Biên lợi nhuận trung bình (% Profit Margin):** 41%
* **Quy mô:** 13.35K giao dịch | 139.40K sản phẩm đã bán

---

## 🗂️ Kiến trúc tệp dữ liệu (Workbook Architecture)

Dự án được cấu trúc chuẩn hóa chia làm 2 lớp xử lý tách biệt:

### 1. Lớp Nền xử lý & Tính toán (Back-end Data)
* **Overview Data (Line 1 & 2):** Khu vực chứa các bảng Pivot nâng cao, xử lý công thức tăng trưởng qua từng năm (YoY % Growth), tách biệt doanh số ngày thường/cuối tuần (`Weekday` vs `Weekend`), hỗ trợ các trường lọc động (Slicers).
<img width="1786" height="531" alt="image" src="https://github.com/user-attachments/assets/eac726fe-7c85-47cd-ad83-ad6d4e006f49" />

<img width="1488" height="331" alt="image" src="https://github.com/user-attachments/assets/d8f9ed21-1df7-41f3-97cf-f6a5800c94db" />


* **Detail Data (Line 1 & 2):** Tập trung vào thuật toán xếp hạng nhóm (`Top-5`), phân nhóm khách hàng theo độ tuổi (`Age Group`), giới tính (`Gender`), phân loại giá trị sản phẩm (`Price Types`) và phân phối địa lý (`Country`).
<img width="833" height="499" alt="image" src="https://github.com/user-attachments/assets/7d51944f-adde-433e-a517-d2e0b229cf7c" />

<img width="962" height="401" alt="image" src="https://github.com/user-attachments/assets/e26de92a-f003-4053-9bd7-1e5abbc83dbc" />

### 2. Giao diện trực quan trực tiếp (Front-end Dashboards)
* **Tab 1: Overview Dashboard:** Tập trung vào các chỉ số tài chính vĩ mô, xu hướng dòng tiền và hành vi mua sắm theo thời gian.
* **Tab 2: Detail Dashboard:** Đi sâu vào phân tích cơ cấu danh mục sản phẩm, chân dung khách hàng và hiệu suất phân phối toàn cầu.

---

## 📊 Chi tiết các phân hệ chức năng

### 🎛️ Tab 1: Overview Dashboard
| Thành phần | Chức năng & Chỉ số hiển thị | Kỹ thuật áp dụng |
| :--- | :--- | :--- |
| **Thẻ KPI Card thông minh** | Hiển thị 6 chỉ số chiến lược: Total Qty, COGS, Revenue, Profit, % Margin, Transactions đi kèm tỷ lệ tăng trưởng so với năm trước (YoY). | Slicers + Dynamic Text + Conditional Formatting |
| **Biểu đồ xu hướng (Monthly Trend)** | Theo dõi biến động lợi nhuận 12 tháng. Tự động highlight tháng đỉnh điểm bằng tiêu đề động (Tháng 10 chiếm 11.99%). | Line Chart + Dynamic Title formulation |
| **Phân tích Thứ trong tuần** | So sánh doanh số chi tiết từ Chủ Nhật đến Thứ Bảy. Biểu đồ Donut phân rã tỷ trọng Weekday (74.89%) vs Weekend (25.11%). | Donut Chart + Column Chart |
| **Cơ cấu theo Quý (Quarterly View)** | Thanh tiến độ trực quan phân bổ lợi nhuận theo 4 Quý, xác định Quý 4 luôn đạt hiệu suất cao nhất (~41%). | Shape Matrix + Data Grouping |

### 🔍 Tab 2: Detail Dashboard
| Thành phần | Chức năng & Chỉ số hiển thị | Kỹ thuật áp dụng |
| :--- | :--- | :--- |
| **Top-5 Profitable Products** | Xếp hạng 5 sản phẩm mang lại lợi nhuận cao nhất (Dẫn đầu là *Mountain-200 Silver* với $977.41K), chiếm 33.8% tổng thể. | Pivot Filter (Top 10) + Bar Chart |
| **Top-5 Profitable Customers** | Xác định 5 khách hàng VIP đóng góp lớn nhất (Dẫn đầu là *Tasha Deng* - $39.46K). Nhóm này chỉ chiếm 1.38%, cho thấy doanh thu phân bổ an toàn. | Pie Chart + Row Ranking |
| **Quản lý vòng đời sản phẩm** | Kiểm soát kho hàng: Tổng sản phẩm hiện có (606), Đang kinh doanh (133), Sản phẩm chưa phát sinh doanh số/Tồn kho (473). | Hàm `COUNTA` + `COUNTIF` nâng cao |
| **Chân dung Khách hàng** | Tỷ lệ giới tính (Nữ 51% / Nam 49%), độ tuổi trung bình 46. Nhóm tuổi *Senior* đóng góp lợi nhuận cao nhất (29% ~ $3.70M). | Histogram + Gender Ratio Progress Bar |
| **Bản đồ Doanh số Toàn cầu** | Trực quan hóa phân phối doanh thu tại các thị trường: Úc ($13M), Mỹ ($13M), Vương Quốc Anh ($6M), Đức ($5M), Pháp ($4M), Canada ($2M). | Excel Filled Map Diagram |

---

## 🚀 Hướng dẫn tương tác (User Guide)

Dashboard được thiết kế theo tư duy **Self-Service BI**, người dùng tương tác qua bộ công cụ điều hướng trực quan:

1. **Bộ lọc thời gian (Time Slicing):** Click chọn các năm `2005`, `2006`, `2007`, `2008` trên bảng Slicer để đồng bộ hóa toàn bộ báo cáo.
2. **Bộ lọc thị trường (Geographical Slicing):** Tại Tab *Detail*, chọn quốc gia cụ thể trên danh sách để xem chi tiết hành vi tiêu dùng tại vùng lãnh thổ đó.
3. **Nút Xóa bộ lọc (Clear Filter):** Click vào nút màu cam `Clear Filter` ở thanh điều hướng trên cùng để đưa tất cả dữ liệu về trạng thái tổng hợp ban đầu.
4. **Chuyển đổi Tab (Tab Navigation):** Sử dụng cặp nút bấm `Overview` và `Detail` để chuyển đổi mượt mà giữa hai giao diện màn hình.

---

## 🛠️ Hướng dẫn bảo trì & Cập nhật dữ liệu

* **Cập nhật định kỳ:** Khi có dữ liệu mới, chỉ cần dán nối tiếp dữ liệu vào bảng Data Source gốc. Vào thẻ `Data` trên thanh Ribbon của Excel -> Chọn `Refresh All`. Hệ thống sẽ tự động tính toán lại toàn bộ dữ liệu nền và biểu đồ.
* **Lưu ý kỹ thuật:** Các chỉ số YoY sử dụng nguyên lý so sánh chéo liên kết năm: 
  $$\text{Percentage} = \frac{\text{Selected Yr} - \text{Previous Yr}}{\text{Previous Yr}}$$
  *Vui lòng không xóa các cột phụ tính toán ở phần Back-end Table để tránh gây ra lỗi hiển thị `#REF!`.*
