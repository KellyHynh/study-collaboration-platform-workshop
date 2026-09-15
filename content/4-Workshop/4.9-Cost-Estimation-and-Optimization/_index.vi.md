---

title: "Dự toán và tối ưu chi phí"

date: 2026-09-15

weight: 9

chapter: false

pre: " <b> 4.9. </b> "

---

# Dự toán và tối ưu chi phí

Phần này ước tính chi phí vận hành hàng tháng và hàng năm của cơ sở hạ tầng AWS được sử dụng để triển khai ứng dụng KnoVerse.

Mức ước tính này dành cho môi trường học tập và thực tập quy mô nhỏ thay vì workload production. Mục tiêu chính là xác định chi phí dự kiến để duy trì hệ thống đã triển khai hoạt động liên tục và thể hiện cách kiến trúc có thể được tối ưu nhằm giảm các khoản chi AWS không cần thiết.

Tất cả các khoản bên dưới là mức ước tính gần đúng bằng USD. Chi phí thực tế phụ thuộc vào AWS Region, cấu hình tài nguyên, lưu lượng truy cập, dung lượng lưu trữ, số lượng request, Free Tier hoặc promotional credits, và thời gian thực tế mà mỗi tài nguyên được duy trì hoạt động. Mức ước tính cuối cùng nên được kiểm tra bằng AWS Pricing Calculator trước khi triển khai hoặc trước khi trình bày chi phí cuối cùng. AWS Pricing Calculator cung cấp ước tính hàng tháng và 12 tháng dựa trên các giả định về workload do người dùng nhập vào.

## 4.9.1. Các giả định về dự toán chi phí

Mức ước tính sử dụng workload đơn giản hóa như sau:

- AWS Region: ap-southeast-1 (Asia Pacific – Singapore)

- Một Amazon EC2 instance nhỏ chạy backend KnoVerse.

- Một Amazon RDS for PostgreSQL instance nhỏ.

- Một Application Load Balancer.

- Một Amazon CloudFront distribution.

- Một AWS WAF Web ACL với một số lượng nhỏ rule.

- Một Amazon S3 bucket để lưu trữ assets của ứng dụng.

- Một AWS Amplify application cho frontend.

- Lưu lượng phát triển/kiểm thử thấp.

- Khoảng 730 giờ hoạt động mỗi tháng.

- Dung lượng lưu trữ và data transfer ở mức nhỏ.

- Không bao gồm AWS Support Plan trả phí.

- Không bao gồm chi phí đăng ký domain.

- Không bao gồm thuế.

Do dự án được thực hiện cho mục đích học tập và trình diễn, workload ước tính nhỏ hơn đáng kể so với một hệ thống production phục vụ số lượng lớn người dùng.

## 4.9.2. Dự toán chi phí các dịch vụ AWS

### Amazon EC2

EC2 instance được sử dụng để chạy backend Node.js/Express của KnoVerse.

Cấu hình ước tính:

- 1 EC2 instance general-purpose nhỏ

- Khoảng 730 giờ hoạt động/tháng

- Hệ điều hành Linux

- EBS volume nhỏ cho ứng dụng và hệ điều hành

Chi phí hàng tháng ước tính:

- EC2 compute: khoảng $8.00–$9.00/tháng

- EBS storage: khoảng $1.00–$2.00/tháng

Tổng chi phí EC2 ước tính: khoảng $10.00/tháng.

Chi phí thực tế phụ thuộc vào loại instance được lựa chọn và cấu hình EBS.

### Amazon RDS for PostgreSQL

Amazon RDS được sử dụng để lưu trữ PostgreSQL database của KnoVerse.

Cấu hình ước tính:

- 1 RDS PostgreSQL instance nhỏ

- Khoảng 730 giờ/tháng

- Storage volume general-purpose nhỏ

- Triển khai Single-AZ cho môi trường học tập

- Không sử dụng cấu hình Multi-AZ

Chi phí hàng tháng ước tính:

- DB instance: khoảng $12.00–$14.00/tháng

- Database storage: khoảng $1.00–$2.00/tháng

Tổng chi phí RDS ước tính: khoảng $14.00/tháng.

Việc sử dụng instance Single-AZ nhỏ là một phương án tối ưu chi phí quan trọng đối với dự án thực tập. Multi-AZ cung cấp khả năng availability cao hơn nhưng sẽ làm tăng chi phí đáng kể.

### Application Load Balancer

Application Load Balancer phân phối lưu lượng HTTP/HTTPS đến backend EC2 instance.

Đối với môi trường phát triển có lưu lượng thấp, chi phí ước tính khoảng:

- Chi phí ALB theo giờ và mức sử dụng LCU thấp: khoảng $18.00–$20.00/tháng

Tổng chi phí ALB ước tính: khoảng $19.00/tháng.

Chi phí ALB thực tế phụ thuộc vào số lượng Load Balancer Capacity Units (LCUs) được sử dụng.

### Amazon CloudFront

CloudFront được sử dụng làm lớp phân phối public phía trước backend ALB.

