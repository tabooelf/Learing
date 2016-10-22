## create a new repository on the command line

```php
echo "# learngit" >> README.md //输出echo
git init  //初始化本地库
git add README.md  //添加文件到暂存区
git commit -m "first commit"  //暂存区提交到库
git remote add origin git@github.com:tabooelf/learngit.git //增加远程库
git push -u origin master //更新关联远程库
```

