
### centos7 升级vim8

```
yum remove vim -y
yum install ncurses-devel python-devel -y
git clone https://github.com/vim/vim.git
cd vim/src

打开Makefile
CONF_OPT_PYTHON = --enable-pythoninterp

make
make install
#设置环境变量，打开`/etc/profile`,最后一行写入
PATH=$PATH:/usr/local/bin/
```

如果之前没有python支持，增加python支持，则需要重新编译

```
cd vim/src
make distclean
./configure --enable-pythoninterp=yes --with-python-config-dir=/usr/lib/python2.7/config
make
make install
```

### 安装文件浏览器nerdtree

插件官网： http://www.vim.org/scripts/script.php?script_id=1658

github： https://github.com/scrooloose/nerdtree

```
git clone https://github.com/scrooloose/nerdtree.git ~/.vim/bundle/nerdtree
```