Đối với workload học tập có lưu lượng thấp, mức sử dụng ước tính khoảng 5 GB data transfer và một số lượng request nhỏ sẽ tạo ra chi phí sử dụng tương đối thấp.

Chi phí hàng tháng ước tính:

- CloudFront requests và data transfer: khoảng $0.50/tháng

Tổng chi phí CloudFront ước tính: khoảng $0.50/tháng.

AWS cũng cung cấp gói CloudFront Free flat-rate cho các trường hợp sử dụng đủ điều kiện. Do đó, mô hình tính phí được lựa chọn cần được kiểm tra trước khi triển khai chính thức vì cấu trúc chi phí có thể khác với mô hình pay-as-you-go truyền thống.

### AWS WAF

AWS WAF bảo vệ public application endpoint khỏi các cuộc tấn công web phổ biến.

Cấu hình ước tính:

- 1 Web ACL

- Một số lượng nhỏ rule

- Lưu lượng request thấp

Chi phí hàng tháng ước tính:

- Web ACL: khoảng $5.00/tháng

- Rules và request processing: khoảng $1.00/tháng

Tổng chi phí WAF ước tính: khoảng $6.00/tháng.

Chi phí WAF thực tế phụ thuộc vào số lượng Web ACL, rule và web request.

### Amazon S3

S3 được sử dụng để lưu trữ application assets và các object khác.

Workload ước tính:

- Khoảng 5 GB Standard storage

- Lưu lượng request thấp

- Một lượng nhỏ data transfer

Chi phí hàng tháng ước tính:

- Storage: khoảng $0.12/tháng

- Requests và các mức sử dụng liên quan: khoảng $0.05/tháng

Tổng chi phí S3 ước tính: khoảng $0.17/tháng.

### AWS Amplify

Amplify được sử dụng để host frontend application của KnoVerse.

Đối với một application phát triển nhỏ với số phút build, storage, request và data transfer hạn chế, mức sử dụng dự kiến có thể nằm trong Free Tier hoặc credits áp dụng cho tài khoản đủ điều kiện.

Đối với mức ước tính thận trọng khi không áp dụng Free Tier:

- Build và hosting usage: khoảng $0.50/tháng

Tổng chi phí Amplify ước tính: khoảng $0.50/tháng.

Số tiền chính xác phụ thuộc vào build minutes, dữ liệu được lưu trữ, request và data transfer.

### Các chi phí hỗ trợ khác

Các chi phí có thể phát sinh khác bao gồm:

- Data transfer giữa các AWS services: khoảng $0.50/tháng đối với workload nhỏ được giả định ở đây.

- CloudWatch logs và monitoring: khoảng $0.50/tháng.

- Elastic IP hoặc các khoản phí networking tùy chọn khác: khoảng $0.00–$1.00/tháng tùy thuộc vào cấu hình.

Tổng chi phí các dịch vụ hỗ trợ ước tính: khoảng $1.00/tháng.

## 4.9.3. Tổng hợp chi phí hàng tháng

Dựa trên các giả định trên, chi phí hàng tháng ước tính là:

| AWS Service                                         | Estimated Monthly Cost |
| --------------------------------------------------- | ---------------------: |
| Amazon EC2 + EBS                                    |                 $10.00 |
| Amazon RDS PostgreSQL                               |                 $14.00 |
| Application Load Balancer                           |                 $19.00 |
| Amazon CloudFront                                   |                  $0.50 |
| AWS WAF                                             |                  $6.00 |
| Amazon S3                                           |                  $0.17 |
| AWS Amplify                                         |                  $0.50 |
| Data Transfer + CloudWatch + other supporting usage |                  $1.00 |
| **Estimated Total**                                 |       **$51.17/month** |

Chi phí hàng năm ước tính:

$51.17 × 12 = **$614.04/year**

Đây là mức ước tính phục vụ cho việc lập kế hoạch khi duy trì cơ sở hạ tầng hoạt động liên tục khoảng 730 giờ mỗi tháng. Không nên xem đây là hóa đơn AWS được đảm bảo.

## 4.9.4. Xem xét Free Tier và Credit

Số tiền thực tế mà dự án phải trả có thể thấp hơn đáng kể nếu tài khoản AWS đủ điều kiện nhận các quyền lợi Free Tier hoặc AWS promotional credits.

Ví dụ, AWS cho biết khách hàng mới có thể nhận AWS Free Tier credits theo chương trình Free Tier hiện tại. Các credits này có thể được áp dụng cho các dịch vụ đủ điều kiện. Vì vậy, chi phí cơ sở hạ tầng ước tính và số tiền thực tế được tính vào tài khoản có thể khác nhau.

Báo cáo nên phân biệt giữa:

- Chi phí cơ sở hạ tầng ước tính trước khi áp dụng credits.

- Các quyền lợi Free Tier được áp dụng.

- AWS promotional credits.

- Số tiền thực tế được tính vào tài khoản AWS.

