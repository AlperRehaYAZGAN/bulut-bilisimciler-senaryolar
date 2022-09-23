# cURL Komutu Nedir, Nasıl Kullanılır?

## Bu örnek ortamımızda cURL komutunun kullanım şekli ve çıktılarını ele alacağız.

### Seviye: Başlangıç

  

## cURL Nedir?

  cURL desteklediği bir çok protokol üzerinden veri akışını gerçekleştirmek amaçlı oluşturulmuş bir açık kaynak kodlu yazılım projesidir. Ücretsiz bir yazılım olarak 1998 yılında kullanıma sunulmuştur. En son kararlı sürüm, 9 Aralık 2020’de piyasaya sürülen 7.74.0’dır.
  "Client URL" nin kısaltmasıdır ve ismindeki c harfi istemciyi(client) ifade eder. cURL projesi **libcurl** ve **cURL** olarak ikiye ayrılır. 
  
 +  **libcurl** çir çok platformda çalışan; bir çok protokolü(FTP, FTPS, HTTP, HTTPS, SCP, SFTP, TFTP, Telnet, LDAP IMAP, POP3, SMTP, vb...) ve yazılımı (C/C++, R, Java, Python, Go, PHP) desteklemektedir.
 
+  **cURL**, libcurl kütüphanesini kullanarak veri göndermek veya veri almak için kullanılır. 
HTTPS gibi güvenli protokol kullanarak bir sunucuya istek yapıldığında ilk olarak SSL sertifika doğrulaması yapar. Eğer istek yapılan sunucu self-signed bir sertifikaya sahipse veya geçersiz bir sertifikası varsa cURL hata mesajı dönecek ve bize istediğimiz veriyi getiremeyecektir. Bu durumu atlatmak yani sertifika doğrulamasının atlanması için -k veya -insecure parametreleri kullanılabilir. 