# squid

+ Setup trên Centos 7 x64
--------------------------------
Step 1. Cài đặt httpd-tools, Squid <br />
#yum -y install httpd-tools <br />
#yum install squid

Step 2. Tạo File Password, Set Password Proxy
#touch /etc/squid/passwd
#chown squid: /etc/squid/passwd
#htpasswd /etc/squid/passwd admin
Nhập Password và Xác minh Password.

Step 3. Cấu hình Squid Config.
#nano /etc/squid/squid.conf

Copy và Paste.

auth_param basic program /usr/lib64/squid/basic_ncsa_auth /etc/squid/passwd
auth_param basic children 5
auth_param basic realm Squid Basic Authentication
auth_param basic credentialsttl 2 hours
acl auth_users proxy_auth REQUIRED
http_access allow auth_users

Ctrl + X => Save Y => Exit.

Restart Squid.
#service squid restart

check status squid.
#service squid status

Mở Port Firewall.
#firewall-cmd --permanent --add-port=1983/tcp
#firewall-cmd --reload