Vì lý do này, AWS Billing and Cost Management dashboard nên được kiểm tra trong và sau quá trình triển khai.

## 4.9.5. Tối ưu chi phí

Một số quyết định thiết kế đã được thực hiện nhằm giữ cho việc triển khai KnoVerse phù hợp với môi trường thực tập và học tập.

### 1. Sử dụng compute instance nhỏ

Backend không yêu cầu một EC2 instance có cấu hình lớn vì workload dự kiến thấp. Một instance nhỏ là đủ để chạy Node.js/Express API.

### 2. Sử dụng RDS Single-AZ

Database sử dụng cấu hình Single-AZ cho môi trường học tập. Multi-AZ hữu ích khi yêu cầu availability cao hơn nhưng không cần thiết đối với một hệ thống demo nhỏ và sẽ làm tăng chi phí.

### 3. Giữ yêu cầu storage ở mức nhỏ

Dự án chỉ lưu trữ dữ liệu và assets cần thiết cho application. Các backup, log và temporary file không cần thiết nên được xóa thường xuyên.

### 4. Sử dụng CloudFront caching

CloudFront có thể cache các response phù hợp và giảm số lượng request đến origin. Điều này có thể cải thiện hiệu năng và giảm origin traffic.

### 5. Theo dõi WAF rules và requests

Chỉ nên bật các WAF rule cần thiết. Các rule không cần thiết và việc logging quá mức nên được tránh vì chi phí WAF và logging phụ thuộc vào mức sử dụng.

### 6. Dừng hoặc xóa resources sau khi kiểm thử

Các resource không cần thiết ngoài thời gian phát triển hoặc trình diễn nên được dừng hoặc xóa khi có thể.

Đặc biệt, EC2 và RDS chạy liên tục có thể trở thành các khoản chi phí định kỳ chính của kiến trúc.

### 7. Theo dõi AWS billing

AWS Billing and Cost Management nên được kiểm tra thường xuyên. Có thể cấu hình Budget alerts để thông báo cho developer khi mức chi tiêu đạt đến một ngưỡng được xác định trước.

## 4.9.6. So sánh chi phí: Always-On và Workshop Usage

Mức $51.17/tháng được ước tính với giả định cơ sở hạ tầng chính được duy trì hoạt động liên tục.

Đối với một dự án thực tập, các resource có thể không cần chạy 24 giờ mỗi ngày.

Nếu backend EC2 và RDS chỉ được sử dụng trong quá trình phát triển, kiểm thử và trình diễn, chi phí hàng tháng thực tế có thể thấp hơn đáng kể. Tuy nhiên, các service như ALB và một số networking components vẫn có thể tiếp tục phát sinh chi phí trong khi chúng vẫn được provision.

Do đó, một chiến lược tiết kiệm chi phí thực tế là:

1. Khởi động các resource cần thiết trước khi phát triển hoặc trình diễn.

2. Thực hiện kiểm thử và verification.

3. Dừng các resource hỗ trợ việc stop.

4. Xóa các resource tạm thời không còn cần thiết.

5. Kiểm tra AWS Billing dashboard sau khi hoàn thành công việc.

## 4.9.7. Đánh giá chi phí cuối cùng

Kiến trúc AWS được đề xuất cho KnoVerse có chi phí ước tính khoảng:

- **Monthly infrastructure cost:** $51.17/month

- **Estimated 12-month cost:** $614.04/year

- **Hardware cost:** $0 additional, vì ứng dụng được triển khai trên cloud infrastructure và không yêu cầu thêm phần cứng vật lý cho quá trình triển khai AWS.

- **AWS Free Tier / promotional credits:** có thể làm giảm số tiền thực tế được tính.

Các khoản chi phí định kỳ lớn nhất trong kiến trúc này dự kiến đến từ Amazon RDS, Application Load Balancer và Amazon EC2. Vì vậy, các resource này nên được ưu tiên cao nhất trong quá trình tối ưu chi phí.

Mức ước tính cho thấy kiến trúc có tính khả thi về mặt kỹ thuật đối với một dự án thực tập quy mô nhỏ, đồng thời cho thấy việc duy trì toàn bộ infrastructure hoạt động liên tục sẽ tốn kém hơn so với một môi trường phát triển tối thiểu. Vì lý do này, việc lập lịch sử dụng resource, right-sizing, monitoring và loại bỏ các resource không sử dụng là những phần quan trọng trong quá trình triển khai.

## 4.9.8. AWS Pricing Calculator

Mức ước tính cuối cùng nên được kiểm tra bằng AWS Pricing Calculator với thông số resource thực tế và Region được sử dụng trong quá trình triển khai.

AWS Pricing Calculator:

https://calculator.aws/

Calculator có thể được sử dụng để tạo ước tính hàng tháng và 12 tháng, xem cách tính chi phí của từng service và so sánh các cấu hình infrastructure khác nhau.

Do đó, các giá trị trong phần này được trình bày như một mức ước tính thực tế phục vụ việc lập kế hoạch thay vì một số tiền cố định trên hóa đơn AWS.
