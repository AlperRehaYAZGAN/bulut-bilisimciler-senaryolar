### Kubernetes Çoklu Worker Ortamı Kurulumu  

Bu senaryo ile Kubernetes ortamınızda birden fazla worker node oluşturup, master node üzerinden bu worker node'lara erişebilir hale getireceksiniz. Başlayalım 🎬...  

Öncelikle node1 makinemize kubernetes master rolü ile ayağa kalkması ve hazırlanması için aşağıdaki komutu yazıyoruz.  

- Master Kurulumu(Node1 mmakinesinde)  
`kubeadm init --apiserver-advertise-address $(hostname -i) --pod-network-cidr 10.5.0.0/16`  (Bu komut uzun sürmektedir. Tamamlanmasını bekleyiniz.)  

Master makinesini ayağa kaldırdıktan sonra ise makineler arası haberleşme için cluster networking aktifleştiriyoruz: `kubectl apply -f https://raw.githubusercontent.com/cloudnativelabs/kube-router/master/daemonset/kubeadm-kuberouter.yaml`  

- Worker Kurulumları(Node2 ve Node3 makinelerinde)  
Kubeadm Kubernetes Cluster kurulumunda Worker rolüne sahip makineler ekleyebilmemiz için Master rolüne sahip makinemizi ilk çalıştırdığımız zaman oluşan anahtarı kullanmamız gerekmektedir. Kubeadm init komut çıktısına geri dönüyoruz. Master makinemize worker rolüne sahip makineleri ekleyebilmemiz için master makinesinde çalıştırdığımız **kubeadm init** sorgu sonucunda çıkan `kubeadm join ${MASTER_IP_PORT} --token ${MASTER_TOKEN} --discovery-token-ca-cert-hash sha256:${MASTER_SHA256_TOKEN}` yapısındaki kodu buluyoruz ve node2 ve node3 isimli iki makineye geçiş yapıp çalıştırıyoruz. 

Worker makinelerde(Node2, Node3):  
`kubeadm join ${MASTER_IP_PORT} --token ${MASTER_TOKEN} --discovery-token-ca-cert-hash sha256:${MASTER_SHA256_TOKEN}`  

Bu kodun çalışması sonucunda ana master makinemize geçiyoruz ve worker makineler ile birlikte aşağıdaki komutu çalıştırıyoruz ve ekran çıktımızı inceliyoruz:  
`kubectl get nodes`  

```
NAME    STATUS   ROLES                  AGE   VERSION
node1   Ready    control-plane,master   45s   v1.20.1
node2   NotReady <none>                 10s   v1.20.1
node3   NotReady <none>                 9s    v1.20.1
```  

Makinelerimiz **NotReady** durumundan **Ready** durumuna gelene kadar bekliyoruz. Worker node eklenmesi tamamlandığında `kubectl get nodes` komutumuzun çıktısı aşağıdaki gibi olmalıdır:  

```
NAME    STATUS   ROLES                  AGE   VERSION
node1   Ready    control-plane,master   20m   v1.20.1
node2   Ready    <none>                 19m   v1.20.1
node3   Ready    <none>                 19m   v1.20.1
```  

Kubernetes ortamımız kurulduğuna göre test edebilecğeimiz uygulamaların kurulumuna geçebiliriz.
