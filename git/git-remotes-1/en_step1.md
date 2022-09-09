## Senaryo 1 - Remote Repository

** Remote ** repository olarak github kullanacağımız için öncesinde aşağıdaki yönergeleri takip ederek github hesabınızda kullanmak üzere bir adet **token** oluşturmanız gerekmektedir.

**Git Clone** ile uzak repository de bulunan master branch  local alana alınır. 
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