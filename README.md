# Báo cáo cuối kì môn học Máy học

## Thông tin
- Chủ đề : Dự đoán khả năng chấp thuận cấp thẻ tín dụng dựa trên hồ sơ đăng ký
- Môn học: Học máy - MAT3533
- Năm học: 2025-2026
- Thành viên:
    + Nguyễn Hữu An - 23001493
    + Nguyễn Thị Quỳnh Anh - 
    + Đào Thị Ngọc Bích - 


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
    - Chuẩn hóa dữ liệu (`Feature Scaling`).
2.  **Cân bằng dữ liệu**: Sử dụng kỹ thuật **SMOTE** (Synthetic Minority Over-sampling Technique) để xử lý tình trạng mất cân bằng lớp (số lượng khách hàng rủi ro cao thường rất ít so với khách hàng tốt).
3.  **Giảm chiều dữ liệu**: Thử nghiệm với **PCA** (Principal Component Analysis) và **LDA** (Linear Discriminant Analysis) để tối ưu hóa hiệu suất mô hình.
4.  **Huấn luyện mô hình**:
    - Gradient Boosting.
    - Multi Layer Perceptron (MLP).
    - Support Vector Machine (SVM).
5. **Đánh giá mô hình**:
    - Sử dụng các chỉ số như Accuracy, Recall, Precision, F1-Score để đánh giá hiệu suất của các mô hình.
    - So sánh các chỉ số này để chọn mô hình tốt nhất.
6. **Các yêu cầu khác**
    - V.v.

## 3. Kết quả mô hình
Tóm tắt quá trình huấn luyện và kết quả huấn luyện, v.v.

| Mô hình | Accuracy | Recall | Precision | F1-Score |
| :--- | :---: | :---: | :---: | :---: |
| Mô hình 1 | ~55% | 0.55 | 0.55 | 0.55 |
| Mô hình 2| **~75%** | **0.74** | **0.74** | **0.74** |
| Mô hình 3 | ~55% | 0.55 | 0.55 | 0.55 |

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
├── models/                 # Chứa các file mô hình đã huấn luyện (nếu có)
├── outputs/                # Hình ảnh đồ thị và báo cáo kết quả
├── credit_card_approval_prediction.ipynb   # Notebook chính của dự án
└── README.md
```
