## Kubernetes Ortamı Kurulumu ve ArgoCD Hazır Hale Getirilmesi  

+ Kubernetes ortamının ArgoCD'ye hazır hale getirilmesi.

Öncelikle node1 makinemize kubernetes master rolü ile ayağa kalkması ve hazırlanması için aşağıdaki komutu yazıyoruz.  

`kubeadm init --apiserver-advertise-address $(hostname -i) --pod-network-cidr 10.5.0.0/16`  (Bu komut uzun sürmektedir.)  

Makineler arası haberleşme için cluster networking aktifleştiriyoruz: `kubectl apply -f https://raw.githubusercontent.com/cloudnativelabs/kube-router/master/daemonset/kubeadm-kuberouter.yaml`
  
Kubeadm init komut çıktısına geri dönüyoruz. Master makinemize worker rolüne sahip makineleri ekleyebilmemiz için master makinesinde çalıştırdığımız "kubeadm init" sorgu sonucunda çıkan `kubeadm join ${MASTER_IP_PORT} --token ${MASTER_TOKEN} --discovery-token-ca-cert-hash sha256:${MASTER_SHA256_TOKEN}` yapısındaki kodu buluyoruz ve node2 ve node3 isimli iki makine daha oluşturarak bu kodu oradaki makinelere yapıştırıyoruz.  

Worker makinelerde:  
`kubeadm join ${MASTER_IP_PORT} --token ${MASTER_TOKEN} --discovery-token-ca-cert-hash sha256:${MASTER_SHA256_TOKEN}`  

Bu kodun çalışması sonucunda ana master makinemize gelip `kubectl get nodes` diyoruz ve eklediğimiz worker makineler ile birlikte ekran çıktımız:  

```
NAME    STATUS   ROLES                  AGE   VERSION
node1   Ready    control-plane,master   45s   v1.20.1
node2   NotReady <none>                 10s   v1.20.1
node3   NotReady <none>                 9s    v1.20.1
```  

Makinelerimiz NotReady durumundan Ready durumuna gelene kadar bekliyoruz. Worker node eklenmesi tamamlandığında `kubectl get nodes` komutumuzun çıktısı aşağıdaki gibi olmalıdır:  

```
NAME    STATUS   ROLES                  AGE   VERSION
node1   Ready    control-plane,master   20m   v1.20.1
node2   Ready    <none>                 19m   v1.20.1
node3   Ready    <none>                 19m   v1.20.1
```  

Kubernetes ortamımız kurulduğuna göre ArgoCD kurulumuna geçebiliriz.
