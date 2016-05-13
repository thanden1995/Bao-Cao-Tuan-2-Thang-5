#Tìm hiểu giao thức HTTP
##Mục Lục
###[1. Giới thiệu sơ lược về HTTP](#1)
###[1.1 Khái niệm của HTTP](#11)
###[1.2 Đặc điểm của HTTP](#12)
###[1.3 Cấu trúc của HTTP](#13)
###[2. Định dạng HTTP request và HTTP resonse](#2)
###[2.1 Phương thức HTTP request](#21)
###[2.2 Phương thức HTTP response](#22)
###[3. Lời cảm ơn](#3)

<a name="1"></a>
##1. Giới thiệu sơ lược về HTTP:

<a name="11"></a>
###1.1 Khái niệm của HTTP:
Hypertext Transfer Protocol (HTTP) là một giao thức không trạng thái (stateless) nằm ở tầng ứng dụng, đảm nhiệm việc giao tiếp giữa các hệ thống phân tán với nhau, và nó là nền tảng của web. 

<a name="12"></a>
###1.2 Đặc điểm của HTTP:
- HTTP có những đặc điểm nổi bật sau:
<ul>
<li>HTTP là giao thức connectionless(kết nối không liên tục)**: HTTP client khởi tạo một yêu cầu HTTP sau đó ngắt kết nối đến Server và chờ đợi phản hồi. Server sẽ xử lý yêu cầu và tái thiết lập kết nối với client để gửi phản hồi trở lại.</li>
<li>HTTP là một phương tiện độc lập**:   Bất kỳ loại dữ liệu nào cũng có thể được gửi bởi HTTP miễn là Server và Client biết cách để kiểm soát nội dung dữ liệu.  Client cũng như Server phải xác định kiểu nội dung bằng cách sử dụng kiểu MIME thích hợp.</li>
<li>HTTP là giao thức stateless**: Như đã được đề cập ở trên, HTTP là connectionless và nó biến HTTP trở thành một giao thức Stateless. Server và Client nhận thức nhau chỉ trong một request.</li>
</ul>

<a name="13"></a>
###1.3 Cấu trúc của HTTP

- Giao thức HTTP là một giao thức Yêu cầu/Phản hồi dựa trên cấu trúc Client/Server, nơi mà các trình duyệt web, các thiết bị tìm kiếm,… hoạt động như các Client, và các Server web hoạt động như một Server.
<ul>
<li>Client gửi một yêu cầu tới Server theo dạng URI, phiên bản giao thức, một thông báo MIME chứa các request modifiers, thông tin Client, và nội dung đối tượng có thể qua một kết nối TCP/IP.</li>
<li>Server phản hồi với một dòng trạng thái, bao gồm phiên bản giao thức của thông báo và một code thành công hoặc lỗi, theo sau bởi một thông báo MIME chứa thông tin Server, thông tin thực thể đa phương tiện và nội dung đối tượng có thể.</li>
</ul>

<a name="2"></a>
##2. Định dạng HTTP request và HTTP resonse

<a name="21"></a>
###2.1 Phương thức HTTP request
- Để bắt đầu trao đổi dữ liệu, phía client khởi tạo một HTTP session bằng cách mở một kết nối TCP đến HTTP server sau đó gửi request đến server này. Request có thể được tạo bằng nhiều cách, trực tiếp khi người dùng nhấp vào một liên kết trên trình duyệt hoặc gián tiếp, ví dụ như một video được đính kèm trong một website và việc request đến website này sẽ dẫn đến một request tới video ấy.

<img src=http://imgur.com/UdYzcOM.png>

- Bắt đầu của HTTP Request sẽ là dòng Request-Line bao gồm 3 thông tin đó là:
<ul>
<li>Method: là phương thức mà HTTP Request này sử dụng, thường là GET, POST, ngoài ra còn một số phương thức khác như HEAD, PUT, DELETE, OPTION, CONNECT. Trong ví dụ trên là GET.</li>
<li>URI: là địa chỉ định danh của tài nguyên. Trong tường hợp này URI là / - tức request cho tài nguyên gốc, nếu request không yêu cầu một tài nguyên cụ thể, URI có thể là dấu *.</li>
<li>HTTP version: là phiên bản HTTP đang sử dụng, ở đây là HTTP 1.1.</li>
</ul>
- Tiếp theo là các trường request-header, cho phép client gửi thêm các thông tin bổ sung về thông điệp HTTP request và về chính client. Một số trường thông dụng như:
<ul>
<li>Accept: loại nội dung có thể nhận được từ thông điệp response. Ví dụ: text/plain, text/html…</li>
<li>Accept-Encoding: các kiểu nén được chấp nhận. Ví dụ: gzip, deflate, xz, exi…</li>
<li>Connection: tùy chọn điều khiển cho kết nối hiện thời. Ví dụ: keep-alive, Upgrade…</li>
<li>Cookie: thông tin HTTP Cookie từ server.</li>
<li>User-Agent: thông tin về user agent của người dùng.</li>
</ul>
**Phương thức GET và POST**

