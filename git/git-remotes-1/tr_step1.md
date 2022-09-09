## Senaryo 1 - Remote Repository

** Remote ** repository olarak github kullanacağımız için öncesinde aşağıdaki linkde belirtilen yönergeleri takip ederek github hesabınızda kullanmak üzere bir adet **token** oluşturmanız gerekmektedir.

"https://docs.github.com/en/enterprise-server@3.4/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token"

**Git Clone** ile uzak repository de bulunan master branch  kendi bilgisayarımıza alabiliriz. Burada kullanıcı adınız, token ve proje adınız ilgili komut içerisinde değiştirilmelidir. 
```
git clone https://<username>:<git_user_token>@github.com/<username>/<project_name>.git
```
```
cd <project_name>
```
```
cat .git/config
```
```
git show-ref master
```