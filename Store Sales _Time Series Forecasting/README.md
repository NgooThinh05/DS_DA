# Store Sales - Time Series Forecasting 🛒📈

## 📖 Giới thiệu chung
Đây là tài liệu và mã nguồn cho dự án giải quyết bài toán trên Kaggle: [Store Sales - Time Series Forecasting](https://www.kaggle.com/competitions/store-sales-time-series-forecasting).

Dự đoán doanh số bán hàng là một trong những bài toán cốt lõi của ngành bán lẻ. Việc dự báo chính xác giúp các cửa hàng tạp hóa, siêu thị quản lý tốt chuỗi cung ứng, tránh tình trạng tồn kho dư thừa (gây lãng phí với thực phẩm dễ hỏng) hoặc thiếu hụt hàng hóa (gây mất doanh thu và làm giảm sự hài lòng của khách hàng). 

Trong dự án này, chúng ta sẽ sử dụng dữ liệu từ **Corporación Favorita** – một tập đoàn bán lẻ tạp hóa lớn có trụ sở tại Ecuador – để xây dựng các mô hình Học máy (Machine Learning) có khả năng dự báo chính xác số lượng sản phẩm bán ra của hàng ngàn mặt hàng tại nhiều cửa hàng khác nhau.

## 🎯 Mục tiêu bài toán
Nhiệm vụ chính là xây dựng một mô hình **Dự báo chuỗi thời gian (Time-Series Forecasting)** để dự đoán `unit_sales` (số lượng bán ra) của từng mặt hàng tại mỗi cửa hàng của Favorita cho một khoảng thời gian 15 ngày trong tương lai.

## 📁 Tập dữ liệu (Dataset)
Dữ liệu huấn luyện (Training data) chứa các bản ghi lịch sử bán hàng bao gồm:
* **Ngày tháng (Date):** Thời điểm giao dịch.
* **Thông tin cửa hàng (Store):** Mã cửa hàng, vị trí (thành phố, bang), loại cửa hàng, phân cụm (cluster).
* **Thông tin sản phẩm (Item):** Nhóm ngành hàng, phân loại sản phẩm.
* **Khuyến mãi (Promotions):** Sản phẩm có đang chạy khuyến mãi vào ngày đó hay không.
* **Số lượng bán (Unit sales):** Biến mục tiêu (Target) cần dự đoán.

Bên cạnh đó, bài toán cung cấp các tập dữ liệu ngoại cảnh rất thú vị có tác động mạnh đến sức mua:
* `holidays_events.csv`: Thông tin về các ngày lễ, sự kiện (Quốc khánh, sự kiện địa phương, ngày nghỉ bù...).
* `oil.csv`: Giá dầu hằng ngày (Kinh tế Ecuador phụ thuộc nhiều vào dầu mỏ, nên biến động giá dầu ảnh hưởng trực tiếp đến sức mua của người dân).
* `transactions.csv`: Tổng số lượng giao dịch của mỗi cửa hàng theo ngày.

## 📏 Metric đánh giá (Evaluation)
Các mô hình dự đoán sẽ được đánh giá dựa trên chỉ số **Root Mean Squared Logarithmic Error (RMSLE)**.

Công thức RMSLE:
$$\text{RMSLE} = \sqrt{ \frac{1}{n} \sum_{i=1}^n \left(\log(1 + \hat{y}_i) - \log(1 + y_i)\right)^2 }$$

Trong đó:
* $n$: Tổng số lượng mẫu dự đoán.
* $\hat{y}_i$: Giá trị dự đoán (predicted unit sales).
* $y_i$: Giá trị thực tế (actual unit sales).
* $\log$: Logarit tự nhiên.

*Lý do dùng RMSLE:* Chỉ số này giúp giảm thiểu sự phạt lỗi quá lớn đối với những mặt hàng có doanh số bán ra đột biến và rất phù hợp với dữ liệu không có giá trị âm (như số lượng hàng hóa).

## 🏆 Kết quả & Thành tích
* **Điểm số (Public Score - RMSLE):** 0.38
* **Thứ hạng:** Top 10% Leaderboard Kaggle.
* **Mô hình tối ưu:** [LightGBM / CatBoost]
