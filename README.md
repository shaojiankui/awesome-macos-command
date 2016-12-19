# awesome-macos-command  [![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/sindresorhus/awesome)
awesome-macos-command, As developer use your macOS terminal command statements to do awesome things.

很棒的macOS命令行，作为开发者，使用你的macOS终端命令语句做些很棒的事情。

## 目录

- [Xcode相关命令](#Xcode相关命令)
    - [xcode-select](#xcode-select)
    - [xcodebuild](#xcodebuild)
    - [xcrun](#xcrun)
- [Git](#git)
    - [SSH Key](#ssh_key)
    - [创建与上传](#创建与上传)
    - [分支 branch](#branch)
- [签名相关命令](#签名相关命令)
- [RubyGems](#rubygems)
- [CocoaPods](#cocoapods)
- [Brew](#brew)
- [SVN](#svn)
- [openssl](#openssl)
- [lipo](#lipo)
- [openssl](#openssl)
- [mac地址](#mac地址)
- [curl](#curl)
- [spctl](#spctl)


.......................

## Xcode相关命令
### xcode-select
#### 安装 Command Line Tools

```
xcode-select --install
```
#### 当前Xcode路径

```
xcode-select --print-path
```
#### 切换Xcode

```
xcode-select -switch xcode_folder_path
```
#### xcode-select版本

```
xcode-select -version
```
### xcodebuild
#### 查看xcode的版本号和build版本

```
xcodebuild -version
```

#### 显示当前系统的sdk、及其版本

```
xcodebuild -showsdks
```
#### 显示工程项目信息

```
 xcodebuild -list
```
#### build工程

```
xcodebuild -sdk iphonesimulator10.0
```
#### build Debug工程

```
xcodebuild -sdk iphonesimulator10.0 -configuration Debug
```
#### clean工程

```
xcodebuild clean -sdk iphonesimulator10.0 -configuration Debug
```
### xcrun
#### 删除不可用的模拟器

```
xcrun simctl delete unavailable
```
### 获取xcode uuid

```
defaults read /Applications/Xcode.app/Contents/Info.plist DVTPlugInCompatibilityUUID
```

## Git
### SSH_KEY
#### 生成SSH KEY

```
ssh-keygen -t rsa -C “your_email@youremail.com”
```
#### 验证SSH KEY

```
ssh -T git@github.com
```
### 创建与上传
####  配置Git信息

```
git config --global user.name "username"

git config --global user.email "your_email@youremail.com"
```
#### 创建项目及上传

```
git init // 初始化Git仓库

git add . //添加所有文件(只是在本地准备好，注意那个“.”表示所有文件)

git commit -m 'create project' //引号中是说明信息

git remote add origin git@github.com:shaojiankui/JKCategories.git //添加远程Git地址

git push origin master  //上传到远程git
```

#### 修改本地文件

```
git add . //修改好本地文件后，如果添加了内容则要先git add

git commit -a -m 'new feature' //修改(本地)
```
#### 上传

```
git push <远程主机名> <本地分支名>:<远程分支名>
```

```
git push origin master 
```
上传到远程git,将本地的master分支推送到origin主机的master分支。如果后者不存在，则会被新建。

如果省略本地分支名，指定远程分支名，则表示删除指定的远程分支，因为这等同于推送一个空的本地分支到远程分支。

```
git push origin :master
//等同于
git push origin --delete master
```
### 分支 branch
#### 列出本地分支

```
git branch
```
#### 列出远程分支

```
git branch -r
```
#### 列本地分支和远程分支

```
git branch -a
```
#### 创建一个新的本地分支

```
git branch newbranch
```
#### 以v2.6为start-point创建本地分支
```
git branch newbranch2.6 v2.6
```
#### 把分支推到远程分支
```
git push origin newbranch2.6 
```
#### 切换分支
```
git checkout  newbranch2.6 
```

#### 重命名分支

```
git branch -m | -M oldbranch newbranch
```
如果newbranch名字分支已经存在，则需要使用-M强制重命名，否则，使用-m进行重命名。
#### 删除本地branchname分支

```
git branch -d | -D branchname
```
#### 删除远程branchname分支

```
git branch -d -r branchname
git push origin :branchname //推送到服务器
```

### tag
#### 显示本地 tag
```
git tag 或者 git tag -l
```
#### 切换到标签
与切换分支命令相同

```
git checkout tagname //查看标签信息
```

用git show命令可以查看标签的版本信息：

```
git show 1.4
```

#### 创建一个tag

```
git tag -a 1.4 -m 'version 1.4' //注解：git tag 是打标签的命令，-a 是添加标签，其后要跟新标签号，-m 及后面的字符串是对该标签的注释。

git push origin –tags  //上传所有tag到远程git
```
####  给指定的commit打tag
打标签不必要在head之上，也可在之前的版本上打，这需要你知道某个提交对象的SHA（通过git log获取）。

```
git tag -a 1.5 0ea9addc03b44e73415c8fadb5e73999f569fc21
```

#### 删除某个tag

```
git tag -d 1.4 //删除本地tag

git push origin :refs/tags/1.4 //删除服务器tag
```

## 签名相关命令
#### 快捷查看系统中能用来对代码进行签名的证书

```
security find-identity -v -p codesigning 
```
#### 对未签名app手动签名

```
codesign -s 'iPhone Developer: 6077782@qq.com (W26TLN2W63)' Example.app

```
#### 对已签名app重新签名
为了重新设置签名，你必须带上 -f 参数，有了这个参数，codesign 会用你选择的签名替换掉已经存在的那一个：

```
codesign -f -s 'iPhone Developer: 6077782@qq.com (W26TLN2W63)' Example.app

```
#### 查看指定app的签名信息
codesign 还可以为你提供有关一个可执行文件签名状态的信息，这些信息在出现不明错误时会提供巨大的帮助：

```
codesign -vv -d Example.app
```
#### 验证签名文件的完整性

```
codesign --verify Example.app
```
#### 查看授权文件 entitlements.plsit

```
codesign -d --entitlements - Example.app
```
#### 查看描述文件.mobileprovision

```
security cms -D -i test.mobileprovision
```
#### 解析描述文件绑定的证书

```
security cms -D -i test.mobileprovision | perl -nle 'print $& if m{(?<=<data>).*?(?=</data>)}' | base64 -D > mobile.cer

```
## RubyGems
#### 查看当前使用的镜像站

```
gem sources -l
```
#### 删除镜像源

```
gem sources --remove https://rubygems.org 
```
#### 添加镜像源

```
gem sources --add http://gems.ruby-china.org/
```
#### 更新RubyGems

```
sudo gem update -n /usr/local/bin --system
//如果 gem -v还是老版本，执行
sudo update_rubygems
```
#### 安装或者升级CocoaPods等软件包

```
sudo gem install -n /usr/local/bin GEM_NAME_HERE
```
## CocoaPods
#### 安装或者升级pod

```
sudo gem install -n /usr/local/bin cocoapods
```
#### pod版本号

```
pod --version
```

#### 切换pod版本库源
 先删除，再添加，再更新

```
pod repo remove master
pod repo add master http://git.oschina.net/akuandev/Specs.git
//pod repo add master https://gitcafe.com/akuandev/Specs.git
pod repo update
```
#### 搜索Pods

```
pod search AFNetworking
```

#### 设置pod仓库

```
pod setup
```
#### pod库更新
执行pod install和pod update的时候，cocoapods都会默认更新一次spec仓库比较耗时作。如果spec版本库不需要更新，给这两个命令加一个参数(--no-repo-update)跳过spec版本库更新
```
pod install --no-repo-update
pod update --no-repo-update
```

## Brew

### 列出已安装的软件
```
brew list
```
### 更新brew
```
brew update 
```
### 显示包依赖
```
brew deps
```
### 安装软件

```
brew install softname
```
### 卸载软件

```
brew uninstall softname
```
### 模糊搜索软件 

```
brew search /softna*/ //
```
## SQL
## SVN
#### 将文件checkout到本地目录

```
svn checkout svn://192.168.1.1/pro/domain
```

#### 往版本库中添加新的文件

```
svn add file
svn add *.php  //(添加当前目录下所有的php文件)
```
#### 将改动的文件提交到版本库
 svn commit -m "LogMessage" [-N] [--no-unlock] PATH(如果选择了保持锁，就使用–no-unlock开关)
```
svn commit -m "add test file for my test" test.php
svn ci //简写
```
#### 加锁/解锁

```
svn lock -m "LockMessage" [--force] PATH
svn lock -m "lock test file" test.php
svn unlock PATH
```
#### 更新到某个版本

```
svn update -r m path
svn up //简写
```
svn update如果后面没有目录，默认将当前目录以及子目录下的所有文件都更新到最新版本。

svn update -r 200 test.php(将版本库中的文件test.php还原到版本200)

svn update test.php(更新，于版本库同步。如果在提交的时候提示过期的话，是因为冲突，需要先update，修改文件，然后清除svn resolved，最后再提交commit)

#### 查看文件或者目录状态

```
svn status path //（目录下的文件和子目录的状态，正常状态不显示）,【?：不在svn的控制中；M：内容被修改；C：发生冲突；A：预定加入到版本库；K：被锁定】
```
#### 删除文件

```
svn delete svn://192.168.1.1/pro/domain/test.php -m "delete test file"
//或者
delete test.php 
svn ci -m 'delete test file'

```
#### 查看日志

```
svn log path
```
#### 查看文件详细信息

```
svn info path
```
#### 比较差异

```
svn diff -r m:n path(对版本m和版本n比较差异)
```

#### 恢复本地修改

```
svn revert PATH
```

#### 比较差异

```
svn diff -r m:n path(对版本m和版本n比较差异)
```
## Cmake

## macOS shell
### UserDefaults
#### 不再产生.DS_Store

```
defaults write com.apple.desktopservices DSDontWriteNetworkStores true  
```
#### 获取Xcode UUID

```
defaults read /Applications/Xcode.app/Contents/Info.plist DVTPlugInCompatibilityUUID
```
#### 显示隐藏Mac文件的命令

```
defaults write com.apple.finder AppleShowAllFiles -bool true //显示

defaults write com.apple.finder AppleShowAllFiles -bool false //隐藏
```
#### 显示finder文件夹路径

```
defaults write com.apple.finder _FXShowPosixPathInTitle -bool YES
```
#### 修改Xcode开发人员组织信息

```
defaults write com.apple.Xcode PBXCustomTemplateMacroDefinitions '{"ORGANIZATIONNAME"="Baidu";}'

defaults write com.apple.Xcode ORGANIZATIONNAME "Baidu"
```
### find
#### 找出当前目录以及其所有子目录下所有名字中包含“view.h”的文件

```
find . -name "*view.h*"  
```
#### 找出当前目录（不包括子目录）下所有名字中后缀为".rmvb"的文件
```
find . -name "*.rmvb" -maxdept 1
```
#### 打印目录树形层级 与tree类似

```
find . -print | sed -e 's;[^/]*/;|____;g;s;____|; |;g'
```
#### 批量重命名当前目录及其子目录下的.sql为.txt

```
 find . -name '*.sql'| awk -F "." '{print $2}'|xargs -I'{}'  mv ./{}.sql ./{}.txt
```
#### 批量删除.DS_Store

```
find  ./ -name ".DS_Store" | xargs rm -Rf

sudo find ./ -name ".DS_Store" -depth -exec rm {} \;  
```

#### 使gitignore生效

```
find . -iname "Demo-Info.plist" |xargs git rm -rf --cached 
```
#### 统计iOS代码的总行数

```
find . -name "*.m" -or -name "*.h" |xargs grep -v "^$"|wc -l   
//grep -v "^$"是去掉空行
```
#### 统计iOS每个类对应的代码行数

```
find . "(" -name "*.m" -or -name "*.strings" -or -name "*.h" ")" -print | xargs wc -l
```

### lipo
#### 查看静态库指令集

```
lipo -info /Users/Jakey/libData.a 

lipo -detailed_info /Users/Jakey/libData.a  //详细信息

lipo -info /Users/Jakey/libData.Framework/libData 

```
#### 找出不支持arm64的静态库

```
find . -name *.a -exec lipo -info "{}" \;
```
#### 提取armv7架构

```
lipo -thin armv7 libData.a -output libData.a.armv7
```
#### 合并静态库

```
lipo –create Release-iphoneos/libiphone.a Debig-iphonesimulator/libiphone.a –output libiphone.a
```
### 挂载远程NFS

```
sudo mount -t nfs 192.168.1.109:/Share /Users/jakey/nfs

```

### openssl
### 随机生成mac地址

```
openssl rand -hex 6 | sed 's/\(..\)/\1:/g; s/.$//'
```


### 显示Library隐藏目录

```
chflags nohidden ~/Library/
```
## mac地址
#### 查看mac地址

```
ifconfig en0 |grep ether
```

#### 修改mac地址

```
sudo ifconfig en0 ether XX-XX-XX-XX-XX-XX
```
### 随机生成mac地址

```
openssl rand -hex 6 | sed 's/\(..\)/\1:/g; s/.$//'
```
### 列出所有的网络连接方式

```
networksetup -listallnetworkservices
```
### 给指定的网络连接方式设定DNS服务器

```
 sudo networksetup-setdnsservers AirPort 192.168.10.200
```
### 配置DNS域名

```
sudo networksetup -setdnsservers networkservice DNS1 DNS2
sudo networksetup -setdnsservers AirPort 192.168.10.200 8.8.8.8
```

###清空DNS缓存

```
dscacheutil -flushcache
```


### route
#### 释放静态路由

```
sudo route -n flush
```
#### 删除默认路由

```
sudo route delete 0.0.0.0  
```
#### 默认使用192.168.1.1网关

```
sudo route add -net 0.0.0.0 192.168.1.1
```

#### 有线网卡使用该网关

```
sudo route add 10.200.0.0 10.200.22.254
```

#### 其它网段指定网关

```
sudo route add 10.0.1.0/24 10.200.22.254
```

### ifconfig
显示网络接口(interface)信息。如接口名称，接口类型，接口的IP地址，硬件的MAC地址等。
#### 网卡的启动与关闭

```
ifconfig en0 up/down
```
#### 配置IP地址

```
sudo ifconfig en0 192.168.1.33 
```

### ARP
ARP协议用在局域网(LAN)内部。借用ARP协议，设备可以知道同一局域网内的IP-MAC对应关系。当我们访问一个本地IP地址时，设备根据该对应关系，与对应的MAC地址通信。通过ARP工具，我们可以知道局域网内的通信是否正常。
#### 显示本地存储的IP-MAC对应关系

```
arp -a
```
#### 经eth0接口，发送ARP请求，查询IP为192.168.1.1设备的MAC地址

```
sudo arping -I eth0 192.168.1.1  //arping需要自行安装
```
#### 查询整个局域网内的所有IP地址的对应MAC地址

```
sudo arp-scan -l //arp-scan需要自行安装
```
#### 监听en0接口的arp协议通信

```
sudo tcpdump -i en0 arp
```

### tcpdump 网络监听
tcpdump是一款网络抓包工具。它可以监听网络接口不同层的通信，并过滤出特定的内容，比如特定协议、特定端口等等。我们上面已经使用tcpdump监听了ARP协议通信。这里我们来看更多的监听方式。

#### 监听en0接口的所有通信

```
sudo tcpdump -i en0
```
#### 用ASCII显示en0接口的通信内容

```
sudo tcpdump -A -i en0 
```
#### 显示en0接口的8080端口的通信

```
sudo tcpdump -i en0 'port 8080'
```
#### 显示eth1接口，来自192.168.1.200的通信

```
sudo tcpdump -i eth1 src 192.168.1.200
```
#### 显示eth1接口80端口，目的地为192.168.1.101的通信

```
sudo tcpdump -i eth1 dst 192.168.1.101 and port 80
```
#### 将lo0接口的通信存入文件record.pcap

```
sudo tcpdump -w record.pcap -i lo0
```
### ping
网络层是一个广域的互联网，互联网上的设备用IP地址识别。ping是向某个IP地址发送ICMP协议的ECHO_REQUEST请求。收到该请求的设备，将返回ICMP回复。如果ping到某个IP地址，那么说明该IP地址的设备可以经网络层顺利到达。
#### 向IP地址192.168.1.255发送ICMP请求。如果该地址的ICMP没有被禁用，那么在该网上的设备将回复  

```
ping 192.168.1.1
```

### 路由
局域网通过路由器，接入广域的互联网。互联网上的通信往往要经过多个路由器接力。途中路由器的故障，可能导致互联网访问异常。
#### 显示路由表

```
netstat -nr
```
#### 追踪到达IP目的地的全程路由

```
traceroute 74.125.128.99
```
#### 通过ICMP协议，追踪路由。ICMP协议经常会被禁用，所以会返回"*"的字符串

```
traceroute -I 74.125.128.99
```
####   通过TCP协议，经80端口，追踪路由。TCP协议的默认端口80很少会被禁用。

```
sudo traceroute -T -p 80 74.125.128.99
```

### 域名
DNS是在域名和IP之间进行翻译。DNS故障会导致我们无法通过域名访问某个网址。 
#### 域名解析

```
host www.baidu.com
```
#### 域名whois

```
whois www.baidu.com
```

### curl
#### 下载单个文件，默认将输出打印到标准输出中(STDOUT)中，其实就是终端

```
curl http://www.skyfox.org
```
#### 通过-o/-O选项保存下载的文件到指定的文件中
-o：将文件保存为命令行中指定的文件名的文件中

-O：使用URL中默认的文件名保存文件到本地

```
curl -o mynews.html http://dev.skyfox.org/news.html

curl -O http://dev.skyfox.org/news.html
```
### 断点续传
通过使用-C选项可对大文件使用断点续传功能

```
curl -C - -O http://dev.skyfox.org/news.html
```
### 从FTP服务器下载文件
CURL同样支持FTP下载，若在url中指定的是某个文件路径而非具体的某个要下载的文件名，CURL则会列出该目录下的所有文件名而并非下载该目录下的所有文件

```
# 列出public_html下的所有文件夹和文件
curl -u ftpuser:ftppass -O ftp://ftp_server/public_html/

# 下载xss.php文件
curl -u ftpuser:ftppass -O ftp://ftp_server/public_html/xss.php

```

### 上传文件到FTP服务器
通过 -T 选项可将指定的本地文件上传到FTP服务器上

```
# 将myfile.txt文件上传到服务器
curl -u ftpuser:ftppass -T myfile.txt ftp://ftp.testserver.com

# 同时上传多个文件
curl -u ftpuser:ftppass -T "{file1,file2}" ftp://ftp.testserver.com

# 从标准输入获取内容保存到服务器指定的文件中
curl -u ftpuser:ftppass -T - ftp://ftp.testserver.com/myfile_1.txt
```
### 为CURL设置代理
-x 选项可以为CURL添加代理功能
```
# 指定代理主机和端口
curl -x proxysever.test.com:3128 http://google.co.in
```
### 保存与使用网站Cookie信息

```
# 将网站的cookies信息保存到sugarcookies文件中
curl -D sugarcookies http://localhost/sugarcrm/index.php

# 使用上次保存的cookie信息
curl -b sugarcookies http://localhost/sugarcrm/index.php

```
### 传递请求数据
默认curl使用GET方式请求数据，这种方式下直接通过URL传递数据
可以通过 --data/-d 方式指定使用POST方式传递数据

```
# GET
curl -u username https://api.github.com/user?access_token=XXXXXXXXXX
 
# POST
curl -u username --data "param1=value1&param2=value" https://api.github.com

# 也可以指定一个文件，将该文件中的内容当作数据传递给服务器端
curl --data @filename https://github.api.com/authorizations

# CURL 发送磁盘上面的JSON文件
curl -X POST  -H 'content-type: application/json'  -d @myjsonfile.txt http://some.url/param  

# CURL在命令行直接发送JSON结构数据
curl -H "Content-Type: application/json" -d '{"user":{"uid":123,"username":"woshishui"},"baseinfo":"afsdaa"}'  http://api.skyfox.org/project/afndemo/getTypes.do
```
### spctl
spctl manages the security assessment policy subsystem.
### 验证APPl来自哪个渠道

```
spctl --assess --verbose /Applications/Xcode.app
```
### 找回允许任何来源的APP选项
系统有一个保护叫做 Gatekeeper , 这个是防止第三方应用访问你的隐私信息的. 如果你想关掉或者开启在终端里输入
```
#关掉
sudo spctl --master-disable
#开启
sudo spctl --master-enable
```


