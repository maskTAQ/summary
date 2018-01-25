## 1、清除git的全局设置
新安装git跳过这一步。如果对git设置过的user.name和user.email，类似这种设置过：

$ git config --global user.name "your_email_prefix"
$ git config --global user.email  "your_email"

必须首先删除该设置， 不然会冲突的。取消全局设置方法：

$ git config --global --unset user.name "your_email_prefix"
$ git config --global --unset user.email "your_email"

## 2、生成新的SSH keys
生成ssh keys命令：

$ ssh-keygen -t rsa -C "your_email"
一般直接回车，默认生成id_rsa和id_rsa.pub，id_rsa私钥_rsa_pub公钥。多个git账户不行，需要注意，出现提示输入文件名的时候(Enter file in which to save the key (~/.ssh/id_rsa): id_rsa_chen)要输入与默认配置不一样的文件名，比如：我这里填的是 id_rsa_personage，另一个是 id_rsa_company

查看生成的ssh keys $ open ~/.ssh

## 3、添加并识别新的SSH keys私钥
因为默认只读取id_rsa，为了让SSH识别新的私钥，需将其添加到SSH agent中 
命令：
$ ssh-agent bash
$ ssh-add ~/.ssh/id_rsa_personage
$ ssh-add ~/.ssh/id_rsa_company
比如:需要分别添加id_rsa_personage和id_rsa_company。特别注意，如果后边出行权限问题：Permission denied（Publickey),很可能是私钥没有导入ssh-agent中

## 4、添加新的SSH keys到Git账号的SSH设置中
将新生成的公钥id_rsa_*.pub添加到你的另一个github帐号(或者公司的gitlab)下的SSH Key中。 

## 5、配置~/.ssh/config文件
创建config文件，如果没有的话
$ touch ~/.ssh/config        # 创建config文件
配置config文件信息
```config
#personage account  
Host github.com  
Hostname github.com  
PreferredAuthentications publickey
User masktaq  
IdentityFile ~/.ssh/id_rsa_personage
  
#company account  
Host github.com  
Hostname github.com  
PreferredAuthentications publickey
User taiaiqiang  
IdentityFile ~/.ssh/id_rsa_company
```

## 6、验证连接Git
连接git命令：

$ ssh -T git@github.com
Hi you user name! You've successfully authenticated, but GitHub does not provide shell access.
 上面是github的成功返回语句

## 7.使用git仓库的时候使用ssh地址。