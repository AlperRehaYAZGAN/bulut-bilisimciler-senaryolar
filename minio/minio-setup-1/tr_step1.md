### S3 Obje Tabanlı Veri Depolama  

####  Seviye: Başlangıç  

Bu örnek ortamımızda  S3 obje tabanlı dağıtık veri saklama çözümünü ele alacağız.  

### Dağıtık Veri Saklama Nedir?

Dağıtık veri saklama tek bir veriyi birden fazla lokasyonda ya da cihazda birbirinden bağımsız şekilde saklamaya yarayan yaklaşımı özetlemektedir. Basit anlamda bir verinin öncesinde oluşturulmuş bir küme içerisinde bütünlüğünü koruyacak şekilde parçalara ayrılarak saklanması yöntemine dayanır. Veri kümesi altındaki her bir bileşen bir bütünün parçasını ifade eder ve kendine atanmış görevi yerine getirir. Görev odaklı bir dağılım yapıldığından bileşenlere kendi içerisinde özgürlük tanınır. 

![Docker Mimaisi](https://blog.min.io/content/images/2019/05/Screen-Shot-2019-05-15-at-3.19.31-PM.png)

Dağıtık veri saklama çözümleri geleneksel yapıların aksine çok daha yüksek boyutlara ulaşmakta ve kümülatif ver saklamada limitler noktasında esneklik sağlamaktadır. Amazon S3, Microsoft Azure Blob Storage, Google Cloud Storage bu çözümlere iyi birer örnek olarak verilebilir. 

+ **Files**, Dağıtık sistemler üzerinde saklanan dosyaların sistemlerin okuyacağı metotlarda tanıtılması ile dosya paylaşımına olanak sağlar.
+ **Block Storage** Dosya paylaşma yöntemine benzer olarak burada dosyalardan ziyade dosyaların saklandığı block fiziksel bileşenler sunuculara tanıtılır. Yaygın kullanımı SAN olarak tanımlanan teknolojidir.
+ **Objects**,  Obje tabanlı veri depolama sistemlerinde verilerin saklandığı tekil ID ya da HASH olarak tanımlanan bileşenlerdir. Geleneksel yapılara göre Obje tabanlı veri saklama çözümlerinin ciddi avantajları vardır. 
    + **Ölçeklenebilme** Obje tabanlı veri depolama sistemleri yatayda ve dikeyde büyüme özelliğine sahip olup büyük boyutlarda kümülatif veri saklamada esneklik sağlar.
    + **Yedekli Yapı**, Dağıtık veri saklama çözümleri verinin farklı lokasyonlarda yedeklenmesi, aynı verinin uygulanacak politikalar ile yedeklenmesi, silinmesinin ya da değiştirilmesinin engellenmesi noktasında veri odaklı avantajlar sağlar. 
    + **Maliyet**, geleneksel çözümlerin aksine genel geçer fiziksel bileşenler kullanılarak bir dağıtık veri saklama çözümü kurgulanabilir. Bu sanal sunucu ya da fiziksel n adet sunucunun bir araya gelmesi ile düşük maliyetli özel çözümler oluşturmak demektir. 
    + **Performans**, dağıtık veri saklama çözümlerinde ihtiyaç duyulan performans verisine göre bir yapı oluşturulabilir ve herhangi bir "t" anında bu yapı arzu edilen şekilde farklı bir yapıya dönüştürülebilir.  

#### Dağıtık Veri Saklama Çözümlerinin Avantajları
+ **Parçalama/Bölümleme**, Dağıtık veri saklama çözümlerinde veriler bir sunucu kümesi içerisinde tanımlanan politikalar ile farklı fiziksel bileşenler üzerinde çalışabilir ve ihtiyaç anında politikalar ile yönetilebilir. Bu uygulama ya da çözüm odaklı politika belirlemek demektir. 
+ **Replikasyon**, Aynı veri merkezi ya da farklı lokasyona doğru verinin replikasyonu yapılabilir. Bu replikasyonda geleneksel çözümlerden farklı genel geçer ortak kullanılan protokoller olması sebebiyle sizi belli firmaların çözümlerine yönlendirmez. A veri merkezide X firmasının çözümü varken B veri merkezinde Y firması olabilir. İki firmanın çözümü arasında replikasyon kurulabilir.

![MinIO Replikasyon](https://min.io/resources/img/home/features/active-active-replication.svg)

+ **Hata Toleransı**, Merkezi bir yapıdan ziyade dağıtılmış bir rol ve sorumluluk olması sebebiyle yüksek hata toleransı sağlık. İhtiyaca göre mimarinin kurgulanmasına olanak sağlar.
+ **Esnek ve Ölçeklenebilir**, Belli konfigürasyonlarda fiziksel bileşenlerin eklenerek yapının yatayda veya dikeyde büyümesine olanak sağlar. Burada önemli olan beklentileri karşılayacak fiziksel bileşenlerin ilgili kümeye eklenmesidir. Bir firma bağımlılığından ziyade isteklere cevap verilebilirlik sorgulanır. 

