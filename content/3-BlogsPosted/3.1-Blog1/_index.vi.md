---

title: "Blog 1"

date: 2026-09-13

weight: 1

chapter: false

pre: " <b> 3.1. </b> "

---

# Tự động xử lý sự cố CI/CD với AWS DevOps Agent và GitHub

Đối với những ai đã từng làm việc với GitHub Actions hoặc các hệ thống CI/CD, có lẽ bạn đã từng gặp tình huống quen thuộc này:

* Push code lên GitHub.

* Pipeline CI/CD thất bại.

* Mở log để tìm lỗi.

* Đọc từng bước Build, Test hoặc Deploy.

* Chỉnh sửa code.

* Tạo Pull Request.

* Chờ review và chạy lại pipeline.

Đối với một vài repository, quy trình này không quá phức tạp. Tuy nhiên, với những hệ thống có nhiều project, nhiều workflow và hàng trăm lần deploy mỗi ngày, việc phân tích log thủ công có thể tiêu tốn rất nhiều thời gian của đội ngũ phát triển.

Trong một bài viết mới trên AWS Blog, mình biết đến ****AWS DevOps Agent****, một AI Agent được thiết kế để tự động điều tra nguyên nhân gốc rễ khiến pipeline thất bại và hỗ trợ tạo Pull Request để khắc phục vấn đề. Điều mình thấy thú vị là AWS không chỉ ứng dụng AI để hỗ trợ lập trình, mà còn đưa AI trực tiếp vào quy trình DevOps.

## AWS DevOps Agent hoạt động như thế nào?

Theo kiến trúc được AWS giới thiệu, khi một GitHub Actions Workflow thất bại, hệ thống có thể tự động kích hoạt AWS DevOps Agent thông qua Webhook.

Luồng xử lý tổng quát có thể được mô tả như sau:

****Developer Push Code → GitHub Actions → Pipeline Failed → Webhook → AWS DevOps Agent → Đọc Workflow Logs, Source Code, Commit History và CloudWatch Logs → Phân tích nguyên nhân → GitHub MCP Server → Tạo Pull Request****

Thay vì yêu cầu DevOps Engineer hoặc Software Engineer tự đọc từng bước trong log, AI Agent có thể tự thực hiện quá trình điều tra tương tự như một kỹ sư có kinh nghiệm.

## Vai trò của từng thành phần

### 1. GitHub App

GitHub App cung cấp quyền **Read-only** để AI Agent có thể:

* Đọc source code.

* Đọc Workflow Logs.

* Kiểm tra lịch sử commit.

* Theo dõi deployment.

Điều này giúp Agent hiểu được những thay đổi nào đã xảy ra trước khi lỗi xuất hiện.

### 2. Amazon CloudWatch

CloudWatch cung cấp log từ các ứng dụng đang chạy trên AWS.

Trong trường hợp pipeline deployment hoàn thành thành công nhưng ứng dụng vẫn không thể khởi động, CloudWatch có thể chứa những thông tin quan trọng giúp AI Agent điều tra nguyên nhân.

Ví dụ:

* Không tìm thấy Secret cần thiết.

* Thiếu IAM permissions cần thiết.

* Xảy ra lỗi Runtime.

* Ứng dụng bị crash.

### 3. GitHub MCP Server

Một điểm khá thú vị là GitHub App chỉ cung cấp cho AI quyền đọc dữ liệu.

Để AI có thể thực hiện các hành động như:

* Tạo Branch.

* Cập nhật file.

* Tạo Pull Request.

* Push code.

AWS sử dụng ****GitHub MCP (Model Context Protocol) Server**** như một cầu nối cho phép Agent ghi các thay đổi trở lại GitHub sau khi xác định được giải pháp tiềm năng.

## Một ví dụ thực tế

AWS đưa ra một ví dụ liên quan đến lỗi TypeScript.

Một developer thêm thuộc tính `trackingId` vào một Object, nhưng Interface tương ứng lại không định nghĩa thuộc tính này.

