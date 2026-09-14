---

title: "Blog 2"

date: 2026-09-13

weight: 2

chapter: false

pre: " <b> 3.2. </b> "

---

# Xây dựng AI Agent cho bài toán phân loại theo lĩnh vực ở quy mô lớn

Xin chào mọi người! Khi nhắc đến AI, có lẽ nhiều người sẽ nghĩ ngay đến ChatGPT hoặc các chatbot có khả năng trả lời câu hỏi. Tuy nhiên, xu hướng AI hiện nay đang dần chuyển sang một khái niệm mới: ****AI Agent**** — những hệ thống AI không chỉ tạo câu trả lời mà còn có thể phân tích dữ liệu, sử dụng công cụ, đưa ra quyết định và giải thích lý do cho những quyết định đó.

Trong một bài viết gần đây trên AWS Blog, mình đã tìm hiểu về cách AWS xây dựng một hệ thống AI Agent chuyên cho ****phân loại dữ liệu theo lĩnh vực**** bằng cách kết hợp Amazon Bedrock với các dịch vụ serverless trên AWS. Điều mình thấy thú vị là bài toán này không chỉ liên quan đến AI, mà còn thể hiện cách AWS xây dựng một kiến trúc có khả năng mở rộng, dễ quản lý và có thể áp dụng cho nhiều ngành nghề khác nhau.

## Bài toán AWS muốn giải quyết

Ở nhiều lĩnh vực như y tế, tài chính hay khu vực công, dữ liệu thường tồn tại dưới dạng văn bản tự do. Những tài liệu này cần được phân loại thành các mã hoặc danh mục tiêu chuẩn để phục vụ báo cáo, thống kê hoặc tuân thủ các quy định.

Trước đây, công việc này chủ yếu được thực hiện thủ công hoặc dựa trên các hệ thống rule-based. Tuy nhiên, khi lượng dữ liệu ngày càng tăng và các quy định thường xuyên thay đổi, những phương pháp này dần bộc lộ nhiều hạn chế về tốc độ xử lý, khả năng mở rộng và chi phí vận hành.

Đó cũng là lý do AWS đề xuất xây dựng một AI Agent có khả năng tự động phân tích dữ liệu, tra cứu thêm thông tin khi cần và đưa ra kết quả phân loại kèm theo lời giải thích.

## AI Agent khác gì so với Chatbot?

Một chatbot thông thường sẽ nhận câu hỏi và tạo câu trả lời dựa trên kiến thức của mô hình ngôn ngữ.

Trong khi đó, AI Agent có khả năng thực hiện nhiều bước trước khi đưa ra kết quả, chẳng hạn như:

* Phân tích dữ liệu đầu vào.

* Tra cứu thông tin từ các nguồn đáng tin cậy.

* Tổng hợp và đánh giá kết quả.

* Đưa ra quyết định cùng với ****Confidence Score****.

* Giải thích quá trình suy luận và lưu lại toàn bộ quy trình xử lý.

Khả năng ****reasoning**** và ****tool use**** chính là yếu tố tạo nên sự khác biệt giữa AI Agent và chatbot truyền thống.

## Kiến trúc AWS đề xuất

Trong bài viết, AWS xây dựng hệ thống theo mô hình serverless với một số dịch vụ quen thuộc:

* ****Amazon S3**** lưu trữ dữ liệu đầu vào.

* ****Amazon EventBridge**** phát hiện khi có dữ liệu mới được tải lên.

* ****AWS Lambda**** xử lý và chia nhỏ dữ liệu.

* ****Amazon SQS**** quản lý hàng đợi để xử lý bất đồng bộ.

* ****Amazon Bedrock**** cung cấp các mô hình AI phục vụ quá trình suy luận.

* ****Amazon DynamoDB**** lưu kết quả phân loại cùng với quá trình suy luận và các nguồn tham khảo.

* ****Amazon CloudWatch**** theo dõi hiệu năng, chi phí và hoạt động của AI Agent.

Thay vì xử lý toàn bộ dữ liệu trên một máy chủ duy nhất, kiến trúc này tận dụng các dịch vụ serverless để tự động mở rộng khi khối lượng dữ liệu tăng lên.

