#Tìm hiểu dịch vụ DNS
##[Mục lục ] (#mucluc)
###[1. Khái niệm DNS: ] (#1)
###[2. Chức năng của DNS:](#2)
###[3. Cơ chế hoạt động của DNS:](#3)
###[4. Cấu trúc hệ thống DNS: ](#4)
###[4.1. Phân loại tên miền DNS:](41)
###[4.2. Phân loại DNS Server:](#42)
###[5. Tìm hiểu DNS Zone và ý nghĩa các bản ghi trong Zone: ](#5)
###[6. Cách cài đặt dịch vụ DNS: ](#6)
###[7. Lời cảm ơn](#7)

<a name="1"></a>
##1. Sơ lược về khái niệm DNS:
- DNS (Domain Name Service hay Domain Name System) là một hệ cơ sở dữ liệu phân tán dùng để ánh xạ giữa các tên miền và các địa chỉ IP. DNS đưa ra một phương pháp đặc biệt để duy trì và liên kết các ánh xạ này trong một thể thống nhất. Trong phạm vi lớn hơn, các máy tính kết nối với internet sử dụng DNS để tạo địa chỉ liên kết dạng URL (Universal Resource Locators). Theo phương pháp này, mỗi máy tính sẽ không cần sử dụng địa chỉ IP cho kết nối mà chỉ cần sử dụng tên miền (domain name) để truy vấn đến kết nối đó.
- Nói một cách đơn giản hơn thì nó là hệ thống phân giải tên miền cho phép máy tính truy vấn không cần thông qua địa chỉ IP mà bằng tên miền.
- Để một hệ thống DNS hoạt động cần có 2 thành phần đó là DNS Server và DNS Client.
<ul>
<li>DNS Server dùng để phân giải tên miền ra địa chỉ IP và ngược lại.</li>
<li>DNS Client dùng để phân giải tên miền cho máy người dùng</li> 
</ul>
-DNS sử dụng port giao tiếp là 53.

<a name="2"></a>
##2. Chức năng của DNS:
- DNS có chức năng chính là phân giải tên miền. Mỗi Website có một tên (là tên miền hay đường dẫn URL:Uniform Resource Locator) và một địa chỉ IP. Khi mở một trình duyệt Web và nhập tên website, trình duyệt sẽ đến thẳng website mà không cần phải thông qua việc nhập địa chỉ IP của trang web. Quá trình dịch tên miền thành địa chỉ IP để cho trình duyệt hiểu và truy cập được vào website là công việc của một DNS server. Các DNS trợ giúp qua lại với nhau để dịch địa chỉ IP thành tên và ngược lại. Người sử dụng chỉ cần nhớ tên, không cần phải nhớ địa chỉ IP. 

<a name="3"></a>
##3. Cơ chế hoạt động của DNS:
<ul>
<li>Bước 1: Trên máy người dùng truy cập Website: htttp://google.com.vn bằng IE. Lập tức IE sẽ nhờ DNS Client phân giải tên miền google.com.vn sang địa chỉ IP.</li>
<li>Bước 2: Gói tin của DNS client sẽ được chuyển xuống tầng Transport và đóng gói giao thức UDP. Sau đó chuyển xuống Network.</li>
<li>Bước 3: Network sẽ đóng IP nguồn là IP máy tính, IP đich sẽ là IP DNS Server.</li>
<li>Bước 4: Đã có IP nguồn và IP đích, dữ liệu sẽ chuyển xuống tầng bên dưới và truyền tới đúng DNS Server.</li> 
<li>Bước 5: Khi yêu cầu gửi tới DNS Server nó sẽ tìm trong cơ sở dữ liệu của mình xem tền miền đó ứng địa chỉ IP của Server Website nào.</li>
<li>Bước 6: Sau khi tìm được nó sẽ gửi lại cho máy có DNS Client yêu cầu.</li>
<li>Bước 7: Nếu không tìm được tên miền trong cơ sở dữ liệu của nó, DNS Server sẽ gửi một bản tin đến DNS Server khác để hỏi tên miền bằng giao thức TCP. Sau khi nhận về dữ liệu về tên miền DNS Server sẽ cập nhật dữ liệu rồi chuyển tên miền được yêu cầu về cho máy DNS Client yêu cầu</li>
<li>Bước 8: IP của Server Website đã sẵn sàng cho tầng Network đóng vào gói dữ liệu của gói tin truy cập Website.</li>
</ul>


