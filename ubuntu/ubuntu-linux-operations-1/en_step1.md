### Ubuntu Linux Operasyonel İşlemler  
  
Bu eğitim setinde linux üzerinde yapılan operasyon işlemlerinin ubuntu üzerinde örneklendirilmesi yapılmıştır.  
  
### Yeni eklenen disk tarama
Eğer ubuntu yüklü olan sunucunuza yeni bir disk eklendi ise ve siz bunu reboot etmeden görmesini istiyor iseniz aşağıdaki komutları çalıştırmanız yeterlidir. 
**1.yol** ) root@ubuntu# **echo "- - -" | tee /sys/class/scsi_host/host****/**scan**
**2.yol** ) root@ubuntu# **rescan-scsi-bus.sh**

### Kullanıcıya tcpdump, traceroute v.b. gibi uygulamalar için çalıştırma yetkisi verme
Eğer kullanıcıyı sudo grubuna eklemeden sudo grubundaki bazı uygulamalara çalıştırma yetkisi vermek istenilir ise aşağıdaki adımlar uygulanır.
**1.yol**) root@ubuntu#**vi /etc/sudoers**
**##Eklenecek kayit##**
**user_name ALL=NOPASSWD:/usr/sbin/tcpdump**

**2.yol**) root@ubuntu#**vi /etc/sudoers.d/user_name**
**##Eklenecek kayit##**
**user_name ALL=NOPASSWD:/usr/sbin/tcpdump**
**user_name ALL=NOPASSWD:/usr/sbin/traceroute**
## Linux swap alanı görüntüleme, açma ve kapatma

Eğer uygulamanızın swap alanına düşmesini istemiyor performans kaybı olmasın isteniliyor ise ubuntu da kullanılan swap alanını görüntüleme ve kapatmak istenilir ise aşağıdaki komutlar kullanılmaktadır. 

	-s --> swap alanı görüntülenir.
**1)** root@ubuntu#**swapon –s** 

	swapoff -a --> swap alanı kapatılır.
**2)** root@ubuntu#**swapoff -a**
root@ubuntu#**vi /etc/fstab**
 #/swap.img       none    swap    sw      0       0

	swapon -a --> swap alanı açılır.
**3)** root@ubuntu#**swaponn -a**

NOT: Eğer swap alanı kapatılmak isteniliyor ise /etc/fstab dosyasından da kaldırılması veya başına # işaretinin konulması gerekir ki reboot sonrası otomatik olarak mount olup açılmasın diye.
root@ubuntu#**vi /etc/fstab**
#/swap.img       none    swap    sw      0       0

## Rsyslog loglarını log server yönlendirme
Eğer sunucunuzdaki rsyslog bir log server göndermek isterseniz aşağıdaki şekilde log server ait ip ye gönderim yapılabilinir. Siz kendi log server ip' nizi yazmalısınız.

**1)** root@ubuntu#**vi /etc/rsyslog.conf**
**#### RULES ####**
__* . *__	__@192.168.1.172:514__
**2)** root@ubuntu#**systemctl restart rsyslog**
**3)** root@ubuntu#**systemctl status rsyslog**

## Service status-restart-stop-start işlemleri

Ubuntu üzerinde bir servisin durumunun sorgulanması, yeniden başlatılması, durdurulması ve başlatılması için aşağıdaki işlemler yapılır.

	Service durumunu öğrenmek için,
root@ubuntu#**systemctl status rsyslog**

	Service durdurmak için,
root@ubuntu#**systemctl stop rsyslog**

	Service yeniden başlatmak için,
root@ubuntu#**systemctl restart rsyslog**

	Service sunucu poweron olduktan sonra otomatik olarak başlaması için,
root@ubuntu#**systemctl enable rsyslog**

	Service otomatik olarak başlamaması için,
root@ubuntu#**systemctl disable rsyslog**

	Service başlatmak için,
root@ubuntu#**systemctl start rsyslog**

__NOT: Bu örnekte rsyslog servisi üzerinden çalışma yapılmıştır siz hangi servisi kontrol etmek istiyorsanız onun  servis ismini yazarak sorgulama yapabilirsiniz.__

## Ubuntu işletim sistemine ait logları listeleme
Eğer sunucunuz üzerindeki kernel loglarını, sistem loglarını, ,servis loglarını, auth loglarını v.b. logları incelemek istenilir ise aşağıdaki komutlar çalıştırılır.

