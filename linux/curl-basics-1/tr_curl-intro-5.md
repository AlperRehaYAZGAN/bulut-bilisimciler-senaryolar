Bir önceki sayfada google.com adresine istek yaptığımızda **301 Moved** yanıtının döndüğünü görmüştük. Biz sayfaya doğru yönlendirme ile ulaşmak istersek `-L` parametresini kullanabiliriz. Bu sayede doğru yönlendirme ile sayfaya ulaşırız. 

```
$ curl -L google.com

<!doctype html><html itemscope="" itemtype="http://schema.org/WebPage" lang="tr"><head><meta content="text/html; charset=UTF-8" http-equiv="Content-Type"><meta content="/images/branding/googleg/1x/googleg_standard_color_128dp.png" itemprop="image"><title>Google</title><script nonce="tDsp_naPcVl2rhPw7UE5lQ">(function(){window.google={kEI:'fesgY_TeA5m6z7sPy8mvmAM',kEXPI:'0,1302536,56873,6059,206,2415,2389,2316,383,246,5,5367,1123753,1197722,672,80,380017,16114,17444,11240,22431,1361,283,12028,17588,4998,13228,3847,10622,22741,5081,885,708,1279,2744,147,1103,841,1982,214,4100,108,3406,606,2023,1777,520,14670,3227,2845,7,29
...
```

Çıktıda olduğu gibi cevap olarak 301 değil sayfa içeriği dönmüştür.

Herhangi bir sebepten ötürü sayfada indirme işlemimiz kesilirse  işlem devam etsin diye `-C` parametresi kullanılabilir.
Aşağıdaki örnekte herhangi bir duruma karşı indirme devam etsin ve tamamlandi.txt dosyasına atılsın denilmiştir.

```
$ $ curl -C - -o tamamlandi.txt http://www.gnu.org/software/gettext/manual/gettext.html

  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 1534k  100 1534k    0     0  1230k      0  0:00:01  0:00:01 --:--:-- 1230k
```


Belirli bir tarihten sonra istediğimiz adresten verileri getirmek için `-z` parametresini kullanabiliriz.

```
$ curl -z 30-July-22 https://jsonplaceholder.typicode.com/albums

[
  {
    "userId": 1,
    "id": 1,
    "title": "quidem molestiae enim"
  },
  {
    "userId": 1,
    "id": 2,
    "title": "sunt qui excepturi placeat culpa"
  },
  {
    "userId": 1,
    "id": 3,
    "title": "omnis laborum odio"
  },
  {
  ...
```