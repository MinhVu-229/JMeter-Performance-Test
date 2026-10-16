# Báo Cáo Kiểm Tra Hiệu Năng Bằng JMeter

## Kiểm tra hiệu năng trang web Phenikaa

### 1. Mục tiêu
- Sử dụng JMeter mô phỏng 100 người dùng truy cập đồng thời vào trang web `https://phenikaa-uni.edu.vn/vi`.
- Đánh giá khả năng chịu tải và thời gian phản hồi của hệ thống.

### 2. Kịch bản kiểm tra
- **Thread Group**:
  - Number of Threads: 100
  - Ramp-up period: 10 giây
  - Duration: 60 giây
- **HTTP Request**:
  - Server Name: `phenikaa-uni.edu.vn`
  - Path: `/vi`
  - Method: GET
  - Content encoding: UTF-8

### 3. Kết quả kiểm tra
| Chỉ số (Metric) | Giá trị (Value) |
| :--- | :--- |
| Tổng số yêu cầu (Total requests) | 100 |
| Yêu cầu thành công (Successful requests) | 47 (47%) |
| Yêu cầu thất bại (Failed requests) | 53 (53%) |
| Thời gian phản hồi trung bình (Average) | 8080 ms |
| Thời gian phản hồi trung vị (Median) | 10024 ms |
| Percentile 90% | 10093 ms |
| Percentile 95% | 10140 ms |
| Sức tải (Throughput) | 5.0 yêu cầu/giây |

### 4. Phân tích kết quả
- **Tỷ lệ thành công/thất bại:** 47% yêu cầu gửi đi thành công, 53% yêu cầu bị thất bại với mã lỗi `500 Internal Server Error`.
- **Thời gian phản hồi:** Thời gian phản hồi trung bình cao (8080 ms), thời gian chờ tối đa lên tới 10261 ms.
- **Nguyên nhân:** Khi số lượng request truy cập đồng thời tăng cao trong thời gian ngắn (100 threads / 10s ramp-up), máy chủ web xuất hiện hiện tượng quá tải tài nguyên dẫn đến phản hồi chậm và trả về lỗi 500 đối với hơn một nửa số yêu cầu.

### 5. Kết luận
Trang web chưa tối ưu tốt cho kịch bản 100 người dùng truy cập dồn dập đồng thời. Tỷ lệ lỗi cao (53%) và thời gian phản hồi kéo dài trên 8 giây. Cần nâng cấp hạ tầng server hoặc tối ưu hóa cơ chế caching/rate-limiting.

### 6. Hình ảnh minh họa
![View Results Tree](view-results-tree.png)
![Aggregate Report](aggregate-report.png)