root@ubuntu#**dmesg**
root@ubuntu#**journalctl**
root@ubuntu#**more /var/log/auth.log**

You can rename the current file by clicking the file name in the navigation bar or by clicking the **Rename** button in the file explorer.

## Client sunuculara ntp server ip’ sinin set edilmesi
Eğer ubuntu sunucunuzun zaman senkronizasyonu bir ntp sunucu üzerinden yapılması isteniliyor ise aşağıdaki işlemler yapılmalıdır.

root@ubuntu#**vi /etc/systemd/timesyncd.conf**
**####EKLENECEK OLAN NTP IP####**
**NTP=10.131.4.44**
root@ubuntu#**systemctl restart systemd-timesyncd.service**
root@ubuntu#**systemctl status systemd-timesyncd.service**
# PAKET İŞLEMLERİ
## Paket yüklemek
Ubuntu paket yöneticisi apt’ dir. Ubuntu da bir paket yüklemek istenildiği zaman **apt install paket_ismi** ile yükleme yapılabilinir. Ubuntu eski versiyonlarında apt-get install paket_ismi ile paketler yüklenirdi. Ancak yeni güncellemeler ile get komutunu yazmana gerek kalmadan direk apt komutuyla işlemler yapıla bilinir.

root@ubuntu#**apt install package_name**
root@ubuntu#**apt install nload**
veya
root@ubuntu#**apt-get install nload**


## Paket Kaldırmak
Kaldırılak istenilen paket aşağıdaki şekilde sunucu üzerinden silinir.

root@ubuntu#**apt remove package_name**
root@ubuntu#**apt remove nload**



## Paketlerin tüm kalıntılarını temizleyerek silmek
Tüm kalıntılarıyla silinmek istenilen paket ismi package_name alanına yazılır.

root@ubuntu#**apt purge package_name**
root@ubuntu#**apt purge nload**

## Paketi yeniden yükleme

Yüklü olan paketin attribute değerlerinde bir değişiklik olursa veya v.b. gibi durumlardan dolayı paketi tekrar yüklemeniz gerekir ise aşağıdaki reinstall komutu çalıştırılır.

root@ubuntu#**apt reinstall package_name**	
root@ubuntu#**apt reinstall nload**	

## Sources list update edilmesi

Ubuntu ‘ da bir paket yükleneceği zaman direk olarak /etc/apt/sources.list altındaki repo url’ ler kontrol edilir ve ilgili paketler bu ilgili sources.list dosyasındaki repo’ lardan çekilir. Eğer siz local repo eklediyseniz veya yeni bir repo url eklediyseniz paket yüklemeden önce bu config file güncellemeniz gerekmektedir.

root@ubuntu#**apt update**

## Upgrade edilmesi

<![endif]-->

Eğer Ubuntu işletim sisteminde kernel seviyesinde ve security patch olarak güncelleme yapılmak isteniliyor ise upgrade komutu çalıştırılmaktadır. Redhat işletim sistemi yüklü olan sunucularda update komutu çalıştırıldığında os seviyesinde güncelleme yapılır iken ubuntu da update komutu sadece sources.list (paketlerin yükleneceği repo adreslerini tutan config file) güncellemektedir. Apt upgrade komutuyla os seviyesinde güncelleme yapılmaktadır. Eğer repoya yeni eklenen repo url adresleri var ise upgrade komutundan önce update komutunu çalıştırarak en güncel repolardan güncellemeler ve paket yüklemeler yapılacaktır.
<![endif]-->

root@ubuntu#**apt update**
root@ubuntu#**apt upgrade**

## Güncellenecek Paketlerin Listelenmesi
apt upgrade komutundan önce hangi paketlerin hangi versiyonlara yükseltileceğini görmek istenilirse aşağıdaki işlem yapılır.
root@ubuntu#**apt list --upgradable**


## Bir üst versiyona yükseltilmesi

Eğer bir paket bağımlılıklarına bağlı kalmadan illa yükseltmek isteniliyor ise, yeni bağımlılıkların kurulması, kullanılmayanların silinmesi ve güncel kernel versiyonun yüklenmesi istenilirse dist-upgrade komutu kullanılır.

