## Install Jekyll

>centos 1511 (7.2)

`yum install -y ruby ruby-devel`

`gem install jekyll`

ok

>Fedora 26 

`yum install -y ruby ruby-devel`

`sudo dnf install redhat-rpm-config`

`gem install bundler`

`gem install jekyll`

ok

## start

> in Fedora

**start a project**

`jekyll new mysite`


**start the local server**

`jekyll serve -H 192.168.1.166`

**build project**

`jekyll build`