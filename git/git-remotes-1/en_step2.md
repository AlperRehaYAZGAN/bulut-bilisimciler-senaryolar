## Senaryo 2 - Senkronizasyon
```
echo "Python 2.1" >> icerik/python.txt
```
```
git add icerik/python.txt
```
```
git commit  -m "Local Repo Added Python 2"
```
```
git  log
```
```
git show-ref  master
```
```
git remote add origin https://<username>:<git_user_token>@github.com/<username>/<project_name>.git
```
```
git push 
```
**git clone** aşamasında bir token tanımlamadıysanız aşağıdaki yönergeyi push adımında uygulayabilirsiniz. 
```
git remote add origin https://<username>:<git_user_token>@github.com/<username>/<project_name>.git
```
```
git branch
```
```
git push -u origin master
```