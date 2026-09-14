---

title: "Proposal"

date: 2026-06-01

weight: 2

chapter: false

pre: " <b> 2. </b> "

---

## STUDY COLLABORATION PLATFORM

### 1. Tổng quan dự án

Dự án là một nền tảng cộng tác học tập trên nền web, được thiết kế nhằm cung cấp một môi trường tập trung để người dùng tạo, quản lý và truy cập nội dung học tập.

Nền tảng tập trung vào các hoạt động học tập phổ biến như tạo khóa học, tổ chức tài liệu học tập, quản lý bài học và tương tác với các nội dung liên quan đến khóa học. Dự án ban đầu được thiết kế như một ứng dụng web quy mô nhỏ nhưng được triển khai sử dụng các dịch vụ AWS nhằm có được kinh nghiệm thực tế về triển khai ứng dụng trên cloud, cấu hình hạ tầng, lưu trữ, networking, monitoring và khả năng mở rộng.

Dự án cũng đóng vai trò là một ví dụ thực tế về cách một ứng dụng web truyền thống có thể được chuyển dần từ môi trường phát triển local sang kiến trúc dựa trên cloud bằng cách sử dụng các dịch vụ AWS được quản lý.

### 2. Mục tiêu

Các mục tiêu chính của dự án bao gồm:

* Xây dựng một nền tảng cộng tác học tập trên nền web có đầy đủ chức năng cơ bản.
* Triển khai các chức năng chính của frontend và backend.
* Thiết kế và triển khai cơ sở dữ liệu quan hệ cho ứng dụng.
* Triển khai ứng dụng bằng các dịch vụ AWS.
* Có được kinh nghiệm thực tế với hạ tầng cloud và việc tích hợp các dịch vụ AWS.
* Áp dụng các dịch vụ AWS vào nhiều thành phần khác nhau của ứng dụng, bao gồm compute, database, storage, content delivery, networking và monitoring.
* Hiểu được sự khác biệt giữa việc phát triển ứng dụng trong môi trường local và vận hành ứng dụng trên cloud.
* Thực hành các kiến thức cơ bản về bảo mật cloud, quản lý tài nguyên, monitoring và tối ưu chi phí.

Dự án chủ yếu tập trung vào việc triển khai AWS thực tế thay vì xây dựng một hệ thống có quy mô production quá phức tạp.

### 3. Vấn đề cần giải quyết

### Vấn đề là gì?

Việc quản lý tài liệu học tập và nội dung học tập trên nhiều công cụ khác nhau có thể khiến việc tổ chức khóa học, bài học và các tài nguyên liên quan trong cùng một nơi trở nên khó khăn.

Về mặt kỹ thuật, việc chỉ phát triển ứng dụng trong môi trường local không cung cấp đủ kinh nghiệm về cloud deployment, cấu hình infrastructure, networking, monitoring và các managed services.

Do đó, dự án hướng tới việc kết hợp xây dựng một ứng dụng web có đầy đủ chức năng với việc triển khai AWS thực tế.

### Giải pháp

Giải pháp được đề xuất là một ứng dụng web tập trung, nơi người dùng có thể quản lý và truy cập nội dung học tập thông qua hệ thống khóa học được tổ chức có cấu trúc.

Ứng dụng sử dụng backend API để xử lý business logic và giao tiếp với cơ sở dữ liệu quan hệ. Amazon RDS được sử dụng để lưu trữ dữ liệu ứng dụng lâu dài, trong khi Amazon S3 được sử dụng để lưu trữ file và các asset.

Backend của ứng dụng được triển khai trên Amazon EC2. Traffic của ứng dụng có thể được phân phối thông qua Application Load Balancer, trong khi Amazon CloudFront được sử dụng cho việc phân phối nội dung và caching.

Amazon CloudWatch được sử dụng để monitoring hạ tầng và môi trường ứng dụng đã triển khai.

Các dịch vụ AWS bổ sung như ElastiCache, AWS Lambda, API Gateway và AWS Amplify sẽ được tìm hiểu trong quá trình phát triển nhằm hiểu các kiến trúc thay thế và những khả năng cải tiến trong tương lai.

### 4. Kiến trúc giải pháp

Kiến trúc đề xuất kết hợp các dịch vụ compute, database, storage, networking, content delivery và monitoring.

Luồng hoạt động chính của ứng dụng:

