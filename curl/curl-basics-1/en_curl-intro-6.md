Şimdi de sertifika doğrulamasını nasıl atlatacağımıza bakalım. Yukarıda da bahsettiğim gibi `-k` veya `-insecure` parametreleri kullanılmalıdır. 

```
$ curl https://self-signed.badssl.com/

curl: (60) server certificate verification failed. CAfile: /etc/ssl/certs/ca-certificates.crt CRLfile: none
More details here: http://curl.haxx.se/docs/sslcerts.html

curl performs SSL certificate verification by default, using a "bundle"
 of Certificate Authority (CA) public keys (CA certs). If the default
 bundle file isn't adequate, you can specify an alternate file
 using the --cacert option.
If this HTTPS server uses a certificate signed by a CA represented in
 the bundle, the certificate verification probably failed due to a
 problem with the certificate (it might be expired, or the name might
 not match the domain name in the URL).
If you'd like to turn off curl's verification of the certificate, use
 the -k (or --insecure) option.
 ```             

Gördüğünüz gibi https://self-signed.badssl.com/ adresine yapılan istek sertifika doğrulamasına takıldı ve bu aşamayı geçemedi. -k parametresi ile bu aşamayı atlamaya çalışalım:

```
$ curl -k https://self-signed.badssl.com/

<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="shortcut icon" href="/icons/favicon-red.ico"/>
  <link rel="apple-touch-icon" href="/icons/icon-red.png"/>
  <title>self-signed.badssl.com</title>
  <link rel="stylesheet" href="/style.css">
  <style>body { background: red; }</style>
</head>
<body>
<div id="content">
  <h1 style="font-size: 12vw;">
    self-signed.<br>badssl.com
  </h1>
</div>

</body>
</html>               
 ```  