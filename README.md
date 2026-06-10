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

## 🧠 Phân tích Insight sâu từ dữ liệu (Deep Data Insights)

Dựa trên luồng dữ liệu xử lý thực tế trên hệ thống báo cáo, chúng ta bóc tách được 4 vấn đề bản chất về sức khỏe doanh nghiệp và hành vi thị trường:

### 1. Hiệu ứng "Đuôi gieo - Đầu gặt" theo mùa vụ (Seasonal Imbalance)
* **Con số chứng minh:** Cấu trúc phân bổ theo quý chỉ ra rằng **Quý 4 (Q4) đóng góp tới 41%** tổng lợi nhuận cả năm. Xu hướng 12 tháng tại năm tài chính mẫu (2007) cho thấy đồ thị đi ngang khá ảm đạm từ tháng 1 đến tháng 8, sau đó bắt đầu **bùng nổ dốc đứng từ tháng 9 và đạt đỉnh vào tháng 10** (chiếm 11.99% tổng số của năm). Nửa đầu năm (Q1: 14%, Q2: 16%) có mức đóng góp rất thấp.
* **Bản chất Insight:** Chu kỳ mua sắm của khách hàng phụ thuộc nặng nề vào các chiến dịch mùa thu và mùa lễ hội cuối năm. Sự mất cân bằng này gây ra áp lực cực lớn lên chuỗi cung ứng, quản trị dòng tiền lưu động trong 6 tháng đầu năm và tiềm ẩn rủi ro tồn kho rất cao nếu thị trường biến động vào quý cuối cùng.

### 2. Nghịch lý danh mục: 96% lợi nhuận nằm ở phân khúc "Nhà giàu" (Pricing Paradox)
* **Con số chứng minh:** Nhóm sản phẩm giá cao (*Price Above $150*) mang về tới **96.5% tổng lợi nhuận** ($12.44M). Ngược lại, nhóm sản phẩm giá thấp (*Price Below $150*) chỉ đóng góp vỏn vẹn **3.5%** ($449.67K). Đặc biệt, cấu trúc sản phẩm bị cô đặc khi dòng xe đạp địa hình **Mountain-200** (Silver và Black) chiếm đến **33.8%** tổng lợi nhuận của toàn bộ danh mục.
* **Bản chất Insight:** Adventure Works vận hành thực tế như một thương hiệu phân khúc "Premium" (Cao cấp) trong mắt người tiêu dùng. Việc hệ thống ghi nhận có tới **473 sản phẩm chưa từng phát sinh doanh số (Unsold Products)** trên tổng số 606 sản phẩm hiện có chứng minh doanh nghiệp đang gánh chi phí cơ hội và chi phí lưu kho rất lớn cho một dải sản phẩm rác không hiệu quả.

### 3. Hành vi "Mua sắm công sở" đầu tuần (Weekly Purchase Patterns)
* **Con số chứng minh:** Nhóm ngày thường (**Weekday**) áp đảo hoàn toàn với **74.89%** tổng lợi nhuận ($9.65M), trong khi cuối tuần (Weekend) chỉ chiếm 25.11%. Biểu đồ phân tích ngày chỉ ra rằng **Chủ Nhật, Thứ Hai và Thứ Ba** là chuỗi 3 ngày có sức mua cao vượt trội và có xu hướng giảm dần về cuối tuần.
* **Bản chất Insight:** Khách hàng chủ lực của Adventure Works (đặc biệt là các đại lý B2B hoặc cá nhân có thu nhập cao) có thói quen lên kế hoạch mua sắm hoặc duyệt chi mua hàng ngay khi tuần mới bắt đầu, thay vì đi mua sắm ngẫu hứng vào ngày nghỉ cuối tuần như các ngành hàng tiêu dùng nhanh (FMCG).