root@ubuntu#**apt dist-upgrade**

	Eğer sadece belirtilen paketin upgrade edilmesi istenilir ise;
root@ubuntu#**apt dist-upgrade package_name**
root@ubuntu#**apt dist-upgrade nload**


## Paketleri hakkında bilgi almak
Eğer bir paketi yüklemeden önce onun hakkında bilgi alınmak istenilirse;

root@ubuntu#**apt info package_name**
root@ubuntu#**apt info nload**

## Gereksiz paketlerin kaldırılması

Bir güncelleme sonrası veya paket kaldırılması sonrasında gereksiz kalan paketlerin temizlenmesi için;

root@ubuntu# **apt autoremove**

## Arşivlenmiş Paketleri Silme

Paket yöneticilerine ai tolan önbellek temizlenir.
root@ubuntu# **apt clean**

Eğer bütün arşiv paketlerini silmek yerine eski sürüm olanlar ve daha sonra kullanılmayacak olanlar, repolardan silinmiş olan arşivler silinmek istenilir ise autoclean komutu kullanılır.
root@ubuntu# **apt autoclean**

## Local olarak .deb ve .rpm uzantılı dosya komutları
Ubuntu Debian ailesinden olduğu için .deb uzantılı paketleri kullanmaktadır.

	Eğer .deb uzantılı paketi sunucuya yüklemek istenilirse;
root@ubuntu#**dpkg -i nload.deb**

	Eğer dpkg -i ve apt install ile yüklenen .deb paketler kaldırılmak istenilirse;
root@ubuntu#**dpkg -r nload.deb**

	Yüklenen paketin konfigürasyon ayarlarını tekrar yapılandırılmak istenilirse;
root@ubuntu#**dpkg-reconfigure nload**


	Yüklü olan tüm paketleri listelemek istenilirse;

root@ubuntu#**dpkg -l**
<![endif]-->

dpkq -l çıktısında yer alan parametrelerin açıklaması;  
**ii :** paket normal olarak sisteme yüklendi.  
**rc :** paket yüklendikten sonra silindi ancak konfigürasyon dosyaları halen mevcut.  
**pn :** paket konfigürasyon dosyaları ile birlikte sistemden kaldırıldı.


	
	Kurulu olan paketin durumunu öğrenmek için;
root@ubuntu# **dpkg -s nload**
# Kullanıcı Yapılandırması

## Kullanıcı eklemek


Eklenmek istenilen kullanıcı ismi username alanına yazılır.

root@ubuntu#**useradd username**
**veya**
root@ubuntu#**adduser username**

## Kullanıcıyı ilgili gruba atama

İlgili kullanıcıya belli gruba atayarak o gruba ait olan servisleri yetki yükseltmesi yapmadan çalıştırılmasını sağlar.

Docker grubuna ilgili user eklenir ve docker grubuna ait servisleri sudo olmadan çalıştırmasını sağlar. İlgili kullanıcı username alanına yazılır.


root@ubuntu#**usermod -a -G docker username**

## Kullanıcıyı silmek için
Silinmek istenilen kullanıcı username alanına yazılır.

root@ubuntu#**userdel username**
**veya**
root@ubuntu#**deluser username**

## Kullanıcı password değiştirme

username kısmına password değiştirilmek istenilen kullanıcı yazılır.

root@ubuntu# **passwd username**

# Network Yapılandırması
Ubuntu da network dosyası yaml dosyasında tutulduğu için yapılandırılacak olan network ayarları yaml formatına uygun olması gerekmektedir.

NOT: Bir tane yaml içerisine, eklenmek istenilen tüm interface bilgileri yazıla bilinir.

## Tek bir interface set edilmesi

Eğer tek bir tane interface var ise aşağıdaki yapılandırma uygulanabilinir.
root@ubuntu#**vi /etc/netplan/50-cloud-init.yaml**
**###EKLENECEK OLAN IP BILGILERI###**
 **network:**
**ethernets:**
**eth0:**
**addresses:**
**- 10.10.2.10/24**
**gateway4: 10.10.2.1**
**nameservers:**
**addresses:**
**-10.10.2.8**
**search: example.intra**
**version: 2**
root@ubuntu# **netplan apply**