<a name="4"></a>
##4. Cấu trúc hệ thống DNS:

<a name="41"></a>
###4.1. Phân loại tên miền DNS:
- Hệ thống tên miền DNS được phân loại và sắp xếp theo mô hình cây logic như sau:

<img src="https://cloud.githubusercontent.com/assets/18635054/15224759/5a5a0c76-18a5-11e6-82e1-cd14d4fce76a.png">


<ul>
<li>Gốc (Domain root): Nó là đỉnh của nhánh cây của tên miền. Nó có thể biểu diễn đơn giản chỉ là dấu chấm “.”</li>
<li>Tên miền cấp một (Top-level-domain) : gồm vài kí tự xác định một nước, khu vưc hoặc tổ chức. Nó đươc thể hiện là “.com” , “.edu” ….</li>
<li>Tên miền cấp hai (Second-level-domain): Nó rất đa dạng rất đa dạng có thể là tên một công ty, một tổ chức hay một cá nhân.</li>
<li>Tên miền cấp nhỏ hơn (Subdomain): Chia thêm ra của tên miền cấp hai trở xuống thường được sử dụng như chi nhánh, phòng ban của một cơ quan hay chủ đề nào đó.</li>
</ul>
- Theo đó, khi một DNS client truy vấn một tên miền nó sẽ đi lần lượt từ root xuống dưới để đến DNS quản lý tên miền cần truy vấn.

- Bao gồm các loại tên miền:
<ul>
<li>Com     :    Tên miền này được dùng cho các tổ chức thương mại.</li>
<li>Edu     :    Tên miền này được dùng cho các cơ quan giáo dục, trường học.</li>
<li>Net     :    Tên miền này được dùng cho các tổ chức mạng lớn.</li>
<li>Gov     :    Tên miền này được dùng cho các tổ chức chính phủ.</li>
<li>Org     :    Tên miền này được dùng cho các tổ chức khác.</li>
<li>Int     :    Tên miền này dùng cho các tổ chức quốc tế.</li>
<li>Info    :    Tên miền này dùng cho việc phục vụ thông tin.</li>
<li>Arpa    :     Tên miền ngược.</li>
<li>Mil     :    Tên miền dành cho các tổ chức quân sự, quốc phòng.</li>
<li>Mã các nước trên thế giới tham gia vào mạng internet, các quốc gia này được qui định bằng hai chữ cái theo tiêu chuẩn ISO-3166 .Ví dụ : Việt Nam là .vn, Singapo là sg….</li>
</ul>

<a name="42"></a>
###4.2. Phân loại DNS Server:
- Primary Server : 
<ul>
<li>Được tạo khi ta add một Primary Zone mới thông qua New Zone Wizard. 
<li>Thông tin về tên miền do nó quản lý được lưu trữ tại đây và sau đó có thể được chuyển sang cho các Secondary Server. 
<li>Các tên miền do Primary Server quản lý thì được tạo và sửa đổi tai Primary Server và được cập nhật đến các Secondary Server.
</ul>

- Secondary Server : 
<ul>
<li>DNS được khuyến nghị nên sử dụng ít nhất là hai DNS Server để lưu cho mỗi một Zone. Primary DNS Server quản lý các Zone và Secondary Server sử dụng để lưu trữ dự phòng cho Primary Server. Secondary DNS Server được khuyến nghị dùng nhưng không nhất thiết phải có.</li>
<li>Secondary Server được phép quản lý domain nhưng dữ liệu về tên miền (domain), nhưng Secondary Server không tạo ra các bản ghi về tên miền (domain) mà nó lấy về từ Primary Server.</li>
<li>Khi lượng truy vấn Zone tăng cao tại Primary Server thì nó sẽ chuyển bớt tải sang cho Secondary Server .Hoặc khi Primary Server gặp sự cố không hoạt động được thì Secondary Server sẽ hoạt động thay thế cho đến khi Primary Server hoạt động trở lại.</li> 
</ul>
- Caching-only Server : 
<ul>
<li>Tất cả các DNS Server đều có khả năng lưu trữ dữ liệu trên bộ nhớ cache của máy để trả lời truy vấn một cách nhanh chóng. Nhưng hê thống DNS còn có một loại Caching-only Server.</li> 
<li>Loại này chỉ sử dụng cho việc truy vấn, lưu giữ câu trả lời dựa trên thông tin có trên cache của máy và cho kết quả truy vấn. Chúng không hề quản lý một domain nào và thông tin mà nó chỉ giới hạn những gì được lưu trên cache của Server.</li> 
<li>Lúc ban đầu khi Server bắt đầu chạy thì nó không lưu thông tin nào trong cache. Thông tin sẽ được cập nhật theo thời gian khi các Client Server truy vấn dịch vụ DNS. Nếu sử dụng kết nối mạng WAN tốc độ thấp thì việc sử dụng caching-only DNS Server là giải pháp hữu hiệu cho phép giảm lưu lượng thông tin truy vấn trên đường truyền.</li> 
<li>Caching-only có khả năng trả lời các câu truy vấn đến Client. Nhưng không chứa Zone nào và cũng không có quyền quản lý bất kì domain nào. Nó sử dụng bộ cache của mình để lưu các truy vấn của DNS của Client. Thông tin sẽ được lưu trong cache để trả lời các truy vấn đến Client.</li>
</ul>
- Stub Server : 
<ul>
<li>Là DNS Server chỉ chứa danh sách các DNS Server đã được authoritative từ Primary DNS.</li>
<li>Sử dụng stub có thể tăng tốc độ phân giải tên và dễ quản lý.</li>
</ul>

