# 常用服务器ssh、ftp

## 1. Linux常用服务器构建-ssh

### <1>ssh介绍
SSH为Secure Shell的缩写，由 IETF 的网络工作小组（Network Working Group）所制定；SSH 为建立在应用层和传输层基础上的安全协议。

SSH是目前较可靠，专为远程登录会话和其他网络服务提供安全性的协议。常用于远程登录，以及用户之间进行资料拷贝。

利用SSH协议可以有效防止远程管理过程中的信息泄露问题。SSH最初是 UNIX 系统上的一个程序，后来又迅速扩展到其他操作平台。SSH 在正确使用时可弥补网络中的漏洞。SSH 客户端适用于多种平台。几乎所有 UNIX 平台—包括 HP-UX、Linux、AIX、Solaris、Digital UNIX、Irix，以及其他平台，都可运行SSH。

使用SSH服务，需要安装相应的服务器和客户端。客户端和服务器的关系：如果，A机器想被B机器远程控制，那么，A机器需要安装SSH服务器，B机器需要安装SSH客户端。


### <2>安装ssh

A.安装ssh服务器

    sudo apt-get install openssh-server

B.远程登陆

    ssh 用户名@IP

使用ssh访问，如访问出现错误。可查看是否有该文件 ～/.ssh/known_ssh 尝试删除该文件解决。

### <3>使用ssh客户端连接服务器

1. 使用ssh命令客户端连接服务器
SSH 告知用户，这个主机不能识别，这时键入"yes"，SSH 就会将相关信息，写入" ~/.ssh/know_hosts" 中，再次访问，就不会有这些信息了。然后输入完口令,就可以登录到主机了。

![](/Images/02day/ssh命令登录.png)

1. 使用ssh第三方客户端连接服务器
![](/Images/02day/putty远程登录.png)


### <4>. scp 

scp(secure copy): 安全拷贝文件,scp 的常用方法：

1.使用该命令的前提条件要求目标主机已经成功安装openssh-server

    如没有安装使用 sudo apt-get install openssh-server 来安装

2.使用格式：

    scp -r 目标用户名@目标主机IP地址：/目标文件的绝对路径  /保存到本机的绝对/相对路径

	举例：
    scp -r itcast@192.168.1.100:/home/itcast/QQ_dir/ ./mytest/lisi
		
	在后续会提示输入“yes”此时，只能输“yes”而不能简单输入“Y”

拷贝单个文件可以不加 -r参数，拷贝目录必须要加。


本地文件复制到远程：
```
scp FileName RemoteUserName@RemoteHostIp:RemoteFile
scp FileName RemoteHostIp:RemoteFolder
scp FileName RemoteHostIp:RemoteFile
```


本地目录复制到远程：
```
scp -r FolderName RemoteUserName@RemoteHostIp:RemoteFolder
scp -r FolderName RemoteHostIp:RemoteFolder
```

远程文件复制到本地：
```
scp RemoteUserName@RemoteHostIp:RemoteFile FileName
scp RemoteHostIp:RemoteFolder FileName
scp RemoteHostIp:RemoteFile FileName
```

远程目录复制到本地：
```
scp -r RemoteUserName@RemoteHostIp:RemoteFolder FolderName
scp -r RemoteHostIp:RemoteFolder FolderName
```

![](/Images/02day/Snip20161219_120.png)


###<5>. sftp 

>sftp(Secure File Transfer Protocol)，安全文件传送协议。可以为传输文件提供一种安全的网络的加密方法。sftp基于ssh 实现安全传输文件，sftp 与 ftp 有着几乎一样的语法和功能，比ftp安全性更高，但是传输速度比ftp要低

>linux下直接在终端中输入：sftp username@remote ip(or remote host name)。出现验证时，只需填入正确的密码即可实现远程链接。登入成功后终端呈现出:sftp>....
在sftp的环境下的操作就和一般ftp的操作类似了，ls,rm,mkdir,dir,pwd,等指令都是对远端进行操作，如果要对本地操作，只需在上述的指令上加‘l’变为：lls,lcd, lpwd等。
上传：put /path/filename(本地主机) /path/filename(远端主机)；
下载：get /path/filename(远端主机) /path/filename(本地主机)。 















