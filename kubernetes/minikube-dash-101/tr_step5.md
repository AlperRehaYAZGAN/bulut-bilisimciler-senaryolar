### Dashboard

`minikube addons enable dashboard` komutu ile Minikube kullanarak dashboard etkinleştirilir.

`kubectl apply -f /opt/kubernetes-dashboard.yaml` komutu ile  YAML dosyasını ekleyerek Kubernetes Dashboard'u kullanılabilir hale getirilir. (Sadece Bulut Bilişim Akademi'de kullanılabilir.)

Kubernetes dashboard'u, uygulamalarınızı bir kullanıcı arayüzünde görüntülemenize olanak tanır. Bu dağıtımda, dashboard 30000 numaralı port'dan kullanıma sunulmuştur ancak başlaması biraz zaman alabilir.

`kubectl get pods -n kubernetes-dashboard -w` komutu ile Dashboard'un ilerleme durumu, kube-system namespace'indeki Pod'ları izlenir.

Çalıştırıldığında, kontrol panelinin URL'i https://2886795285-30000-kitek05.environments.bulutbilisimakademi.com/ şeklindedir.