Hai phương thức được sử dụng nhiều nhất trong HTTP request là GET và POST

Với GET, câu truy vấn sẽ được đính kèm vào đường dẫn của HTTP request. Ví dụ: /?username=”abc”&password=”def”

Một số đặc điểm của phương thức GET:
<ul>
<li>GET request có thể được cached, bookmark và lưu trong lịch sử của trình duyệt.</li>
<li>GET request bị giới hạn về chiều dài, do chiều dài của URL là có hạn.</li>
<li>GET request không nên dùng với dữ liệu quan trọng, chỉ dùng để nhận dữ liệu.</li>
</ul>
Ngược lại, với POST thì câu truy vấn sẽ được gửi trong phần message body của HTTP request, một số đặc điểm của POST như:
<ul>
<li>POST không thể, cached, bookmark hay lưu trong lịch sử trình duyệt.</li>
<li>POST không bị giới hạn về độ dài.</li>
</ul>

Ngoài GET và POST, HTTP request còn có thể có một số phương thức khác như:
<ul>
<li>HEAD:; giống như GET nhưng chỉ gửi về HTTP header.</li>
<li>PUT: tải lên một mô tả về URI định trước.</li>
<li>DELETE: xóa một tài nguyên định trước.</li>
<li>OPTIONS: trả về phương thức HTTP mà server hỗ trợ.</li>
<li>CONNECT: chuyển kết nối của HTTP request thành một kết nối HTTP tunnel.</li>
</ul>

<a name="22"></a>
###2.2 Phương thức HTTP response
Cấu trúc HTTP response gần giống với HTTP request, chỉ khác nhau là thay vì Request-Line, thì HTTP có response có Status-Line. Và giống như Request-Line, Status-Line cũng có ba phần như sau:
<ul>
<li>HTTP-version: phiên bản HTTP cao nhất mà server hỗ trợ.</li>
<li>Status-Code: mã kết quả trả về.</li>
<li>Reason-Phrase: mô tả về Status-Code.</li>
</ul>

<img src=http://img.prntscr.com/img?url=http://i.imgur.com/bX716rJ.png>



*Một số loại Status-Code thông dụng mà server trả về cho client như sau:

- 1xx: information Message:** các status code này chỉ có tính chất tạm thời, client có thể không quan tâm.

- 2xx Successful:** khi đã xử lý thành công request của client, server trả về status dạng này:
<ul>
<li>200 OK: request thành công.</li>
<li>202 Accepted: request đã được nhận, nhưng không có kết quả nào trả về, thông báo cho client tiếp tục chờ đợi.</li>
<li>204 No Content: request đã được xử lý nhưng không có thành phần nào được trả về.</li>
<li>205 Reset: giống như 204 nhưng mã này còn yêu câu client reset lại document view.</li>
<li>206 Partial Content: server chỉ gửi về một phần dữ liệu, phụ thuộc vào giá trị range header của client đã gửi.</li>
</ul>
- 3xx Redirection:** server thông báo cho client phải thực hiện thêm thao tác để hoàn tất request:
<ul>
<li>301 Moved Permanently: tài nguyên đã được chuyển hoàn toàn tới địa chỉ Location trong HTTP response.</li>
<li>303 See other: tài nguyên đã được chuyển tạm thời tới địa chỉ Location trong HTTP response.</li>
<li>304 Not Modified: tài nguyên không thay đổi từ lần cuối client request, nên client có thể sử dụng đã lưu trong cache.</li>
</ul>
- 4xx Client error:** lỗi của client:
<ul>
<li>400 Bad Request: request không đúng dạng, cú pháp.</li>
<li>401 Unauthorized: client chưa xác thực.</li>
<li>403 Forbidden: client không có quyền truy cập.</li>
<li>404 Not Found: không tìm thấy tài nguyên.</li>
<li>405 Method Not Allowed: phương thức không được server hỗ trợ.</li>
</ul>
- 5xx Server Error:** lỗi của server:
<ul>
<li>500 Internal Server Error: có lỗi trong quá trình xử lý của server.</li>
<li>501 Not Implemented: server không hỗ trợ chức năng client yêu cầu.</li>
<li>503: Service Unavailable: Server bị quá tải, hoặc bị lỗi xử lý.</li>
</ul>

<a name="3"></a>
##2. Lời cảm ơn:
Bài viết còn nhiều thiếu sót mong nhận được những ý kiến đóng góp từ mọi người. Cảm ơn bạn đã dành thời gian cho bài viết này!
Mọi ý kiến đóng góp liên hệ email: thanden1995@gmail.com
