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
Trước khi chúng ta nói về tìm nạp dữ liệu, hãy nói về một trong những khái niệm quan trọng nhất trong Next.js: Pre-rendering Kết xuất trước.   
Theo mặc định, Next.js hiển thị trước mọi trang. Điều này có nghĩa là Next.js tạo trước HTML cho từng trang, thay vì để tất cả được thực hiện bởi JavaScript phía máy khách. Kết xuất trước có thể mang lại hiệu suất và SEO tốt hơn.  
Mỗi HTML được tạo được liên kết với mã JavaScript minimal cần thiết cho trang đó. Khi một trang được tải bởi trình duyệt, mã JavaScript của trang đó sẽ chạy và làm cho trang tương tác hoàn toàn. (Quá trình này được gọi là quá trình hydrat hóa.)  
#### Kiểm tra xem kết xuất trước có đang diễn ra không
Bạn có thể kiểm tra xem quá trình kết xuất trước có đang diễn ra hay không bằng cách thực hiện các bước sau:   
- Tắt JavaScript trong trình duyệt của bạn (đây là cách thực hiện trong Chrome) và… 
- Hãy thử truy cập trang này (kết quả cuối cùng của hướng dẫn này).
Bạn sẽ thấy rằng ứng dụng của bạn được hiển thị mà không có JavaScript. Đó là vì Next.js đã hiển thị trước ứng dụng thành HTML tĩnh, cho phép bạn xem giao diện người dùng ứng dụng mà không cần chạy JavaScript.
> Lưu ý: Bạn cũng có thể thử các bước trên trên máy chủ localhost, nhưng CSS sẽ không được tải nếu bạn tắt JavaScript.


Nếu ứng dụng của bạn là ứng dụng React.js thuần túy (không có Next.js), thì sẽ không có kết xuất trước, vì vậy bạn sẽ không thể thấy ứng dụng nếu bạn tắt JavaScript. Ví dụ:  
Bật JavaScript trong trình duyệt của bạn và xem trang này https://create-react-template.vercel.app/. Đây là một ứng dụng React.js đơn giản được xây dựng bằng Create React App  
Bây giờ, hãy tắt JavaScript và truy cập lại vào cùng một trang. Bạn sẽ không thấy ứng dụng nữa - thay vào đó, nó sẽ thông báo “Bạn cần bật JavaScript để chạy ứng dụng này”. Điều này là do ứng dụng không được hiển thị trước thành HTML tĩnh.

#### Summary: Pre-rendering vs No Pre-rendering
Đây là 1 đồ họa tóm tắt
![image](https://user-images.githubusercontent.com/6966136/179656119-32e4fc84-53bc-45e6-9c31-1fab61b80e1f.png)
![image](https://user-images.githubusercontent.com/6966136/179656142-0e23a234-1e91-47d8-bc8f-dfd03ade65ef.png)
Tiếp theo, hãy nói về hai hình thức kết xuất trước trong Next.js.
## Two Forms of Pre-rendering
Next.js có 2 hình thức của pre-rendering: Static Generation and Server-side Rendering. Sự khác biệt là khi nó tạo ra html cho 1 trang 
- Static Generation là hình thức pre-rendering mà tạo ra html trong 1 lần . The pre-rendered HTML được sử dụng lại sau mỗi lần request
- Server-side Rendering là pre-rendering method mà sinh ra html trên mỗi request
![image](https://user-images.githubusercontent.com/6966136/179657236-eee52822-7131-4ca8-9c55-999800dab589.png)
![image](https://user-images.githubusercontent.com/6966136/179657256-4bb216bb-6762-4ff3-aeb8-0d2f79e5e556.png)