* Người dùng truy cập ứng dụng web thông qua frontend.
* CloudFront cung cấp content delivery và caching khi phù hợp.
* Traffic của ứng dụng được chuyển đến backend thông qua Application Load Balancer.
* Backend application chạy trên Amazon EC2.
* EC2 giao tiếp với Amazon RDS để lưu trữ dữ liệu ứng dụng lâu dài.
* Amazon S3 lưu trữ các file được upload và application assets.
* Amazon CloudWatch thu thập thông tin monitoring và application logs.
* IAM kiểm soát quyền giữa người dùng, ứng dụng và các AWS resources.
* VPC cung cấp môi trường networking cho AWS infrastructure.

Kiến trúc sẽ được điều chỉnh trong quá trình phát triển dựa trên yêu cầu thực tế, chi phí và các giới hạn khi triển khai.

![Final Project AWS Architecture](images/2-Proposal/platform_architecture.PNG)

### Các dịch vụ AWS được sử dụng

* **Amazon EC2**: Host và chạy backend application.
* **Amazon RDS**: Cung cấp relational database để lưu trữ dữ liệu ứng dụng lâu dài.
* **Amazon S3**: Lưu trữ các file được upload và application assets.
* **Amazon CloudFront**: Cung cấp content delivery và caching.
* **Application Load Balancer**: Phân phối traffic đến ứng dụng và cung cấp health checks.
* **Amazon VPC**: Cung cấp môi trường networking cho các AWS resources.
* **Amazon CloudWatch**: Cung cấp monitoring, metrics và logs.
* **AWS IAM**: Quản lý quyền truy cập vào các AWS resources.
* **Amazon ElastiCache**: Được tìm hiểu để caching các dữ liệu ứng dụng thường xuyên được truy cập.
* **AWS Lambda**: Được tìm hiểu như một giải pháp serverless computing thay thế.
* **Amazon API Gateway**: Được tìm hiểu để expose các serverless APIs.
* **AWS Amplify**: Được tìm hiểu như một phương pháp thay thế cho frontend hosting và deployment.

### Thiết kế các thành phần

* **Frontend**: Cung cấp giao diện người dùng để quản lý và truy cập nội dung học tập.
* **Backend**: Cung cấp REST APIs và xử lý business logic của ứng dụng.
* **Database**: Amazon RDS lưu trữ dữ liệu ứng dụng có cấu trúc như khóa học, bài học và các thông tin liên quan.
* **File Storage**: Amazon S3 lưu trữ các file của ứng dụng và tài nguyên được upload.
* **Compute**: Amazon EC2 chạy backend application.
* **Networking**: Amazon VPC và security groups kiểm soát giao tiếp mạng giữa các thành phần của ứng dụng.
* **Load Balancing**: Application Load Balancer quản lý traffic đến ứng dụng và thực hiện health checks.
* **Content Delivery**: CloudFront cung cấp caching và phân phối các nội dung ứng dụng phù hợp.
* **Monitoring**: CloudWatch cung cấp infrastructure metrics và logs.
* **Security**: IAM được sử dụng để kiểm soát quyền truy cập AWS resources theo nguyên tắc least privilege.

### 5. Timeline

Dự án được lên kế hoạch trong khoảng thời gian 12 tuần.

* **Tuần 1-3: AWS Fundamentals**

  * Tìm hiểu các khái niệm cơ bản về AWS và các nhóm dịch vụ.
  * Học và thực hành S3, RDS, EC2 và AWS infrastructure cơ bản.
  * Làm quen với AWS Console và CLI.

* **Tuần 4-7: AWS Service Exploration**

  * Thực hành tích hợp S3 và CloudFront.
  * Tìm hiểu VPC, Application Load Balancer và CloudWatch.
  * Áp dụng các dịch vụ AWS vào một web application nhỏ.
  * Tìm hiểu Lambda, API Gateway, ElastiCache và Redis.

* **Tuần 8: Project Planning**

  * Xác định requirements và scope của dự án.
  * Thiết kế database structure.
  * Thiết kế system architecture và AWS architecture ban đầu.
  * Chuẩn bị development environment.

* **Tuần 9: Backend and Database Development**

  * Triển khai cấu trúc backend chính.
  * Thiết lập database cho dự án.
  * Phát triển các API chính và CRUD operations.
  * Tích hợp backend với Amazon RDS.

* **Tuần 10: Core Feature Development**

  * Triển khai các chức năng chính của ứng dụng.
  * Tích hợp frontend và backend.
  * Triển khai chức năng sử dụng Amazon S3.
  * Tiếp tục kiểm thử các workflow chính của ứng dụng.

