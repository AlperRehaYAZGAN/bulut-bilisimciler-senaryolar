## Ansible ile Otomasyona Giriş 
### Seviye: Başlangıç  
Bu örnek ortamımızda interaktif örnekler ile Ansible'ın temel yapısını inceleyeceğiz.

#### Ansible Temel Kavramlar

Ansible, manuel olarak yaptığınız işleri otomatize etmenizi sağlayan bir otomasyon tool’udur. Birçok modülü sayesinde network cihazlarınızdan bulut ortamlarına kadar kullandığınız sunuculara geniş kapsamlı otomasyon hizmeti sunmanızı sağlar.

Ansible’ın temel yapısını incelemek istersek;

**Control Node:** Ansible’ın kurulu olduğu makinedir. Bu makine üzerinden ansible komutlarını, playbook’larını çalıştırabiliriz.

**Managed Nodes:** Ansible tarafından yönetilen makinelerdir. Örneğin bir playbook’un uygulanmasını istediğimiz hostumuz bu yapıdaki managed node olacaktır.

![Mimari](https://miro.medium.com/max/963/0*9tjXPw5vgixFz6I3)

Ayrıca Ansible ile çalışmaya başladığımızda aşağıdaki terimleri de sıklıkla duyacağız.

**Modules:** Ansible’ın farklı görevler için oluşturulmuş kod kümeleridir. Ansible’ın zengin bir modül kütüphanesi bulunmaktadır.

**Inventory:** Ansible komutlarının uygulandığı hostların tamamını kapsayan envanter diyebiliriz.
Kullanım amacınıza göre farklı farklı bir çok envanter ya da tüm hostlarınız için tek bir envanter oluşturabilirsiniz. 

Inventory oluşturduktan sonra içerisine girip “hosts” kısmına playbook'un çalışırken bağlanacağı değişkeni ekleyebilirsiniz. Bu değişken bir sunucu olabileceği gibi bir network cihazı da olabilir. Bu gibi farklılıklarda inventory dosyanızı ayırmak yönetim açısından sizi rahatlatacaktır.

**Playbooks:** Otomasyon ile yapılacak görevlerin toplandığı dosyadır. YAML formatındadır. Mesela envanterdeki tüm sunuculara remote bağlantı sağlayıp backup scriptini başlat şekilinde bir playbook’umuz olabilir. Ad-hoc komutlarını YAML formatına dönüştürerek kolaylıkla playbook oluşturabiliriz.

![playbook)](https://miro.medium.com/max/963/0*BxInjuE_acj1N6fe)

***NOT:*** Ansible ad-hoc komutları, tek bir görevi (task) yerine getirmek içi komut satırını kullanarak ansible'ı çalıştırma şeklimizdir. Hızlı ve kolay bir şekilde uygulanabilirler fakat tekrar tekrar kullanılmaları pratikte pek mümkün değildir. 

Gelin şimdi biraz pratik yaparak öğrendiklerimizi pekiştirelim.  