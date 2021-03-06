---
title: 免密登录远程服务器配置
date: 2019-06-18
tags: Linux
category: 应知必会Linux
description: 从现在开始你就不用再每次输入密码登录远程服务器啦 🛠
---

去年双11，阿里云搞活动，「拼团购买云服务器」，收到同事的拼团邀请后开始丧心病狂的邀请其他同事朋友，最终以低廉的价格买了三年的阿里云服务器，嘻嘻~。

虽然对服务器知识了解的不多，但是也在一直星星点点的在积累这方面的知识。我相信还有更多跟我一样的前端农民工，客户端界面开发久了对黑乎乎的终端里密密麻麻的「天书」也充满了好奇。

天也不早了，开始说正题。

一般我们登录到服务器都是用`ssh`去登录，关于`ssh`的使用可以自行百度，网上有很多，就不再赘述
``` bash
ssh root@12.123.45.6
```

然后敲回车终端窗口就会出现以下提示

```bash
root@12.123.45.6's password: 🔑
```

提示我们输入远程服务器密码，输入完之后就进入到了远程服务器啦！

其实看起来也没有那么麻烦，但是由于懒惰是程序猿灵感的来源之一。况且为了以后更好的去[持续集成](<https://baike.baidu.com/item/%E6%8C%81%E7%BB%AD%E9%9B%86%E6%88%90/6250744>)，手动输入密码这些操作当然是能省则省了。

### 免密登录的原理

使用`非对称加密`，密码学这部分不多说，由于我自己研究的也不是很深，所以暂时不误导大家。就先简单举个形象的例子一笔带过：

​	服务器上有把锁(公钥)，A口袋里有把钥匙(私钥)，B口袋里也有把钥匙(私钥)，一个锁可以配置多把钥匙，但是钥匙都是一样的，都放在自己的口袋里小心保管着，锁是公开的。有钥匙才能开锁，而且得是对应的钥匙。

### 下面我们来配置**免密登录**

1. 登录远程服务器

   ```bash
   ssh root@12.123.45.6
   root@12.123.45.6's password: 🔑 #输入密码
   ```

   

2. 进入远程服务器，生成秘钥对

   ```bash
   ssh-keygen -t rsa -C "coolb" -f "coolb_rsa"
   ```

   这里我们解释一下这几个参数的含义

   - -t：指定加密方式，一般我们使用`rsa`的加密方式，当然也可以使用其他加密方式，可以自行折腾。
   - -C：指定密钥的名称，这里的参数值`coolb`，将会参与最终秘钥对的加密，即会在最终的加密字符串里有体现。
   - -f：指定秘钥对文件名

   最终会在你当前目录下生成两个文件`coolb_rsa` 和 `coolb_rsa.pub`，前者是秘钥文件，后者是公钥。

3. 上传配置公钥

   1. 将生成的公钥到服务器对应的home路径下的`.ssh/`中，输入一下命令，这里的`home`就是服务器登录用户的根目录，例如我用`root`用户登录的，我的根目录就是`~`。

      ```bash
      ssh-copy-id -i "coolb_rsa.pub" root@12.123.45.6
      ```

      这里的坑注意⚠️，公钥名一定是个字符串要用*引号*框起来。

      回车，提示输入密码，第一次上传公钥会有些提示。

   2. **配置公钥文件的访问权限为600**

      ```bash
      chmod 600 coolb_rsa.pub
      ```

4. 配置本地私钥

   上面几步都是在远程服务器上操作的，这步操作是在本地机器上操作。

   1. 把第二步生成的**私钥**复制到你的home目录下的`.ssh/ `路径下，你可以通过`vi`打开`coolb_rsa`私钥文件，复制里面的内容，粘贴到你本机的`.ssh/`下一个新建的文件里，比如我这里新建一个文件还叫`coolb_rsa`，打开这个文件，将刚才复制的私钥的内容粘贴到这个文件里。

   2. **配置你的私钥文件访问权限为 600**

      ``` bash
      chmod 600 coolb_rsa
      ```

5. 免密登陆功能的本地配置文件

   1. 编辑本地home目录下的`.ssh/`路径下的`config`文件，如果没有，新建一个即可，编辑config文件

      ```sh
      Host coolb
      User root
      HostName 12.123.45.6
      IdentityFile ~/.ssh/coolb_rsa
      # --------------- 以下几行照抄就行，上面几个需要配置对应的参数
      Protocol 2
      Compression yes
      ServerAliveInterval 60  #配置发送心跳包的频率
      ServerAliveCountMax 20  #每次心跳包发送个数
      LogLevel INFO #日志等级
      ```

      这里我们只是针对单主机进行的免密登录的配置，当然也可以对多主机进行配置，这里暂时先不介绍。

   2. **配置config文件访问权限为644**

      ``` bash
      chmod 644 config
      ```




都配置完了？恭喜你你已经可以进行免密登录啦，根据本文的步骤做的配置，可以在终端中输入

```bash
ssh coolb
```

敲回车，biu~，就直接跳过密码验证直接访问到远程服务器了！是不是很方便呢？

### 总结

当然，凡是涉及到登录远程服务器验证密码的地方，这个免密配置都生效，例如向远程服务器传文件

``` bash
scp xxx.md coolb:~/
```

也不需要验证密码了，就可以将本地的`xxx.md`文件传到远端的`~`路径下了。



🏁另外，几个需要特别注意的地方我都特别标出来了：

1. 公钥名称的引号不能少
2. 文件的访问权限不能忘记配置



> 以上内容都经过博主验证，若有不对的地方，欢迎指出，一起学习，感谢阅读！