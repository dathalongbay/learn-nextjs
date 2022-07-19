# Pre-rendering and Data Fetching

Trong bài học này, chúng ta sẽ tìm hiểu cách tìm nạp dữ liệu blog bên ngoài vào ứng dụng của mình. Chúng tôi sẽ lưu trữ nội dung blog trong file system (hệ thống tệp), nhưng nó sẽ hoạt động nếu nội dung được lưu trữ ở nơi khác (ví dụ: cơ sở dữ liệu).
#### Bạn sẽ học được gì trong bài học này
Trong bài học này, bạn sẽ tìm hiểu về: 
- Tính năng kết xuất trước của Next.js (pre-rendering feature).
- Hai hình thức kết xuất trước: Tạo tĩnh và Kết xuất phía máy chủ. 
- Tạo tĩnh có dữ liệu và không có dữ liệu.
- getStaticProps và cách sử dụng nó để nhập dữ liệu blog bên ngoài vào trang index
- Một số thông tin hữu ích trên getStaticProps.



## Setup
Nếu bạn đang tiếp tục bài học trước, bạn có thể bỏ qua trang này. Nhấp vào nút bên dưới để chuyển đến trang tiếp theo.
#### Download Starter Code (Optional)
Nếu bạn KHÔNG tiếp tục bài học trước, bạn có thể tải xuống, cài đặt và chạy mã khởi động cho bài học này bên dưới. Thao tác này thiết lập một thư mục blog nextjs sao cho giống với kết quả của bài học trước.
Một lần nữa, điều này KHÔNG cần thiết nếu bạn vừa hoàn thành bài học trước.
```
npx create-next-app nextjs-blog --use-npm --example "https://github.com/vercel/next-learn/tree/master/basics/data-fetching-starter"
```
Sau đó làm theo hướng dẫn trong command line (cd vào thư mục và khởi động máy chủ phát triển).  
Bạn cũng nên cập nhật các tệp sau:  
```
public/images/profile.jpg with your photo (Recommended: 400px width/height).  
const name = '[Your Name]' in components/layout.js với tên bạn.  
<p>[Your Self Introduction]</p> in pages/index.js với giới thiệu về bản thân bạn
```
## Pre-rendering