## Birden fazla interface set edilmesi
Eğer birden fazla birden interface var ise aşağıdaki yapılandırma set edilir.
root@ubuntu# **vi /etc/netplan/50-cloud-init.yaml**
**###EKLENECEK OLAN IP BILGILERI###**
**network:**
**ethernets:**
**eth0:**
**addresses:**
**- 10.10.2.10/24**
**gateway4: 10.10.2.1**
**nameservers:**
**addresses:**
**-10.10.2.8**
**search: example.intra**
**eth1:**
**addresses:**
**- 10.10.3.10/24**
**version: 2**
root@ubuntu# **netplan apply**

## Bond interface set edilmesi

root@ubuntu# **vi /etc/netplan/50-cloud-init.yaml**
**###EKLENECEK OLAN IP BILGILERI###**
**network:**
**bonds:**
**bond-data:**
**addresses:**
**- 10.10.2.10/24**
**gateway4: 10.10.2.1**
**interfaces:**
**- eth0**
**- eth1**
**nameservers:**
**addresses:**
**- 10.10.2.8**
**search:**
**- example.intra**
**parameters:**
**lacp-rate: fast**
**mode: 802.3ad**
**ethernets:**
**eth0: {}**
**eth1: {}**
**version: 2**
root@ubuntu# **netplan apply**
## Network Manager ile interface set edilmesi


Network ayarlarının daha kolay ve pratik olması açısından Network manager ile network yönetimini sağlayabiliriz.

Network manager ubuntuda default olarak gelmemektedir. Network manager yüklenerek nmtui ve nmcli tools kullanılarak network yapılandırması yapıla bilinir.

root@ubuntu#  **apt install network-manager**
root@ubuntu#  **systemctl start NetworkManager.service**
root@ubuntu#  **systemctl enable NetworkManager.service**
root@ubuntu#  **nmtui**
# Route Yapılandırması
## route eklemek
Eklemek istediğiniz route tanımını aşağıdaki şekilde verebilirsiniz. 
root@ubuntu#**ip route add 10.220.1.4/32 via 10.220.1.1**


Default gateway eklemek için;
root@ubuntu#**ip route add default via 192.168.216.1**


Default gateway silmek için;
root@ubuntu#**ip route del default**
<![endif]-->

Route tablosunun listelenmesi;
Route tablosunun listelenmesi için net-tools paketinin yüklü olması gerekir. Eğer net-tools yüklü değil ise ilgili paket yüklenerek route tablosu listelenir.
root@ubuntu#**apt install net-tools**
root@ubuntu#**route**

Kalıcı route eklemek için;

root@ubuntu# **vi /etc/netplan/50-cloud-init.yaml**
**network:**
**ethernets:**
**eth0:**
**addresses:**
**- 10.10.2.10/24**
**gateway4: 10.10.2.1**
**- to: 192.168.1.0/24  
via: 192.168.2.101**
**nameservers:**
**addresses:**
**-10.10.2.8**
**search: example.intra**
**version: 2**
root@ubuntu# **netplan apply**
root@ubuntu# **route -n**

**NOT: Gateway4 satırının altına eklenmek istenilen route’ lar kalıcı olması için buraya eklenebilinir.**

**NOT: Eğer birden fazla interface var ise hangi interface üzerinden route yapılması isteniliyor ise onun altına eklenebilinir.**

## Netplan apply debug etmek

Eğer network ayarlarında bir değişiklik yaptıktan sonra  aktif olmasını istiyorsanız netplan apply çalıştırmanız gerekmektedir. Network config file bir yaml dosyası olduğu için eğer syntax yazımında bir yanlışlık olursa netplay apply hata verecektir. İşte bu verilen hatayı detaylındırıp sorunu çözmek adına aşağıdaki işlemler yapılabilinir.

root@ubuntu# **netplan --debug apply**

# SSH Servis Yapılandırması
## SSH Servisi Kurulumu
Ubuntu sunucuda eğer ssh servisi kurulu değil ise kurulumu yapılır.
root@ubuntu#**sudo apt install openssh-server**
root@ubuntu#**sudo systemctl enable sshd**
root@ubuntu#**sudo systemctl start sshd**

## Kurulumu ve yapılandırması

Eğer root kullanıcısının ssh ile bağlanması kapatılacak, local user ssh bağlanması kısıtlanacak  v.b. gibi global ayarlarda sshd_config file set edilir.