### 4. Chân dung khách hàng: Giàu có, Trung niên và An toàn rủi ro (Demographics)
* **Con số chứng minh:** Độ tuổi trung bình của khách hàng là **46 tuổi**, trong đó nhóm tuổi **Senior** (Người lớn tuổi) đóng góp lợi nhuận cao nhất (**29%** ~ $3.70M). Tỷ lệ giới tính đạt mức cân bằng hoàn hảo (Nữ 51% / Nam 49%).
* **Tỷ lệ tập trung khách hàng:** Nhóm Top 5 khách hàng mang lại lợi nhuận lớn nhất (dẫn đầu bởi *Tasha Deng* và *Jon Zhou*) chỉ chiếm vỏn vẹn **1.38%** tổng lợi nhuận.
* **Bản chất Insight:** Tệp khách hàng có nền tảng tài chính cực kỳ vững chắc và trung thành. Việc tỷ lệ tập trung khách hàng ở mức siêu thấp chứng minh doanh nghiệp có độ an toàn hệ thống rất cao; không bị rủi ro phụ thuộc nguồn thu vào một vài "khách hàng cá mập". Thị trường đang có mô hình lưỡng cực phát triển mạnh nhất tại **Úc và Mỹ** ($13M lợi nhuận mỗi nước).

---

## 🎯 Khuyến nghị chiến lược hành động ngay (Actionable Recommendations)

Để tối ưu hóa trực tiếp vào doanh thu và giải quyết bài toán chi phí vận hành ngay lập tức, ban quản trị cần triển khai 3 nhóm chiến lược thực chiến:

### 1. Hành động về Sản phẩm & Kho bãi (Cắt tỉa danh mục và Giải phóng vốn)
* **Kích hoạt chiến dịch "Xả kho - Thu hồi vốn" cho 473 mã sản phẩm đóng băng:** Tuyệt đối dừng kế hoạch nhập hàng hoặc sản xuất mới cho các nhóm này. Thiết kế chiến lược bán kèm (Bundle Strategy): *"Mua xe đạp dòng Mountain-200 (Sản phẩm cốt lõi), Tặng kèm hoặc mua giá gốc các phụ kiện/sản phẩm thuộc nhóm tồn kho"*. Mục tiêu tối thượng là giải phóng mặt bằng kho bãi và thu hồi dòng vốn lưu động đang bị nghẽn.
* **Bảo vệ chuỗi cung ứng dòng sản phẩm cốt lõi:** Do dòng xe Mountain-200 gánh tới hơn 1/3 lợi nhuận toàn công ty, bộ phận mua hàng (Procurement) phải ký hợp đồng cam kết nguồn cung dài hạn, đảm bảo *không bao giờ được xảy ra tình trạng đứt gãy hàng hóa (Out-of-stock)* tại hai thị trường trọng điểm là Úc và Mỹ.

### 2. Hành động về Tiếp thị & Bán hàng (Tối ưu ngân sách theo thời gian)
* **Dịch chuyển khung giờ và ngân sách Marketing:** Tập trung 70% ngân sách quảng cáo kỹ thuật số (Facebook Ads, Google Ads, Email Campaign) vào các khung giờ từ **chiều Chủ Nhật đến hết ngày Thứ Ba**. Đây là thời điểm vàng khi khách hàng mở máy làm việc và có tỷ lệ chuyển đổi đơn hàng cao nhất. Cắt giảm tối đa ngân sách vào các ngày Thứ Năm, Thứ Sáu để tránh lãng phí.
* **Tái định vị thông điệp truyền thông:** Thay vì sử dụng các hình ảnh người trẻ tuổi đua xe mạo hiểm tốc độ cao, hãy chuyển dịch sang các chiến dịch mang thông điệp: *"Sức khỏe bền bỉ ở tuổi trung niên", "Sự thành đạt và trải nghiệm tự do tự tại"*. Hình ảnh đại diện nên tập trung vào nhóm khách hàng từ 40 - 50 tuổi để đánh trúng tâm lý phân khúc Senior đang mang lại dòng tiền lớn nhất cho doanh nghiệp.

### 3. Chiến lược cân bằng tài chính (Giảm áp lực doanh số cuối năm)
* **Tạo chiến dịch kích cầu "Trái mùa" vào Q1 và Q2:** Doanh số nửa đầu năm rất thấp (chỉ bằng 1/3 so với Q4). Doanh nghiệp cần chủ động tạo ra các sự kiện kích cầu lớn vào Tháng 2 và Tháng 3 lấy chủ đề *"Đón xuân cùng Adventure Works"* kết hợp với các giải pháp tài chính như liên kết ngân hàng trả góp 0% cho các dòng xe cao cấp. Việc này nhằm phân bổ lại nhu cầu của khách hàng đều hơn cho các tháng trong năm, giảm thiểu rủi ro dòng tiền bị "đói vốn" vào đầu năm và "quá tải vận hành" vào cuối năm.

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
