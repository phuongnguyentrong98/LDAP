## LDAP
I. Mục Lục :
II. LDAP :

1. Giới thiệu :
- Ldap : LDAP server là gì– là chữ viết tắt của từ Lightweight Directory Access Protocol. LDAP được phát triển dựa trên chuẩn X500. Đây là một chuẩn cho dịch vụ thư mục (Directory Service – DS) chạy trên nền tảng OSI.
- LDAP được coi là lightweight vì nó sử dụng gói tin trên không thấp, được xác định chính xác trên lớp TCP của danh sách giao thức TCP/IP còn X500 là hạng nặng vì là thuộc lớp giao thức ứng dụng, có chứa nhiều header hơn (các header của các layer tầng thấp hơn). Mặt khác, nếu bạn muốn đổi tên cho server thì có thể tìm hiểu name server là gì để hiểu phương thức đổi.
- LDAP là một giao thức truy cập vì vậy nó theo mô hình dạng cây (Directory Information Tree). LDAP là một giao thức truy cập dạng client/server.

2. Phương thức hoạt động : 
- LDAP hoạt động theo mô hình là client-server. Một hay nhiều LDAP server chứa các thông tin về cây thư mục (Directory Information Tree – DIT). Client kết nối đến server và gửi đi yêu cầu. Server phản hồi lại bằng chính nó hoặc trỏ tới LDAP server khác để client lấy được thông tin. Trình tự khi có kết nối với LDAP là:
	 - Connect (kết nối với LDAP): client sẽ mở kết nối tới LDAP server
	 -Bind (kiểu kết nối: ẩn danh hoặc đăng nhập xác thực): client gửi đi các thông tin xác thực
	 -Search (tìm kiếm): client gửi đi yêu cầu tìm kiếm
	 -Interpret search (xử lý tìm kiếm): server thực hiện việc xử lý tìm kiếm
	 -Result (kết quả): máy chủ trả lại kết quả cho client
	 -Unbind: client gửi đi yêu cầu đóng kết nối tới server
	 -Close connection (đóng kết nối): đóng đi kết nối từ server
	 
