[root@control-plane certs]# openssl genrsa -out ca.key 4096
Generating RSA private key, 4096 bit long modulus (2 primes)
................................................................................................................................................................................................................................................++++
.......................................................................................++++
e is 65537 (0x010001)
[root@control-plane certs]# openssl req -x509 -new -nodes -sha512 -days 365 \
> -key ca.key \
> -out ca.crt
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [XX]:kr
State or Province Name (full name) []:uilljeonbu
Locality Name (eg, city) [Default City]:
Organization Name (eg, company) [Default Company Ltd]:
Organizational Unit Name (eg, section) []:
Common Name (eg, your name or your server's hostname) []:
Email Address []:
[root@control-plane certs]# openssl genrsa -out server.key 4096
Generating RSA private key, 4096 bit long modulus (2 primes)
.......++++
......................++++
e is 65537 (0x010001)
[root@control-plane certs]# openssl req -sha512 -new \
> -key server.key \
> -out server.csr
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [XX]:kr
State or Province Name (full name) []:
Locality Name (eg, city) [Default City]:
Organization Name (eg, company) [Default Company Ltd]:
Organizational Unit Name (eg, section) []:
Common Name (eg, your name or your server's hostname) []:
Email Address []:

Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:
An optional company name []:
[root@control-plane certs]#  vi v3ext.cnf
[root@control-plane certs]# ls
ca.crt  ca.key  server.csr  server.key
[root@control-plane certs]# ls
ca.crt  ca.key  server.csr  server.key
[root@control-plane certs]#  vi v3ext.cnf
[root@control-plane certs]#  openssl x509 -req -sha512 -days 365 \
> -extfile v3ext.cnf \
> -CA ca.crt -CAkey ca.key -CAcreateserial \
> -in server.csr \
> -out server.crt
Signature ok
subject=C = kr, L = Default City, O = Default Company Ltd
Getting CA Private Key
[root@control-plane certs]# openssl x509 -inform PEM -in server.crt -out server.cert
[root@control-plane certs]#




링크: +https://wookiist.dev/126
+ Resseting