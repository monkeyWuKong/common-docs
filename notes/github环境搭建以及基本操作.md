#GitHub

##设置git

###设置用户名
[Setting your username in Git](https://help.github.com/articles/setting-your-username-in-git/#platform-linux)

用户名与你的github账号是不一样的，你随时可以更改。用户名在今后的push记录中会出现。对于以前的push记录，显示的会是老的用户名。

**全局用户名**

```
$ git config --global user.name "Mona Lisa"
```
确认设置正确：
```
$ git config --global user.name
> Mona Lisa
```

**为单独的仓库设置用户名**

转到对应仓库的目录：
```
$ git config user.name "Mona Lisa"
```
确认：
```
$ git config user.name
> Mona Lisa
```

###设置邮件地址

[Setting your email in Git](https://help.github.com/articles/setting-your-email-in-git/)

...