![mo hinh](https://user-images.githubusercontent.com/68736233/90852938-0322ad00-e3a3-11ea-9dea-fa2a38ae1577.png)


- Môi trường LDAP trải rộng hai vùng địa lý: SFO và AMS. Vì nó sẽ không thường xuyên xảy ra rằng người dùng trong SFO đang đăng nhập hoặc truy cập tài nguyên trong AMS, cây thư mục được chia thành hai phần, một phần dành cho SFO và một phần dành cho AMS . Mọi máy chủ trong mỗi địa lý sẽ biết cách truy cập thông tin trong phân vùng khác; nó sẽ chậm hơn một chút vì máy chủ từ xa cần để được truy cập.

![so do](https://user-images.githubusercontent.com/68736233/90852418-a07ce180-e3a1-11ea-9116-27cd209f8f57.png)

- Để cài đặt LDAP , các bạn hãy tham khảo : 

```
https://blog.cloud365.vn/ldap/LDAP-part-2-cai-dat-ldap-centos-7/
```

3. Tạo Dữ Liệu Trong LDAP :
- Để tạo dữ liệu trong LDAP, trước hết chúng ta sẽ tạo ra các file LDIF chứa các thông tin thuộc tính của các object, mỗi object sẽ được phân cách với nhau bởi một dòng trống. Trong file LDIF chúng ta có thể khai báo thông tin của một hoặc nhiều object cùng lúc điều được.
- Ví dụ ta sẽ khởi tạo thông tin của user1 trong file user1.ldif như sau:
	 dn: uid=user1,ou=sinhvien,dc=utc,dc=edu,dc=vn
	 uid: user1
	 cn: user1
	 givenName: user1
	 sn: user1
	 objectClass: person
	 objectClass: organizationalPerson
	 objectClass: inetOrgPerson
	 objectClass: posixAccount
	 objectClass: top
	 objectClass: shadowAccount
	 userPassword: kiemtra
	 shadowLastChange: 15360
	 shadowMin: 0
	 shadowMax: 99999
	 shadowWarning: 7
	 loginShell: /bin/bash
	 uidNumber: 602
	 gidNumber: 602
	 homeDirectory: /home/user1
	 gecos: User 1
	 
- Sau khi khởi tạo file LDIF chúng ta sẽ đưa dữ liệu vừa khởi tạo vào LDAP bằng cấu trúc lệnh như sau:

```
ldapadd -x -h 192.168.8.137 -D cn=Manager,dc=utc,dc=edu,dc=vn -w kiemtra -f user1.ldif
```

- Sau khi đã khởi tạo dữ liệu cho LDAP, ta có thể kiểm tra lại các dữ liệu đã được đưa vào LDAP bằng cấu trúc lệnh sau:

```
ldapsearch -x -h 192.168.8.137 –b dc=utc,dc=edu,dc=vn -D uid=user1,ou=sinhvien,dc=utc,dc=edu,dc=vn -w 
```

4. 1 số câu lệnh LDAP :
4.1 Liên kết ldap (ldapbind) :
- Sử dụng công cụ dòng lệnh ldapbind để xác thực với máy chủ thư mục. Bạn cũng có thể sử dụng ldapbind để tìm hiểu xem máy chủ có đang chạy hay không
- Câu lệnh : 

```
ldapbind [options]
```

- Lệnh này xác thực người dùng orcladmin đến máy chủ thư mục myhost đặt tại cổng 389.

4.2 Ldapsearch :
- Sử dụng công cụ dòng lệnh ldapsearch để tìm kiếm các mục nhập cụ thể trong một thư mục. Ldapsearch mở kết nối đến một thư mục, xác thực người dùng thực hiện thao tác, tìm kiếm mục nhập được chỉ định và in kết quả theo định dạng mà người dùng chỉ định.
- Câu lệnh :

```
ldapsearch  [options]  filter [attributes]
```

- vd  'ldapsearch -h myhost -p 389 -s base -b "ou=Manager,dc=cloud365,dc=local" \ "objectclass=*"'
- Lệnh này tìm kiếm máy chủ thư mục myhost, nằm ở cổng 389. Options (-s) là cơ sở và phần của thư mục được tìm kiếm là cơ sở DN (-b) được chỉ định.
- "objectclass = *" có nghĩa là các giá trị cho tất cả các lớp đối tượng của mục nhập được trả về. Không có thuộc tính nào được trả về vì chúng chưa được yêu cầu. Ví dụ giả định xác thực ẩn danh vì các tùy chọn xác thực không được chỉ định.

4.3 ldapadd :
- Sử dụng công cụ dòng lệnh ldapadd để thêm các mục nhập vào thư mục. Ldapadd mở một kết nối đến thư mục và xác thực người dùng. Sau đó, nó mở tệp LDIF được cung cấp dưới dạng đối số và thêm liên tiếp từng mục nhập trong tệp.
- Câu lệnh :

```
ldapadd [options] [-f LDIF-filename]
```

-vd : ' ldapadd -h myhost -p 389 -D "cn=orcladmin" -w welcome -f jhay.ldif '
- Sử dụng lệnh này, người dùng orcladmin xác thực vào thư mục myhost, nằm ở cổng 389. Sau đó, lệnh mở tệp jhay.ldif và thêm nội dung của tệp vào thư mục. Ví dụ: tệp có thể thêm mục nhập uid = jhay, cn = Nhân sự, cn = acme, dc = com và các lớp đối tượng và thuộc tính của nó.

4.4 ldapdelete :
- Sử dụng công cụ dòng lệnh ldapdelete để xóa các mục nhập lá khỏi thư mục. Ldapdelete mở kết nối đến máy chủ thư mục và xác thực người dùng. Sau đó, nó sẽ xóa các mục nhập đã chỉ định.
- Câu lệnh : 

```
ldapdelete [options] "entry DN"
```

- vd : ldapdelete -h myhost -p 389 -D "cn=orcladmin" -w welcome \ "ou=Manager,dc=cloud365,dc=local"
- Lệnh này xác thực người dùng orcladmin vào thư mục myhost, sử dụng mật khẩu , sau đó, nó xóa mục nhập "ou=Manager,dc=cloud365,dc=local"

4.5 ldapmodify :
- Sử dụng công cụ dòng lệnh ldapmodify để sửa đổi các mục nhập hiện có. Ldapmodify mở kết nối đến thư mục và xác thực người dùng. Sau đó, nó mở tệp LDIF được cung cấp dưới dạng đối số và sửa đổi các mục nhập LDAP được chỉ định bởi tệp.
- ldapmodify sử dụng dạng đã sửa đổi của tệp LDIF. Trong chính tệp đó, bạn sử dụng kiểu thay đổi thuộc tính để chỉ định kiểu thay đổi. Ví dụ là kiểu thay đổi: add.
- Có thể có bốn loại thay đổi:
	 - thêm - thêm một mục mới
	 - sửa đổi - thay đổi một mục nhập hiện có, nghĩa là nó thêm, xóa hoặc thay thế các thuộc tính của mục nhập
	 - xóa - xóa một mục hiện có
	 - modrdn - sửa đổi RDN của một mục hiện có
	 
- Câu lệnh :

```
ldapmodify [options] [-f LDIF-filename]
```