root@ubuntu# **vi /etc/ssh/sshd_config**
**##EKLENECEK PARAMETRELER###**
**PermitRootLogin no**
**DenyUsers username**
**DenyGroups groupname**
root@ubuntu# **systemctl restart sshd**

# NFS Client Servisi
Eğer sunucu bir nfs server' a dosya paylaşımına erişim sağlayacak ise aşağıdaki paketler yüklenir.
root@ubuntu# **apt install nfs-common** 

## NFS Client Yapılandırması

Hizmet veren NFS server’ lardan mount edilebilecek alanları görebilmek için;
root@ubuntu# **showmount -e nfs_server_ip**

Mount edilme örneği;
root@ubuntu# **mount 10.10.10.2:/export/nfsshare /mnt/**

Eğer reboot sonrası mount edilen alanın kaybolmamasını istiyorsanız aşağıdaki fstab dosyasına eklemek gerekmektedir.
root@ubuntu# **vi /etc/fstab**
**##eklenecek mountpoint bilgileri ##**
**10.10.10.2:/export/nfsshare/mnt nfs defaults 0 0**


Mount edilen alanın kaldırılması
root@ubuntu# **umount /mnt**
NOT: Eğer fstab dosyasında tanımlı ise oradan da ilgili kayıtın silinmesi gerekir.

fstab dosyasındaki tüm alanların mount edilmesi;
root@ubuntu# **mount -a**

# Iptables Yapılandırması

Eğer iptables üzerinden kısıtlama yapılmak istenilir ise buradan ilgili yapılandırmalar yapılacaktır.
## Iptables Kuralları
	Belirli bir portu herkese açmak için;
root@ubuntu# **iptables -A INPUT -p tcp --dport 8001 -j ACCEPT**

	Belirli bir portu sadece belli bir ip açmak için;

root@ubuntu# **iptables -A INPUT -p tcp --dport 3000 -s 192.168.0.155 -j ACCEPT**

	Belirli bir portu herkese kapatmak için;
root@ubuntu# **iptables -A INPUT -p tcp --dport 5601 -j DROP**


	Belirli bir portu sadece belli bir ip kapatmak için;
root@ubuntu# **iptables -A INPUT -p tcp --dport 2211 -s 192.168.6.65 -j DROP**

	Belli bir ip subnet’ in erişimini kapatmak için;
root@ubuntu# **iptables -A INPUT -s 192.168.0.0/22 -j DROP**

	Tüm subnet yasaklanmış ip lerden sadece tek bir ip ye erişim verilmesi.
	(Bir önceki komut /22 tüm ip bloklarını engeller. 
	Bu kural ise /22 ip bloğundaki erişim verilmek istenilen ip yazılır.)

root@ubuntu# **iptables -A INPUT -s 192.168.0.5 -j ACCEPT**


**NOT**: Eğer genel bir kural yazılacak ise yani /22 subnetindeki tüm iplerin yasaklanıp sadece arasındaki tek bir ip nin erişim sağlaması isteniliyor ise öncelikle erişim sağlanmak istenilen ip kuralı çalıştırılır daha sonra yasaklanmak istenilen /22 DROP kuralı çalıştırılır.


Ayarların kaydedilmesi için varsayılan olarak gelmeyen iptables-persistent paketi yüklenir. 
Eğer bu paket yüklenmeden iptables üzerinden ayarlar yapılır ise reboot sonrası silinecektir. Kalıcı olması için ilgili paketin yüklenmesi ve aşağıdaki komutun çalıştırılması gerekmektedir.

root@ubuntu# **sudo apt install iptables-persistent netfilter-persistent**
root@ubuntu#  **systemctl enable netfilter-persistent.service**
root@ubuntu# **netfilter-persistent save**
root@ubuntu# **netfilter-persistent start**
root@ubuntu# **iptables-save  > /etc/iptables/rules.v4**

	ÖRNEK: reboot sonrası yapılan iptables kayıtların kalıcı olabilmesi için;
root@ubuntu# **iptables -A INPUT -s 192.168.0.5 -j ACCEPT**
root@ubuntu# **iptables-save  > /etc/iptables/rules.v4**


	iptables rules restore için;
root@ubuntu# **iptables-restore  < /etc/iptables/rules.v4**