## Quy trình hoạt động

Quy trình xử lý có thể được tóm tắt như sau:

1. Người dùng tải dữ liệu lên Amazon S3.

2. EventBridge phát hiện sự kiện và kích hoạt Lambda.

3. Lambda chia dữ liệu thành các nhóm nhỏ và đưa vào Amazon SQS.

4. Một Lambda khác đọc từng nhóm dữ liệu và gửi yêu cầu đến AI Agent.

5. AI Agent sử dụng Amazon Bedrock để thực hiện quá trình suy luận và có thể gọi thêm các công cụ như web search hoặc Amazon Bedrock Knowledge Bases để lấy thông tin trước khi đưa ra kết quả.

6. Kết quả được lưu vào DynamoDB với các thông tin như:

   * Classification Code.

   * Description.

   * Confidence Score.

   * Reasoning process.

   * Reference sources.

7. CloudWatch ghi nhận các chỉ số như thời gian xử lý, số lượng token sử dụng và chi phí để hỗ trợ việc theo dõi và tối ưu hệ thống.

Một điểm đáng chú ý của kiến trúc này là AI không chỉ trả về kết quả cuối cùng mà còn lưu lại toàn bộ quá trình suy luận. Điều này giúp tăng tính minh bạch và hỗ trợ việc kiểm tra khi cần thiết.

## Điều mình thấy ấn tượng nhất

Sau khi đọc bài viết, điều khiến mình ấn tượng không phải là việc AWS sử dụng một mô hình AI mới, mà là cách họ thiết kế toàn bộ quy trình xử lý.

Thay vì chỉ để AI đưa ra câu trả lời, hệ thống còn chú trọng đến những yếu tố rất quan trọng trong môi trường doanh nghiệp như:

* Khả năng mở rộng nhờ kiến trúc serverless.

* Tính minh bạch thông qua reasoning và nguồn tham khảo.

* Audit Trail cho từng quyết định.

* Theo dõi hiệu năng và chi phí bằng CloudWatch.

Theo mình, đây là những yếu tố quan trọng giúp AI có thể được ứng dụng trong các lĩnh vực yêu cầu độ tin cậy cao như y tế, tài chính hay khu vực công.

## Kết luận

AI Agent đang mở ra một cách tiếp cận mới trong việc xây dựng các ứng dụng AI trên nền tảng đám mây. Thay vì chỉ đóng vai trò như một chatbot, AI giờ đây có thể phân tích dữ liệu, sử dụng công cụ, tra cứu thông tin, giải thích quyết định và hỗ trợ con người xử lý những bài toán phức tạp hơn.

Qua bài viết này, mình nhận thấy việc kết hợp ****Amazon Bedrock**** với các dịch vụ serverless như ****Lambda, SQS, DynamoDB và EventBridge**** không chỉ giúp xây dựng một hệ thống AI có khả năng mở rộng mà còn đáp ứng được các yêu cầu về tính minh bạch, quản trị và vận hành trong môi trường thực tế.

Đây là một hướng phát triển rất đáng chú ý đối với những ai đang tìm hiểu về AI trên AWS, đặc biệt trong bối cảnh AI Agent đang trở thành một xu hướng mới của ngành công nghệ.

![Domain-Specific Classification Architecture](images/3-BlogsPosted/blog2.png)

## Tài liệu tham khảo

**AWS Blog:**

[Building AI agents for domain-specific classification at scale](https://aws.amazon.com/vi/blogs/publicsector/building-ai-agents-for-domain-specific-classification-at-scale/?fbclid=IwY2xjawUTseBwZG9mAWV4dG4DYWVtAjEwAGJyaWQRMUlSbHJNYTFyZ25OVXRySzlzcnRjBmFwcF9pZBAyMjIwMzkxNzg4MjAwODkyAAEePI-I1hySd2uaqr3S4zH3-fVZZJWDoGgvvdlYX-6PjofPQvqLBL7VgR-yAuU_aem_cZYA-3tPQyL9WXPVIzO-Ig)
