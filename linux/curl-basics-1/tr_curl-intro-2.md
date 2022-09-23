## cURL Komut Satırı Kullanımı

Öncelikle Linux makinemizde cURL versiyonunu öğrenmek için aşağıdaki komutu kullanabiliriz:

```
$ curl enter link description here--version

curl 7.68.0 (x86_64-pc-linux-gnu) libcurl/7.68.0 OpenSSL/1.1.1f zlib/1.2.11 brotli/1.0.7 libidn2/2.2.0 libpsl/0.21.0 (+libidn2/2.2.0) libssh/0.9.3/openssl/zlib nghttp2/1.40.0 librtmp/2.3
Release-Date: 2020-01-08
Protocols: dict file ftp ftps gopher http https imap imaps ldap ldaps pop3 pop3s rtmp rtsp scp sftp smb smbs smtp smtps telnet tftp 
Features: AsynchDNS brotli GSS-API HTTP2 HTTPS-proxy IDN IPv6 Kerberos Largefile libz NTLM NTLM_WB PSL SPNEGO SSL TLS-SRP UnixSockets
```

Buradan anlaşıldığı üzere mevcut versiyon 7.68.0'dır.



Genel cURL kullanımı şu şekildedir:

```
curl [OPTIONS] [URL]
```

Bu şekilde yani en basit kullanımıyla URL kısmında belirtilen adresin içerikleri cevap olarak dönecektir. Cevaplar stdout olarak verilir.

