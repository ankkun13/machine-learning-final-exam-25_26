# Báo cáo cuối kì môn học Máy học

## Thông tin
- Chủ đề : Dự đoán khả năng chấp thuận cấp thẻ tín dụng dựa trên hồ sơ đăng ký
- Môn học: Học máy - MAT3533
- Năm học: 2025-2026
- Thành viên:
    + Nguyễn Hữu An - 23001493
    + Nguyễn Thị Quỳnh Anh - 23001496
    + Đào Thị Ngọc Bích - 23001501


## Phân công công việc

| Tên | Công việc |
| :--- | :---: |
| Đào Thị Ngọc Bích | Tiền xử lý, giảm chiều chuyển bài toán từ phân loại sang bài toán hồi quy |
| Nguyễn Hữu An | Tiền xử lý dữ liệu, xây dựng mô hình Gradient Boosting, SVM |
| Nguyễn Thị Quỳnh Anh | Phân cụm dữ liệu và mô hình MLP |
| Tất cả thành viên | Viết báo cáo, làm slide|

## Thành phần báo cáo

# Credit Card Approval Prediction - Dự đoán phê duyệt thẻ tín dụng

Dự án này tập trung vào việc xây dựng các mô hình học máy để dự định rủi ro tín dụng của khách hàng dựa trên thông tin cá nhân và lịch sử thanh toán. Mục tiêu chính là phân loại khách hàng thành hai nhóm: rủi ro cao (`Is_high_risk = 1`) và rủi ro thấp (`Is_high_risk = 0`).

## 1. Bộ dữ liệu (Dataset)
Dữ liệu bao gồm hai tệp CSV chính:
- `application_record.csv`: Chứa thông tin nhân khẩu học và kinh tế của khách hàng (thu nhập, giới hạn tín dụng, nghề nghiệp, v.v.).
- `credit_record.csv`: Chứa lịch sử thanh toán hàng tháng của khách hàng.

Biến mục tiêu `Is_high_risk` được trích xuất từ `credit_record.csv`. Khách hàng bị coi là rủi ro cao nếu họ có các khoản nợ quá hạn hơn 60 ngày.

## 2. Quy trình thực hiện
Quy trình xây dựng mô hình bao gồm các bước sau:
1.  **Tiền xử lý dữ liệu**:
    - Kết hợp (`Merge`) hai bộ dữ liệu thông qua ID khách hàng.
    - Xử lý các giá trị thiếu (`Missing values`).
    - Mã hóa các biến phân loại (`One-hot encoding`).
    - Chuẩn hóa dữ liệu (`MinMax Scaler`).
2.  **Cân bằng dữ liệu**: Sử dụng kỹ thuật **SMOTE** (Synthetic Minority Over-sampling Technique) để xử lý tình trạng mất cân bằng lớp (số lượng khách hàng rủi ro cao thường rất ít so với khách hàng tốt).
3.  **Giảm chiều dữ liệu**: Thử nghiệm với **PCA** (Principal Component Analysis) và **LDA** (Linear Discriminant Analysis) để tối ưu hóa hiệu suất mô hình.
4. **Phân cụm dữ liệu**:
    - Sử dụng **GMM** (Gaussian Mixture Model) và **DBSCAN** để khám phá cấu trúc dữ liệu không giám sát .
5.  **Huấn luyện mô hình**:
    - Gradient Boosting.
    - Multi Layer Perceptron (MLP).
    - Support Vector Machine (SVM).
6. **Đánh giá mô hình**:
    - Sử dụng các chỉ số như Accuracy, Recall, Precision, F1-Score để đánh giá hiệu suất của các mô hình.
    - So sánh các chỉ số này để chọn mô hình tốt nhất.
7. **Phân loại sang hồi quy**
    - Chuyển đổi bài toán sang dự đoán "mức độ rủi ro" liên tục bằng cách sử dụng xác suất từ mô hình phân loại làm biến mục tiêu.
    - Sử dụng mô hình XGBoost Regressor và Random Forest Regressor.

## 3. Kết quả mô hình
Kết quả tốt nhất của lớp rủi ro cao (`Is_high_risk = 1`) trên tập dữ liệu gốc (tỷ lệ chia 80:20) của các mô hình phân loại:

| Mô hình | Accuracy | Recall | Precision | F1-Score | ROC-AUC |
| :--- | :---: | :---: | :---: | :---: | :---: |
| MLP | 0.82 | 0.69 | **0.93** | 0.79 | 0.89 |
| Gradient Boosting | 0.78 | 0.78 | 0.79 | 0.78 | 0.89 |
| SVM | **0.86** | **0.87** | 0.86 | **0.86** | 0.86 |

## 4. Cài đặt và sử dụng
Yêu cầu hệ thống: Python 3.10+ và các thư viện trong `requirements.txt`:
```bash
pip install -r requirements.txt
```
hoặc cài đặt thủ công:
```bash
pip install pandas numpy matplotlib seaborn scikit-learn imbalanced-learn
```

**Sử dụng**:
Để xem chi tiết quá trình huấn luyện và đánh giá, hãy mở file notebook:
`credit_card_approval_prediction.ipynb`

## 5. Cấu trúc thư mục
```text
.
├── datasets/
│   ├── processed/          # Dữ liệu sau khi xử lý
│   └── raw/                # Dữ liệu gốc (application_record, credit_record)
├── report.pdf                # Báo cáo
├── presentation.pdf                # Slide báo cáo
├── credit_card_approval_prediction.ipynb   # Notebook chính của dự án
└── README.md
```
