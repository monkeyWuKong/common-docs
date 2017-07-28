
## [NIS](https://en.wikipedia.org/wiki/Network_Information_Service)

参考维基百科。

Network Information Service, 原来也称为 Yellow Pages or YP （黄页）, 一种C/S架构的目录服务协议，专门用于分布式系统相关的配置数据，如电脑和电脑网络之间的用户，主机名等。

因为British Telecom公司已经拥有了“Yellow Pages”的商标，因此sun就将自己系统的名字改成了NIS，但是NIS的很多命令，函数仍然是以'yp'开头。

A NIS/YP system maintains and distributes a central directory of **user** and **group** information, **hostnames**, **e-mail aliases** and **other text-based tables of information** in a computer network. 

For example, in a common UNIX environment, the list of users for identification is placed in /etc/passwd, and secret authentication hashes in /etc/shadow. NIS adds another "global" user list which is used for identifying users on any client of the NIS domain.

Administrators have the ability to configure NIS to serve password data to outside processes to authenticate users using various versions of the Unix crypt(3) hash algorithms. However, in such cases, any NIS(0307) client can retrieve the entire password database for offline inspection. **Kerberos** was designed to handle authentication in a more secure manner.


### 接替技术

原来的NIS设计貌似有固有的局限性，特别是在可扩展性和安全性的领域，所以其他的技术出现了以代替它。

后面的NIS+的出现也并没有改善多少局面。

随着时间推移，LDAP（轻量级目录访问协议）出现。

