# squid Proxy

+ Setup trên Centos 7 x64
--------------------------------
Step 1. Cài đặt httpd-tools, Squid <br />
#yum -y install httpd-tools <br />
#yum -y install squid

Step 2. Tạo File Password, Set Password Proxy <br />
#touch /etc/squid/passwd <br />
#chown squid: /etc/squid/passwd <br />
#htpasswd /etc/squid/passwd admin <br />
Nhập Password và Xác minh Password.

Step 3. Cấu hình Squid Config. <br />
#nano /etc/squid/squid.conf

Copy và Paste.

auth_param basic program /usr/lib64/squid/basic_ncsa_auth /etc/squid/passwd <br />
auth_param basic children 5 <br />
auth_param basic realm Squid Basic Authentication <br />
auth_param basic credentialsttl 2 hours <br />
acl auth_users proxy_auth REQUIRED <br />
http_access allow auth_users

Ctrl + X => Save Y => Exit.

Restart Squid. <br />
#service squid restart

check status squid. <br />
#service squid status

Mở Port Firewall. <br />
#firewall-cmd --permanent --add-port=1983/tcp <br />
#firewall-cmd --reload
