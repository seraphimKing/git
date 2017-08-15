# git碰坑
之前将项目上传到git上都是图形化界面直接点击，很简单，不用脑子的跟着中文走就行。今天用命令上传文件却碰到了一大堆坑，花了两个多小时才上传完成，真的是满满的落寞感，于是在这里将遇到的问题简单记录一下，防止重蹈覆辙。<br/><br/>

首先出现的问题是在push文件的时候一直报错，后来想想应该是ssh公钥的问题。之前因为设置的比较乱，可能有地方设置错了，于是就把之前的ssh公钥全删了。<br/>
(1)然后将.ssh文件夹中的known_hosts给删除。<br/><br/>
(2)跟着生成ssh公钥的教程将ssh再生成出来，然后去.ssh文件中的id_rsa.pub中的公钥给复制下来，粘贴到相应位置。<br/><br/>
(3)运行ssh -T git@git.oschina.net，还是报错：Permanently added (RSA) to the list of known hosts问题解决，然后又去网上找了大量教程，http://www.2cto.com/os/201307/227199.html，根据它修改/etc/ssh/sshd-config文件，将其中的PubkeyAuthentication yes修改为no，再运行一下，就成功了。<br/><br/>
(4)push的时候又出错了 fatal: remote origin already exists。然后想到项目已经被我重新创建过了，所以生成的ssh变了。于是git remote rm origin将远程主机删除，又git remote add origin ..了一遍，然后push，果然成功了。<br/><br/>
(5)中间在修改的过程中还发现我把名字设置错了，又设了一遍 —.—这毛病<br/>
    git config --global user.name "IT女巫的饭后甜点"<br/>
    git config --global user.email "153853991@qq.com"<br/><br/>
(6)又看了一遍阮一峰大神的教程 http://www.cnblogs.com/haoshine/p/5884816.html 前端之路漫漫！