### Mini Kube'e Giriş

Minikube, Kubernetes'i yerel olarak çalıştırmayı kolaylaştıran bir araçtır. Minikube, Kubernetes'i denemek veya her gün geliştirmeler yapmak isteyen kullanıcılar için bilgisayarınızda bir VM içinde single-node bir Kubernetes kümesi çalıştırır.

Daha fazla detaya buradan ulaşabilirsiniz. https://github.com/kubernetes/minikube

 Minikube şuanda ortama indirilmiş ve configüre edilmiştir. 

 `minicube version` komutu ile kontrol edip, versiyon bilgisini öğrenebilirsiniz.

 `minicube start --wait=false` komutu ile cluster'ı başlatabilirsiniz.

 Harika! Artık terminalinizde çalışan bir Kubernetes cluster'ınız var. Minikube sizin için bir sanal makine başlattı ve şimdi bu VM'de bir Kubernetes cluster'ı çalışıyor.
