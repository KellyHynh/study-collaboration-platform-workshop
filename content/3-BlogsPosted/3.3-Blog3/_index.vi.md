---

title: "Blog 3"

date: 2026-09-13

weight: 3

chapter: false

pre: " <b> 3.3. </b> "

---

# Phân loại file bằng AI với AWS: Khi AI có thể đọc nội dung để tự động phân loại file

Xin chào mọi người!

Trong nhiều hệ thống xử lý tài liệu, việc phân loại file thường được thực hiện dựa trên tên file hoặc thư mục mà người dùng upload file vào. Cách tiếp cận này tương đối đơn giản nhưng cũng dễ xảy ra sai sót. Nếu tên file không tuân theo format được yêu cầu hoặc người dùng sử dụng một quy tắc đặt tên khác, hệ thống có thể phân loại file không chính xác.

Trong quá trình tìm hiểu về AWS, mình đã đọc được một bài viết khá thú vị về việc sử dụng AI để phân loại file dựa trên chính nội dung bên trong file thay vì chỉ dựa vào filename.

Bài viết có tên ****"Build AI-powered file classification with AWS Transfer Family"**** và được AWS giới thiệu vào tháng 9/2026. Điều mình thấy thú vị là giải pháp này không chỉ sử dụng AI mà còn kết hợp nhiều dịch vụ AWS thành một pipeline xử lý file hoàn chỉnh.

## Bài toán cần giải quyết

Hãy thử tưởng tượng một hệ thống mà các đối tác bên ngoài liên tục upload nhiều loại tài liệu khác nhau:

* Invoice

* Contract

* Purchase Order

* Report

* Các tài liệu PDF hoặc hình ảnh khác

Nếu hệ thống chỉ dựa vào tên file như:

`invoice_001.pdf`

`contract_002.pdf`

`report_003.pdf`

thì các file có thể được phân loại tương đối dễ dàng.

Tuy nhiên, trong thực tế, tên file có thể không tuân theo một quy tắc cố định. Ví dụ, một file invoice có thể đơn giản được đặt tên là:

`document_123.pdf`

Lúc này, việc phân loại dựa trên filename sẽ không còn đáng tin cậy.

Giải pháp được AWS giới thiệu là để hệ thống phân tích nội dung bên trong file và sử dụng AI để xác định file thuộc loại tài liệu nào.

## Kiến trúc AWS

Một trong những điểm mình thích ở kiến trúc này là AWS không sử dụng một service duy nhất để xử lý toàn bộ công việc. Thay vào đó, pipeline được chia thành nhiều thành phần.

****AWS Transfer Family**** cung cấp các giao thức truyền file để các hệ thống bên ngoài có thể gửi dữ liệu vào AWS.

File sau đó được lưu trữ trong ****Amazon S3****. Khi một file mới xuất hiện, ****Amazon EventBridge**** phát hiện sự kiện và gửi yêu cầu xử lý vào ****Amazon SQS****.

Việc sử dụng SQS giúp tách quá trình nhận file khỏi quá trình phân tích. Nếu có nhiều file được upload cùng lúc, hệ thống có thể xử lý chúng thông qua hàng đợi thay vì cố gắng xử lý tất cả ngay lập tức.

Sau đó, AWS Lambda lấy các message từ SQS và bắt đầu quá trình phân tích.

## AI đọc nội dung file như thế nào?

Đây là phần mình thấy thú vị nhất.

Không phải tất cả các file đều có thể được xử lý trực tiếp bằng cùng một quy trình. Với những tài liệu như PDF hoặc hình ảnh, hệ thống có thể sử dụng ****Amazon Textract**** để trích xuất thông tin từ tài liệu.

Sau khi có được nội dung cần thiết, ****Amazon Bedrock**** được sử dụng để phân tích thông tin và xác định loại tài liệu.

Ví dụ, thay vì chỉ nhìn thấy:

`document_123.pdf`

AI có thể phân tích những nội dung như:

`Invoice Number: INV-2026-001`

`Amount: $2,500`

`Due Date: ...`

Dựa trên những thông tin này, hệ thống có thể xác định đây là một ****Invoice****, ngay cả khi filename không thể hiện điều đó.

Đây là một điểm khác biệt quan trọng: hệ thống phân loại tài liệu dựa trên **nội dung** thay vì những metadata đơn giản như filename.

## Tại sao sử dụng Serverless?

Một điều mình nhận thấy khi tìm hiểu kiến trúc này là phần lớn pipeline sử dụng các dịch vụ managed hoặc serverless như ****Lambda, SQS, EventBridge và S3****.

Cách tiếp cận này rất phù hợp với những hệ thống xử lý file có workload không ổn định.

Ví dụ, trong điều kiện bình thường, hệ thống có thể chỉ nhận một vài file mỗi giờ. Tuy nhiên, tại một thời điểm nào đó, có thể có hàng nghìn file được upload.

Thay vì phải duy trì một server luôn chạy để chờ file, hệ thống có thể sử dụng mô hình event-driven:

>

****File được gửi lên → Event được tạo → Message được đưa vào queue → File được xử lý khi có tài nguyên.****

Cách thiết kế này giúp giảm sự phụ thuộc trực tiếp giữa các thành phần trong hệ thống và giúp kiến trúc dễ mở rộng hơn khi workload tăng.

**## Điều mình học được**

Điều mình thấy đáng chú ý nhất sau khi đọc bài viết không đơn giản là ****"AWS sử dụng AI để phân loại file."****

Điều quan trọng hơn là cách AI được đặt bên trong một kiến trúc cloud hoàn chỉnh.

****Amazon Bedrock**** chịu trách nhiệm cho việc phân tích và suy luận, trong khi các dịch vụ khác đảm nhận việc lưu trữ, truyền dữ liệu, điều phối sự kiện và xử lý bất đồng bộ.

Có thể hình dung workflow tổng thể như sau:

>

****S3 lưu dữ liệu → EventBridge phát hiện sự kiện → SQS quản lý queue → Lambda xử lý → Textract đọc tài liệu → Bedrock phân loại.****

Mỗi service giải quyết một vấn đề riêng, nhưng khi được kết hợp lại, chúng tạo thành một workflow tự động.

Qua đó, mình cũng nhận ra rằng khi xây dựng một ứng dụng AI thực tế, việc lựa chọn model chỉ là một phần của bài toán. Kiến trúc xung quanh model cũng quan trọng không kém.

## Kết luận

Bài viết về ****AI-powered file classification**** cho mình một góc nhìn khá thú vị về cách kết hợp Generative AI với kiến trúc Serverless và Event-driven trên AWS.

Thay vì xây dựng một server lớn để nhận file, đọc tài liệu và phân loại tất cả trong một quy trình duy nhất, AWS chia nhỏ hệ thống thành nhiều thành phần với trách nhiệm rõ ràng.

Đặc biệt, việc kết hợp ****Amazon Bedrock**** với ****Amazon Textract**** cho thấy AI có thể được sử dụng không chỉ để trò chuyện mà còn để xử lý những dữ liệu thực tế như tài liệu và hình ảnh.

Theo mình, đây là một hướng tiếp cận rất đáng tìm hiểu đối với những ai đang học AWS và muốn kết hợp ****Cloud + AI**** vào các bài toán thực tế.

![AI-powered File Classification Architecture](/images/3-BlogsPosted/blog3.png)

## Tài liệu tham khảo

****AWS Storage Blog:****

[Build AI-powered file classification with AWS Transfer Family](https://aws.amazon.com/vi/blogs/storage/build-ai-powered-file-classification-with-aws-transfer-family/)