* **Tuần 11: Integration and Testing**

  * Hoàn thiện các chức năng chính còn lại.
  * Tích hợp các thành phần chính của ứng dụng.
  * Thực hiện functional testing.
  * Sửa lỗi và chuẩn bị dự án cho deployment.

* **Tuần 12: AWS Deployment**

  * Deploy backend lên Amazon EC2.
  * Cấu hình RDS và S3 cho ứng dụng đã triển khai.
  * Cấu hình Application Load Balancer và CloudFront.
  * Cấu hình CloudWatch monitoring.
  * Thực hiện kiểm thử deployment cuối cùng.
  * Hoàn thiện AWS architecture và deployment documentation.

### 6. Ngân sách dự kiến

Dự án được thiết kế nhằm giảm thiểu chi phí infrastructure bằng cách sử dụng các resources đủ điều kiện sử dụng AWS Free Tier khi có thể, đồng thời tắt hoặc xóa các resources không cần thiết sau khi testing.

Chi phí thực tế phụ thuộc vào resource usage, thời gian deployment, data transfer, storage và điều kiện Free Tier áp dụng cho AWS account.

Các nhóm chi phí chính bao gồm:

* Amazon EC2: Compute resources để chạy backend application.
* Amazon RDS: Managed relational database.
* Amazon S3: Storage cho application files và assets.
* CloudFront: Content delivery và data transfer.
* Application Load Balancer: Load balancing và traffic processing.
* CloudWatch: Monitoring, metrics và logs.
* Các dịch vụ khác: Có thể sử dụng thử nghiệm ElastiCache, Lambda, API Gateway hoặc Amplify.

Việc quản lý chi phí sẽ được thực hiện trong suốt quá trình dự án bằng cách theo dõi AWS usage, xóa các resources không sử dụng và kiểm tra chi phí dự kiến trước khi kích hoạt thêm các services.

### 7. Rủi ro

#### Risk Matrix

* **Chi phí AWS phát sinh ngoài dự kiến**: Mức độ ảnh hưởng trung bình, xác suất trung bình.
* **Lỗi cấu hình deployment**: Mức độ ảnh hưởng trung bình, xác suất trung bình.
* **Vấn đề kết nối database**: Mức độ ảnh hưởng trung bình, xác suất trung bình.
* **Application bugs trong quá trình deployment**: Mức độ ảnh hưởng trung bình, xác suất trung bình.
* **Vấn đề về cấu hình AWS resources hoặc services**: Mức độ ảnh hưởng trung bình, xác suất thấp.
* **Thời gian phát triển hạn chế**: Mức độ ảnh hưởng cao, xác suất trung bình.

#### Chiến lược giảm thiểu rủi ro

* Thường xuyên theo dõi việc sử dụng AWS resources.
* Sử dụng cost monitoring và budget alerts khi phù hợp.
* Xóa các resources không sử dụng sau khi thử nghiệm và testing.
* Cấu hình security groups và IAM permissions cẩn thận.
* Tách application configuration khỏi source code bằng environment variables.
* Kiểm thử các thành phần của ứng dụng trong local environment trước khi deploy lên AWS.
* Backup các dữ liệu quan trọng của dự án và sử dụng version control.
* Triển khai và kiểm thử từng AWS component theo từng bước thay vì cấu hình toàn bộ infrastructure cùng lúc.

#### Kế hoạch dự phòng

Nếu một AWS service cụ thể gây ra độ phức tạp hoặc chi phí ngoài dự kiến, kiến trúc có thể được đơn giản hóa trong khi vẫn duy trì các chức năng cốt lõi của dự án.

Ứng dụng cũng có thể tiếp tục được phát triển và kiểm thử trong local environment nếu một cloud resource tạm thời không khả dụng hoặc cần được cấu hình lại.

### Kết quả dự kiến

Khi hoàn thành dự án, các kết quả dự kiến bao gồm:

* Một nền tảng cộng tác học tập trên nền web có đầy đủ chức năng cơ bản.
* Backend API và relational database hoạt động.
* Ứng dụng được triển khai thành công trên AWS.
* Có kinh nghiệm thực tế với EC2, RDS, S3, CloudFront, VPC, ALB và CloudWatch.
* Có hiểu biết cơ bản về IAM, ElastiCache, Lambda, API Gateway và Amplify.
* Có AWS architecture và deployment process được document.
* Có kinh nghiệm thực tế về cloud infrastructure, monitoring, security và cost management.

Dự án cuối cùng sẽ thể hiện không chỉ khả năng phát triển một web application có chức năng thực tế mà còn khả năng thiết kế, triển khai, monitoring và quản lý một ứng dụng bằng nhiều AWS services.