## Iptables üzerinden izin verilen ip adreslerinin silinmesi

	iptables –S ile silmek istediğimiz kuralı(ip) bulunur. 
	Silinmek istenilen kural kopyalanır.

root@ubuntu# **iptables –S** -->  kurallar listelenir
root@ubuntu# **iptables –D <iptables -S ile kopyalanan kural yapıştırılır>**
root@ubuntu# **iptables-save  > /etc/iptables/rules.v4**


	ÖRNEK: iptables kural silme
**1.yol)** root@ubuntu# **iptables –S**
-A INPUT -s 192.168.0.5/32 -j ACCEPT
root@ubuntu# **iptables –D INPUT -s 192.168.0.5/32 -j ACCEPT**
root@ubuntu# **iptables-save  > /etc/iptables/rules.v4**


**2.yol)** Farklı bir yol olarak da kurallar  **iptables –L –line-numbers** parametresi ile sıra numaralarıyla listelenir. Daha sonra silmek istediğimiz kuralın sıra numarasını yazarak silebilirsiniz.


root@ubuntu# **iptables –L –line-numbers**
root@ubuntu# **iptables –D INPUT 3** --> buradaki 3 line-numbers ile alınan kuralın sıra numarasıdır.
root@ubuntu# **iptables-save  > /etc/iptables/rules.v4**

# LVM Yapılandırması 1
Logical volume yapılandırması ile ilgili örnekler aşağıda anlatılmaktadır.
## LVM oluşturma 1
	Yeni eklenen diskler aşağıdaki  script ile taratılır.
root@ubuntu#  **rescan-scsi-bus.sh**

	Yeni 123 id'li disk ile physical volume oluşturulur.
root@ubuntu# **pvcreate /dev/mapper/123**

	Yeni eklenen 123 id'li disk ile volume group create edilir.
root@ubuntu# **vgcreate vg_oracle /dev/mapper/123**

	logical volume create edilir.
root@ubuntu#  **lvcreate -l 100%FREE vg_oracle -n lv_oracle**

	Oluşturulan lv formatlanır.
root@ubuntu#  **mkfs.xfs /dev/vg_oracle-lv_oracle**

	Reboot sonrası kalıcı olması için fstab eklenir.
root@ubuntu#  **vi /etc/fstab**
**##eklenecek kayit##**
/dev/mapper/vg_oracle-lv_oracle  /oracle xfs defaults 0 0
	
	Oluşturulan lvm yapısı /oracle dizine mount edilir.
root@ubuntu# **mount /oracle**
	
	Dizine ait yetkilendirmeler verilir.
root@ubuntu#  **chown oracle: /oracle**

## LVM oluşturma 2
Eğer SAN üzerinden gelen diskin alias değiştirilip kendiniz diske bir isimlendirme verip  lvm oluşturulmak istenilir ise aşağıdaki adımlar uygulanır.

	Değişiklik yapılmadan önce multipath.conf file backup alınır.
root@ubuntu#  **cp /etc/multipath.conf /etc/multipath.conf.backup**

	Yeni eklenen diskler taratılır.
root@ubuntu#  **rescan-scsi-bus.sh**

	Multipath üzerinden mpath' ler listelenir.
	Yeni eklenen disklerin wwid' leri karşılaştırılır.
root@ubuntu#  **multipath -ll | grep mpath-**

	Yeni eklenen diskler belirlendikten sonra hangi mpath' e denk 
	geliniyor ise o mpath' ler silinir.
root@ubuntu#  **multipath -f mpathXX**

	Multipath config file içerisine yeni eklenen disklerin wwidleri
	verilmek istenilen alias ile girilir. 
root@ubuntu#  **vi /etc/multipath.conf**
**##eklenecek aliasn tanimi##**
multipath {
wwid **3624a93705b4497a3486740d2000122b2**
alias oracle  
}

	multipath komutuyla multipath.config file yeniden yüklenir.
root@ubuntu#  **multipath**

	Yeni oracle alias' lı disk ile physical volume oluşturulur.
root@ubuntu# **pvcreate /dev/mapper/oracle**

	Yeni eklenen disk ile volume group create edilir.
root@ubuntu# **vgcreate vg_oracle /dev/mapper/oracle**

	logical volume create edilir.
root@ubuntu#  **lvcreate -l 100%FREE vg_oracle -n lv_oracle**

	Oluşturulan lv formatlanır.
