Birde `-O` parametresi vardır ve bu parametreyi kullandığımızda -o parametresinden farklı olarak istek yapılan adresin uzantısında bir dosya oluşturarak, çıktıyı oraya yazar.

```
$ curl -O https://medium.com/@damlayazici -O https://medium.com/t%C3%BCrk-telekom-bulut-teknolojileri?source=user_profile---------0----------------------------

  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   99k    0   99k    0     0    99k      0 --:--:-- --:--:-- --:--:--   99k
100  297k    0  297k    0     0   298k      0 --:--:-- --:--:-- --:--:--  145M
```

Burada gördüğünüz gibi hem https://medium.com/@damlayazici adresine hem de https://medium.com/t%C3%BCrk-telekom-bulut-teknolojileri?source=user_profile---------0---------------------------- adresine aynı komut içerisinde `-O` kullanılarak istek yapıldı.
 `@damlayazici` ve  `t%C3%BCrk-telekom-bulut-teknolojileri?source=user_profile---------0----------------------------` adında iki dosyanın oluşmuş olması, ve istek sonuçlarının içine yazılmış olması gerekir. `ls` ile dosyaların oluşup olmadığına bakalım:

```
$ ls

@damlayazici
cert.pem
key.pem
t%C3%BCrk-telekom-bulut-teknolojileri?source=user_profile---------0----------------------------
workshop.lic
```

Gördüğünüz gibi dosyalar arasında bu iki dosyanın da oluştuğu görülüyor. `cat` komutuyla isterseniz dosya içlerini kontrol edebilirsiniz.