<a name="5"></a>
##5. Tìm hiểu DNS Zone và ý nghĩa các bản ghi trong Zone:
- Trong DNS Server có 2 thành phần chính là:
<ul>
<li>Forward lookup zone sẽ phân giải các bản ghi từ Tên sang địa chỉ IP.</li>
<li>Reverse lookup zone sẽ phân giải các bản ghi từ IP sang Tên.</li>
</ul>
- Ý nghĩa các bản ghi:

+ SOA: (Start of authority) chỉ ra rằng máy chủ Name Server là nơi cung cấp thông tin tin cậy từ dữ liệu có trong zone. Cú pháp của record SOA:
<ul>
<li>Serial : Áp dụng cho mọi dữ liệu trong zone và là 1 số nguyên. Ở đây họ sử dụng đinh dạng YYYYMMDDNN, trong đó YYYY là năm, MM là tháng, DD là ngày, NN số lần sửa đổi dữ liệu zone trong ngày. Vd: 2011071001</li>
<li>Refresh: Chỉ ra khoảng thời gian máy chủ Secondary kiểm tra dữ liệu zone trên máy Primary để cập nhật nếu cần.</li>
<li>Retry: nếu máy chủ Secondary không kết nối được với máy chủ Primary theo thời hạn mô tả trong refresh.</li>
<li>Expire : Nếu sau khoảng thời gian này mà máy chủ Secondary không kết nối được với máy chủ Primary thì dữ liệu zone trên máy Secondary sẽ bị quá hạn.</li>
<li>Minimum TTL: TTL viết tắt của time to live. Giá trị này áp dụng cho mọi record trong zone và được đính kèm trong thông tin trả lời một truy vấn. Mục đích của nó là chỉ ra thời gian mà các máy chủ name server khác cache lại thông tin trả lời.</li>
</ul>
+ NS (Name Server): Mỗi name server cho zone sẽ có một NS record. Cú pháp khai báo:
<ul>
<li>[tên-domain] IN NS [DNS-Server_name]</li>
</ul>
+ SRV: Service – Được sử dụng bởi Active Directory để lưu thông tin về vị trí của Domain Controllers
+ AAAA: Host – Phân giải tên máy thành địa chỉ IP (IPv6)
+ SRV: Service – Được sử dụng bởi Active Directory để lưu thông tin về vị trí của Domain Controllers
+ AAAA: Host – Phân giải tên máy thành địa chỉ IP (IPv6)
+ A (Address) ánh xạ tên máy(hostname) vào địa chỉ IP. 
+ MX: Mail exchange – Chỉ đến mail Server trong domain.
+ CNAME (Alias): Canonical name – Cho phép một host có thể có nhiều tên.
+ PTR (pointer) dùng để ánh xạ địa chỉ IP thành hostname. 

<a name="6"></a>
##6. Cách cài đặt dịch vụ DNS
- Để cài đặt DNS có thể xem [Cai dat DNS](http://vnlab.com.vn/cai-dat-va-cau-hinh-dns-server-tren-centos-7-0/)

<a name="7"></a>
##7. Lời cảm ơn
- Bài viết còn nhiều thiếu sót mong nhận được những ý kiến đóng góp từ mọi người.
Mọi chi tiết liên hệ email: thanden1995@gmail.com