root@ubuntu#  **mkfs.xfs /dev/vg_oracle-lv_oracle**

	Reboot sonrası kalıcı olması için fstab eklenir.
root@ubuntu#  **vi /etc/fstab**
**##eklenecek kayit##**
/dev/mapper/vg_oracle-lv_oracle  /oracle xfs defaults 0 0
	
	Oluşturulan lvm yapısı /oracle dizine mount edilir.
root@ubuntu# **mount /oracle**
	
	Dizine ait yetkilendirmeler verilir.
root@ubuntu#  **chown oracle: /oracle**

## LVM vgextend ve lvextend etme
	Yeni eklenen diskler taratılır.
root@ubuntu#  **rescan-scsi-bus.sh**

	Yeni disk ile physical volume oluşturulur.
root@ubuntu#  **pvcreate /dev/mapper/124**

	Yeni eklenen disk extend edilmek istenilen vg' ye eklenir.
root@ubuntu#  **vgextend vg_oracle /dev/mapper/oracle02**

	Extend edilmek istenilen lv belirtilir.
root@ubuntu#  **lvextend -L +250G /dev/vg_oracle/lv_oracle**

	Mount edilmiş olan dizin resize edilir.
root@ubuntu# **xfs_growfs /oracle**

	Extend edilmiş alan kontrol edilir.
root@ubuntu# **df -h /oracle**

# Multipath
SAN storage üzerinden eklenen disklerin multipath servisi üzerinden yönetilmesi için aşağıdaki kurulumun yapılması gerekmektedir.

## Multipath tools yükleme

	multipath.tools servisi aşağıdaki şekilde kurulup başlatılır.
root@ubuntu#  **apt install multipath-tools**
root@ubuntu#  **systemctl enable multipathd.service**
root@ubuntu#  **systemctl start multipathd.service**
root@ubuntu#  **systemctl status multipathd.service**

	multipath.conf file ile alias ekleme işlemleri ve ilgili policy tanımlamaları yapılır.
root@ubuntu#  **vi /etc/multipath.conf**
	
	san storage üzerinden gelen tüm diskler listelenir.
root@ubuntu#  **multipath -ll**

	Belirtilen mpath silinir. 
root@ubuntu#  **mpath -f mpathAA**

	multipath.conf yeniden yüklenir.
root@ubuntu#  **multipath**

# Firewall

Ubuntu işletim sistemi üzerindeki local firewall durumunun kontrol edilmesi gereken service ufw dir.

## Firewall servisinin kontrol edilmesi
	Firewall servisinin durumunun kontrol edilmesi
root@ubuntu#**systemctl status ufw**

	Firewall servisinin yeniden başlatılması
root@ubuntu#**systemctl restart ufw**

	Firewall servisinin durdurulması
root@ubuntu#**systemctl stop ufw**

	Firewall servisinin otomatik başlaması
root@ubuntu#**systemctl enable ufw**

	Firewall servisinin otomatik başlamaması
root@ubuntu#**systemctl disable ufw**


	Belirli portların açılması için;
root@ubuntu#**ufw allow 20/tcp**
root@ubuntu#**ufw allow 21/tcp**

	Belirli port aralığının açılması
root@ubuntu#**ufw allow 40000:50000/tcp**
root@ubuntu#**ufw reload**
 
 ## Portların kontrol edilmesi

Açık olan portların hangisi olduğunu listelemek için netstat service kullanılmaktadır.
Eğer sunucuda yüklü değil ise net-tools paketini yükleyerek netstat komutunu çalıştırabilirsiniz.
root@ubuntu#**apt install net-tools**
root@ubuntu#**netstat -vpntl**

# Limits yapılandırması

/etc/security/limits.conf  ve /etc/sysctl.conf  dosyasına kalıcı olarak saklanmasını istediğimiz limitleri tanımlayabiliriz. 

## Security limits ve kernel sysctl.conf parametrelerin belirlenmesi

	Belirlenecek olan limitler ilgili config file kayıt edilir.
root@ubuntu#  **vi /etc/security/limits.conf**
root@ubuntu# **sysctl -p**

	sysctl içerisine ilgili parametreler girilir ve kayıt edilir.
root@ubuntu#  **vi /etc/sysctl.conf**
root@ubuntu# **sysctl -p**