Kết quả là bước Build bị thất bại.

Thay vì chỉ thông báo:

`TS2353`

`Object literal may only specify known properties...`

AWS DevOps Agent có thể:

* Đọc Build logs.

* Mở đúng file gây ra lỗi.

* Kiểm tra định nghĩa của Interface.

* Xác định commit đã tạo ra thay đổi.

* Phân tích nguyên nhân gốc rễ.

* Đề xuất cách sửa.

* Tạo Pull Request để developer review.

Điều này có thể giúp giảm đáng kể thời gian cần thiết để điều tra các lỗi trong CI/CD.

## Điều mình thấy ấn tượng

Sau khi đọc bài viết, điều khiến mình ấn tượng nhất không phải là việc AI có thể tạo Pull Request.

Điều đáng chú ý hơn là AWS đang xây dựng một quy trình troubleshooting CI/CD hoàn chỉnh hơn:

* Hệ thống phát hiện lỗi.

* AI điều tra nguyên nhân.

* AI đề xuất giải pháp.

* Con người review các thay đổi trước khi merge.

Điều này vẫn duy trì mô hình ****Human-in-the-loop****, nghĩa là AI không trực tiếp thay đổi source code mà không có sự kiểm tra của con người. Pull Request được tạo ra vẫn cần được developer review và approve.

Theo mình, đây là một cách tiếp cận hợp lý vì vừa tận dụng được sức mạnh của AI, vừa duy trì sự kiểm soát của con người đối với chất lượng code và tính an toàn của hệ thống.

## Best Practices từ AWS

AWS cũng đưa ra một số khuyến nghị khi triển khai cách tiếp cận này:

* Áp dụng nguyên tắc ****Least Privilege**** cho GitHub App và Personal Access Token.

* Chỉ bật những permissions mà AI thực sự cần sử dụng.

* Luôn yêu cầu con người review Pull Request trước khi merge.

* Theo dõi hoạt động của Agent thông qua Amazon CloudWatch.

* Xác thực Webhook bằng HMAC để ngăn chặn các request giả mạo.

Đây đều là những nguyên tắc quan trọng để duy trì tính bảo mật khi đưa nhiều automation hơn vào quy trình phát triển.

## Kết luận

Theo mình, AWS DevOps Agent cho thấy một hướng phát triển khá thú vị của DevOps trong tương lai.

Trước đây, AI chủ yếu được sử dụng để hỗ trợ developer viết code. Hiện nay, AI đang bắt đầu tham gia vào nhiều phần hơn trong vòng đời phát triển phần mềm, bao gồm theo dõi CI/CD pipeline, phân tích log, xác định nguyên nhân lỗi và đề xuất Pull Request để khắc phục vấn đề.

Mặc dù công nghệ này chưa thể hoàn toàn thay thế vai trò của DevOps Engineer hay Software Engineer, nó có thể giúp giảm đáng kể thời gian xử lý sự cố và cho phép đội ngũ kỹ thuật tập trung nhiều hơn vào việc phát triển các tính năng mới.

![AWS DevOps Agent Architecture](images/3-BlogsPosted/blog1.png)

## Tài liệu tham khảo

****AWS Blog:****

[AWS DevOps Agent and GitHub CI/CD Troubleshooting](https://aws.amazon.com/vi/blogs/mt/automate-ci-cd-troubleshooting-with-aws-devops-agent-and-github/?fbclid=IwY2xjawUTrv9wZG9mAWV4dG4DYWVtAjEwAGJyaWQRMUlSbHJNYTFyZ25OVXRySzlzcnRjBmFwcF9pZBAyMjIwMzkxNzg4MjAwODkyAAEeK5VwKabHemtPovw3AsP3aBI7kLFROu1OC4KgnJY3DQaO56vyO7bxCPGKiTQ_aem_6a_p6f8MRgNteopw3DcC9Q)
