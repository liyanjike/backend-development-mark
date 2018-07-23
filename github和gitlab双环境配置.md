# mac系统同时配置github与gitlab环境
***
&emsp;对于使用分布式版本控制系统git的很多开发者来说，他们也许在开发过程中遇到一个问题：公司使用内部局域网才能登陆的gitlab，而个人开发项目和一些个人学习则需要放置在github上。这时，开发者们需要在系统中同时配置github和gitlab两个版本控制系统的环境。
***

## 1.什么是公钥和私钥？
&emsp;文件传输过程中，文件加密是非常重要的一环。无论是github还是gitlab，他们都使用ssh协议来防止远程管理过程中的信息泄露问题。ssh的加密机制中采用了RSA非对称加密，即同时存在公钥和私钥。用户将自己的公钥存储在远程主机，登录时，远程主机会向用户发送一条消息，用户用自己的私钥加密后，再发给服务器。远程主机用事先存储的公钥进行解密，如果成功，就证明用户可信。至此，用户才能在本地git仓库中进行pull和push的操作，否则操作无法进行！
## 2.生成公钥和私钥
&emsp;mac系统中进入文件夹 cd ~/.ssh，如果不存在该文件夹可新建一个.ssh文件夹；若存在且为空，那么可以在命令行中开始配置环境了<br>

执行下面命令行同时生成公钥和私钥<br>
```
ssh-keygen -t rsa -C "注册 gitlab 账户的邮箱" 
```

&emsp;此处参数C一定要大写

&emsp;提示输入名称时输入gitlab标识字样增加可读性，之后两个密钥文件将以此命名，比如id\_rsa\_lab

执行下面命令行同时生成公钥和私钥<br>
```
ssh-keygen -t rsa -C "注册 github 账户的邮箱" 
```

同理，输入以github标识的名称，比如id_rsa_hub<br>

## 3.公钥需要提交给远端git服务器
&emsp;在～/.ssh文件夹下，分别cat + id\_rsa\_hub.pub和id\_rsa\_lab.pub文件，将他们分别配置到github和gitlab网页的SSH keys中
## 4.更新SSh配置
&emsp;在～/.ssh路径下输入命令行vim + config，添加github和gitlab的用户配置信息<br>
&emsp;在文件夹内添加如下内容<br>

```
    Host github.com
    HostName github.com
    User githubuser@xyz.com
    IdentityFile ~/.ssh/id_rsa_github

    Host gitlab.com
    HostName gitlab.com
    User gitlabuser@xyz.com
    IdentityFile ~/.ssh/id_rsa_gitlab
    
```

##5.配置仓库用户信息
&emsp;在公司内部，gitlab更为常用，可配置为全局用户信息<br>

```
git config --global user.name "gitlabuser"<br>
git config --global user.email "gitlabuser@xyz.com"

```

&emsp;进入本地 github 仓库配置 git 用户信息<br>

```
~/github$ git config --local user.name "githubuser"
~/github$ git config --local user.email "githubuser@xyz.com"
```
