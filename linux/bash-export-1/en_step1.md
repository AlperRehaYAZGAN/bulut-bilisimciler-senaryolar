###  Seviye: Başlangıç

Bu bölüme kadar temel olarak değişkenleri nasıl tanımlayabileceğimizden ve tanımlama yaparken nelere dikkat etmemiz gerektiğinden bahsettik. Ancak henüz değinmediğimiz ve önemli olan başka bir konu da; değişkenlerin "export" edilmediği sürece yalnızca tanımlandıkları konsol üzerinden çağırılabiliyor olduklarıdır.

Örneğin bir betik dosyasını çalıştırdığımızda mevcut kabuk(shell) bu işlem için çatallama(fork) yaparak bir alt kabuk(subshell) oluşturur ve betiği bu alt kabukta çalıştırır. Daha sonra görev tamamlanınca alt kabuk öldürülerek ana kabuğa dönülür. Böylelikle tek bir kabuk altında birden fazla alt kabuk oluşturularak aynı anda pek çok işlemin gerçekleştirilmesi mümkün olur. Kabuğun çalışma yapısını daha iyi anlamak adına aşağıdaki diagrama göz atabilirsiniz:


![Export](https://raw.githubusercontent.com/taylanbildik/bash_script_dersleri/master/img/De%C4%9Fi%C5%9Fkenler/alt-kabuk.png)


İşte kabuğun çalışma yapısı böyle olduğundan, bizler herhangi bir değişken tanımladığımızda bu değişkenin alt kabuklarda da tanınmasını istiyorsak mutlaka export komutu ile değişkenimizi alt kabuklara ulaştırmalıyız.

Bu durumu gözlemlemek için çalışmakta olduğum kabuk üzerinde `degisken="yeni değer"` şeklinde bir değişken tanımlayıp konsola bastıralım:

``` {.sh}
root@bulutbilisimakademi:~# degisken="yeni değer"
root@bulutbilisimakademi:~# echo $degisken
>>yeni değer
```

Tanımladığımız kabuk üzerinde değişkenimizi kolaylıkla bastırdık, şimdi de aynı değişkeni betik dosyası içerisinden çağırarak bastırmayı deneyelim. Bu işlem için "test.sh" isimli bir betik dosyası oluşturup, daha öncesinde tanımlamış olduğumuz değişkeni çağırmak üzere `echo $degisken` komutunu yazalım. Ayrıca betik dosyası içerisinde de "degisken1="deneme"" şeklinde yeni bir değişken tanımlayıp `echo $degisken1` komutu ile bu değişkenin çağırılmasını sağlayalım:

``` {.sh}
root@bulutbilisimakademi:~# cat > test.sh
echo $degisken
degisken1="deneme"
echo $degisken1
```

Tanımlamaları yaptık. Son olacak `Ctrl+C` tuş kombinasyonuyla dosyadan çıkalım ve betik dosyamızı çalıştırarak sonuçları gözlemleyelim:

``` {.sh}
root@bulutbilisimakademi:~# bash test.sh
>>deneme
```

Gördüğünüz gibi betik dosyası içerisinde tanımlamış olduğumuz "degisken1" basılırken daha önce tanımlamış olduğumuz "degisken" basılmadı. Bunun nedeni başta da belirtiğimiz şekilde, tanımlanan değişkenlerin **export** edilmediği sürece yalnızca tanımlandığı kabuk üzerinde çalışabildiğidir. Biz betik dosyasını çalıştırdığımızda bulunduğumuz kabuk altında hemen bir alt kabuk oluşturuldu ve betik dosyamız bu alt kabuk üzerinde yürütüldü. Dolayısı ile üst kabukta tanımlanmış olan değişken alt kabuğa export edilmediği için alt kabuk tarafından tanınamadı ve değeri basılamadı.

Şimdi aynı işlemi **export** ederek tekrarlayalım:

``` {.sh}
root@bulutbilisimakademi:~# echo $degisken
>>yeni değer

root@bulutbilisimakademi:~# export degisken
root@bulutbilisimakademi:~# bash test.sh
>>yeni değer
deneme
```

Gördüğünüz gibi değişkenimizi **export** ettikten sonra alt kabukta çalıştırılan betik dosyası içerisinden de bu değişkeni çağırabildik. Böylelikle **export** komutunun işlevini test ederek görmüş olduk. 


Şimdi ise bir değişkenin sıfırlanması işlemine göz atalım. Tanımladığımız değişkenleri sıfırlamak yani tanımsız hale getirmek istersek `unset` komutunu kullanabiliyoruz. Şimdi örnek olması açısından çeşitli değişkenleri sıfırlamayı deneyelim:

``` {.sh}
root@bulutbilisimakademi:~# degisken="değer"
root@bulutbilisimakademi:~# declare -p degisken
>>declare -- degisken:"deger"

root@bulutbilisimakademi:~# unset degisken
root@bulutbilisimakademi:~# declare -p degisken
>>-bash: declare: degisken: not found
```

Gördüğünüz gibi sabit değişkenler hariç diğer değişkenler `unset` komutu sayesinde kolaylıkla sıfırlanabiliyor. Sabit değişkenlerin sıfırlanmasının ancak değişkenin tanımlandığı kabuğun kapatılması ile mümkün olacağını zaten biliyorsunuz. O yüzden sabit değişkenler hariç, tanımlamış olduğunuz diğer değişkenleri tanımsız yapmak isterseniz `unset` komutunu kullanmanız yeterli.


Şimdiye kadar pek çok değişken tanımlayıp bu değişkenlerin değerlerini konsola bastırdık. Ancak şu ana kadar ki bastırmış olduğumuz değerler bizlerin atadığı değerlerin birebir aynısıydı. Fakat her zaman basılan bu değerlerin tamamına ihtiyaç duymayabiliyoruz. İşte bu gibi durumlarda alacağımız çıktıları düzenlemek, yani örneğin bir kısmını bastırmak ya da bir kısımını silmek gibi işlevleri yerine getirmek için birkaç farklı kullanım şekli bulunuyor. Şimdi genel olarak bu kullanımları ele alalım.


+ Değişkene atanan değer içerisinde belirli bir kısımı almak istersek komutumuzu ${degisken:başlangıç:uzunluk} şeklinde kullanıyoruz.

Başlangıç : Seçme işleminin başlanacağı yeri temsil eder. Boş bırakılırsa en baştan itibaren seçer.

Uzunluk : Seçme işleminin ne kadar uzunlukta olacağını belirtir. Bu kısım boş bırakılırsa seçme işlemi otomatik olarak değerin sonuna kadar yapılır.

Şimdi örnek kullanımlara bakalım.

Öncelikle "deneme" isimli değişkene "123456789" değerini atayalım:
``` {.sh}
root@bulutbilisimakademi:~# deneme="123456789"
```

Değişken değerinin ilk 3 karakterini bastıralım:
``` {.sh}
root@bulutbilisimakademi:~# echo ${deneme::3}
>>123
```

Değişken değerinin 2. karakterinden sonraki tüm karakterleri bastıralım:
``` {.sh}
root@bulutbilisimakademi:~# echo ${deneme:2}
>>3456789
```

Değişken değerinin 2. karakterinden itibaren 4 karakter bastıralım:
``` {.sh}
root@bulutbilisimakademi:~# echo ${deneme:2:4}
>>3456
```


Şu ana kadar kendimiz nasıl değişken tanımlarız bunu ele almıştık. Şimdi ise sistemde tanımlı olan değişkenlerden bahsederek yolculuğumuza devam edelim.

Ortam Değişkenlerini Görüntülemek: Sistemin işleyişinde pek çok konuda kolaylık sunan çeşitli ortam değişkenleri vardır. Bunları görmek istersek komut satırına set , env ya da printenv komutlarından birini ihtiyacımıza göre kullanabiliriz. 


`set` komutu, shell'e ait olan değişkenlerin adını ve değerlerini verir:

``` {.sh}
root@bulutbilisimakademi:~# set
>>BASH=/bin/bash
BASHOPTS=checkwinsize:cmdhist:complete_fullquote:expand_aliases:extglob:extquote:force_fignore:globasciiranges:histappend:interactive_comments:login_shell:progcomp:promptvars:sourcepath
BASH_ALIASES=()
BASH_ARGC=([0]="0")
BASH_ARGV=()
BASH_CMDS=()
BASH_COMPLETION_VERSINFO=([0]="2" [1]="10")
BASH_LINENO=()
BASH_REMATCH=()
BASH_SOURCE=()
```


`env` komutu, sistemde bulunan bütün "export" edilmiş yani dışa(alt kabuklara) aktarılmış değişkenlerle beraber değişkenleri gösterir:

``` {.sh}
root@bulutbilisimakademi:~# env
>>SHELL=/bin/bash
WT_SESSION=0dc1754e-7e57-4fae-ac31-7bdcfda3c0b4
NAME=BulutBilişimAkademi
PWD=/home/bulutbilisimakademi
LOGNAME=bulutbilisimakademi-wsl
MOTD_SHOWN=update-motd
VIRTUALENVWRAPPER_SCRIPT=/usr/share/virtualenvwrapper/virtualenvwrapper.sh
HOME=/home/bulutbilisimakademi
LANG=C.UTF-8
```


`printenv` komutu, sistemde bulunan bütün çevresel değişkenleri verir:

``` {.sh}
root@bulutbilisimakademi:~# printenv
>>SHELL=/bin/bash
WT_SESSION=0dc1754e-7e57-4fae-ac31-7bdcfda3c0b4
NAME=BulutBilişimAkademi
PWD=/home/bulutbilisimakademi
LOGNAME=bulutbilisimakademi-wsl
MOTD_SHOWN=update-motd
VIRTUALENVWRAPPER_SCRIPT=/usr/share/virtualenvwrapper/virtualenvwrapper.sh
HOME=/home/bulutbilisimakademi
LANG=C.UTF-8
LS_COLORS=rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:mi=00:su=37;41:sg=30;43:ca=30;41:tw=30;42:ow=34;42:st=37;44:ex=01;32:*.tar=01;31:*.tgz=01;31:*.arc=01;31:*.arj=01;31:*.taz=01;31:*.lha=01;31:*.lz4=01;31:*.lzh=01;31:*.lzma=01;31:*.tlz=01;31:*.txz=01;31:*.tzo=01;31:*.t7z=01;31:*.zip=01;31:*.z=01;31:*.dz=01;31:*.gz=01;31:*.lrz=01;31:*.lz=01;31:*.lzo=01;31:*.xz=01;31:*.zst=01;31:*.tzst=01;31:*.bz2=01;31:*.bz=01;31:*.tbz=01;31:*.tbz2=01;31:*.tz=01;31:*.deb=01;31:*.rpm=01;31:*.jar=01;31:*.war=01;31:*.ear=01;31:*.sar=01;31:*.rar=01;31:*.alz=01;31:*.ace=01;31:*.zoo=01;31:*.cpio=01;31:*.7z=01;31:*.rz=01;31:*.cab=01;31:*.wim=01;31:*.swm=01;31:*.dwm=01;31:*.esd=01;31:*.jpg=01;35:*.jpeg=01;35:*.mjpg=01;35:*.mjpeg=01;35:*.gif=01;35:*.bmp=01;35:*.pbm=01;35:*.pgm=01;35:*.ppm=01;35:*.tga=01;35:*.xbm=01;35:*.xpm=01;35:*.tif=01;35:*.tiff=01;35:*.png=01;35:*.svg=01;35:*.svgz=01;35:*.mng=01;35:*.pcx=01;35:*.mov=01;35:*.mpg=01;35:*.mpeg=01;35:*.m2v=01;35:*.mkv=01;35:*.webm=01;35:*.ogm=01;35:*.mp4=01;35:*.m4v=01;35:*.mp4v=01;35:*.vob=01;35:*.qt=01;35:*.nuv=01;35:*.wmv=01;35:*.asf=01;35:*.rm=01;35:*.rmvb=01;35:*.flc=01;35:*.avi=01;35:*.fli=01;35:*.flv=01;35:*.gl=01;35:*.dl=01;35:*.xcf=01;35:*.xwd=01;35:*.yuv=01;35:*.cgm=01;35:*.emf=01;35:*.ogv=01;35:*.ogx=01;35:*.aac=00;36:*.au=00;36:*.flac=00;36:*.m4a=00;36:*.mid=00;36:*.midi=00;36:*.mka=00;36:*.mp3=00;36:*.mpc=00;36:*.ogg=00;36:*.ra=00;36:*.wav=00;36:*.oga=00;36:*.opus=00;36:*.spx=00;36:*.xspf=00;36:
VIRTUALENVWRAPPER_WORKON_CD=1
WORKON_HOME=/home/bulutbilisimakademi/.virtualenvs
LESSCLOSE=/usr/bin/lesspipe %s %s
TERM=xterm-256color
LESSOPEN=| /usr/bin/lesspipe %s
USER=bulutbilisimakademi
VIRTUALENVWRAPPER_PROJECT_FILENAME=.project
SHLVL=1
WSLENV=WT_SESSION::WT_PROFILE_ID
```



Son olarak değişkenleri bastırırken kullandığımız `echo` komutununun çoklu işlevlerini kullanarak, farklı çıktıları nasıl elde ederiz ona bakalım.

+ `-e` echo komutunun ardından gireceğimiz ters slash işaretli özel parametrelerin doğru şekilde yorumlanabilmesini sağlar. Yani echo komutunun farklı bastırma seçeneklerini kullanmak istiyorsak mutlaka -e parametresini kullanmamız gerekiyor. Bu durumu birazdan örnekler üzerinden göstereceğiz.


+ `-n` : Sonraki satırı atlamaz, yani satır atlanmasını engeller. İşlevini anlamak için aşağıdaki iki çıktıyı dikkatlice incelemeniz yeterlidir.
``` {.sh}
root@bulutbilisimakademi:~# echo "deneme"
>>deneme
root@bulutbilisimakademi:~# echo -n "deneme"
>>deneme root@bulutbilisimakademi:~# e
```


+ `\n` : Yeni satıra atlar. Kullanıldığı yerden sonra, bir alt satıra geçerek çıktıları bastırır. Yani bir satır atlamış olur. 
``` {.sh}
root@bulutbilisimakademi:~# echo "test \nmetni"
>> test \nmetni

root@bulutbilisimakademi:~# echo -e "test \nmetni"
>>test
metni
```



+ `\b` : Soldan bir karakter siler:
``` {.sh}
root@bulutbilisimakademi:~# echo -e "test \bmetni"
>>testmetni

root@bulutbilisimakademi:~# echo -e "test\b metni"
>>tes metni

root@bulutbilisimakademi:~# echo -e "te\bst metni"
>>tst metni
```

+ `\e` : Sağdan bir karakter siler:
``` {.sh}
root@bulutbilisimakademi:~# echo -e "test \emetni"
>>test etni

root@bulutbilisimakademi:~# echo -e "test\e metni"
>>testmetni

root@bulutbilisimakademi:~# echo -e "te\est metni"
>>tet metni
```

+ `\c` : Sağında yer alan her şeyi siler:
``` {.sh}
root@bulutbilisimakademi:~# echo -e "test m\cetni"
>>test m

root@bulutbilisimakademi:~# echo -e "test\c metni"
>>test

root@bulutbilisimakademi:~# echo -e "te\cst metni"
>>te
```


+ `\t` : Tab tuşu görevi görür:
``` {.sh}
root@bulutbilisimakademi:~# echo -e "test m\tetni"
>>test m    etni

root@bulutbilisimakademi:~# echo -e "test\t metni"
>>test    metni

root@bulutbilisimakademi:~# echo -e "te\tst metni"
>>te    st metni
```


+ `\v` : Dikey tab görevi görür:
``` {.sh}
root@bulutbilisimakademi:~# echo -e "test m\vetni"
>>test m    
            etni

root@bulutbilisimakademi:~# echo -e "test\v metni"
>>test
            metni

root@bulutbilisimakademi:~# echo -e "te\vst metni"
>>te    
        st metni


``` 

+ `\\` : Ters eğik çizgi basmak üzere kullanılır:
``` {.sh}
root@bulutbilisimakademi:~# echo -e "test m\etni"
>>test m

root@bulutbilisimakademi:~# echo -e "test m\\etni"
>>test m

root@bulutbilisimakademi:~# echo -e "test m\\\etni"
>>test m\etni

root@bulutbilisimakademi:~# echo -e "test m\\\\etni"
>>test m\etni
```


+ `\a` : Çıktı ile birlikte (konsol destekliyorsa) uyarı sesi çıkmasını sağlar:
``` {.sh}
root@bulutbilisimakademi:~# echo -e "test m\aetni"
>>test metni

root@bulutbilisimakademi:~# echo -e "\atest metni"
>>test metni
```

Bu bölümde değişkenler konusuna daha detaylı bir bakış attık ve son olarak `echo` komutunun alabileceği parametrelere baktık. Bir sonraki bölümde görüşmek üzere
