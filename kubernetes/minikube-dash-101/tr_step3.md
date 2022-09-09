### Cluster Bilgileri

Cluster, kubectl CLI kullanılarak etkileşime girebilir. Bu, Kubernetes'i ve cluster üzerinde çalışan uygulamaları yönetmek için kullanılan ana yaklaşımdır.

`kubectl cluster-info` komutu ile cluster'ın detay bilgilerini ve 'health' durumunu görüntüleyebilirsiniz.

`kubectl get nodes` komutu ile cluster'ın kullandığı node'ları görüntüleyebilirsiniz.

Node "NotReady" olarak işaretlenmişse component'leri başlatıyor demektir.

Bu komut, uygulamalarımızı barındırmak için kullanılabilecek tüm node'ları gösterir. Artık yalnızca bir node'umuz var ve durumunun hazır olduğunu görebiliyoruz (deployment için başvuruları kabul etmeye hazır).
