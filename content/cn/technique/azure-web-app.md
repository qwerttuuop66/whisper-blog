---
title: "使用azure static web apps 搭建静态博客"
date: 2022-12-20T19:27:37+10:00
draft: false
weight: 4
featured_image: "/images/original-url-page.png"
---

![网页](https://i.postimg.cc/0y0mL7P8/test-master.png "blog page")

 <!--more-->

> 前提：需要使用 github 部署网页，需要自己写 html，css，JavaScript 代码，此方法并不适合零代码基础的小白来搭建自己的博客
> 此方法的优势：直接与 GitHub 代码仓连结，当代码仓内修改完成后 pull request 可实现自动更新网站内容；支持 https；对博客的网页设计有全方位的掌控。

### 第一步，上传自己的博客内容代码

1. 在 github 中上传自己的代码，以本文为例，上传至 live-blog2 代码仓的 master branch，同时 create 另一个名为“demo”的 branch，之所以要 create 另一个 branch 的原因会在第四步骤做解释。

### 第二步，利用 azure static web apps 部署网站

1. 登陆页面：https://portal.azure.com -> 使用自己的微软账号灯登陆后，选择订阅方式：free trail （需要有实体信用卡验证身份）或是自费（需要有实体信用卡或是借记卡）；或者通过https://azure.microsoft.com/en-us/free/students/ ->选择 Azure for Students 登陆， Azure for Students 和 free trail 两者都可以可获得 200 美元的 Azure 产品和服务免费额度，以及 12 个月的热门免费服务
   （github 提供给在校学生免费的资源库中包含了 Azure for Students 的学生包，如何获取）
2. 新建资源 (create resource)-> 静态 Web 应用（static web apps）
3. 填写表单

   - ![选择自己的订阅方式](https://i.postimg.cc/mgt4QHSp/azure-static-web-app1.png "subscribe01")
   - subsription: 选择自己的订阅方式
     free trail 或是 Purchase Options（自费） 或是 Azure for Students
   - resouce group：可以是之前建立的资源组，可以新建一个资源组
   - name：给自己的 app 取一个名字
   - hosting plan：a) free, b) standard
     对于只是搭建博客来说，free 计划足够用
     两者的区别是，standard 可以在自己的网页中添加用户的身份验证功能（Custom authentication），以及私有终结点（private endpoint，可以使用私有 IP 访问本地资源例如数据库等，而非通过公网 ip 用 internet 访问资源）

     ![选择自己的订阅方式](https://i.postimg.cc/hjbRSbSv/azure-static-web-app2.png "subscribe02")

   - function api：选择服务器所在地区名称，优先选择离自己近的地方
   - deployment detail：本文以 github 作为部署方式，选择自己的 GitHub 账号，代码仓（repository），以及分支（branch）
   - ![选择自己的订阅方式](https://i.postimg.cc/50fkmcV9/azure-static-web-app3.png "subscribe03")

   - build details：

     build presets：选择自己网站的搭建框架，本文以自己写的 html，css，JavaScript 为例，选择“Custom”

     app location，搭建的代码在代码仓的所在位置，如果在根目录下，该空格填写“/”

     api location 和 output location 默认不填写

   - review+create：点击创建即可

4. 创建完成之后会有如下所示界面，点击 browse，可预览搭建好的网站

   - ![界面](https://i.postimg.cc/qR7xRprK/azure-static-web-app4.png "subscribe04")

### 第三步，修改域名

> URL 一栏会显示自动生成的网址，例如本文中的初始网址为“https://happy-bush-0d4cdbc00.2.azurestaticapps.net”，但本文添加了“custom domain”绑定了自己的域名，具体操作如下

1. 购买一个自己的域名，本文通过 GitHub 学生包中 namecheap.com 提供的免费域名资格（如何获取？）
2. namecheap 登陆账号后，在"Domain List"菜单栏找到自己的域名选择“manage”，点击“Advanced DNS”，增加一个新的“CNAME record”

   ![namecheap](https://i.postimg.cc/przhXCBm/namecheap1.png "namecheap1")

   ![namecheap](https://i.postimg.cc/yd9YFd35/namecheap.png "namecheap2")

   ![namecheap](https://i.postimg.cc/fRrwpXxp/namecheap2.png "namecheap3")

   - host 为主机域名，可以是“www”，或是自己命名的其他单词如本文中的“blog2”
   - value 为初始网址除去“https://”后的结果“green-bay-076566700.2.azurestaticapps.net”，TTL 可以理解为设定网页的最长加载时间，本文设定的是 1min。

3. 点击下图中“custom domain”，点击添加按钮“add”，有两个选项：“Azure DNS”和“other DNS”，本文中使用的是 namecheap 提供的 DNS，因此点击第二个。

   ![namecheap](https://i.postimg.cc/FzWqzbsQ/domain-DNS.png "domain")

4. 在弹出的表单中填写“domain name”，由于在 namecheap 中添加的主机域名为“blog2”，购买的 subdomain 为“liuliuwu.me”，因此在该空可填写为“blog2.liuliuwu.me”，下一步点击 add，等待认证（该认证过程需要关闭网络代理 VPN 等服务，可能有延迟，如果显示验证失败，可以多等十几分钟后重复 第 4 步骤重新验证）

   ![namecheap](https://i.postimg.cc/MTh5FsTH/domain1.png "domain")

   ![namecheap](https://i.postimg.cc/PrKZL3jD/domain-DNS2.png "domain")

5. 证成功后，在“custom domain”页面显示了两条记录

   ![namecheap](https://i.postimg.cc/PrKZL3jD/domain-DNS2.png "domain")

6. 在网页中输入“https://blog2.liuliuwu.me”，验证绑定域名成功

### 第四步，更新网页内容

> 由于使用 static web apps 做网站部署时，会自动在 live-blog2 的 github 代码仓中，新建.github/workfolw/xxxx.yml 文件，而本地的 live-blog2 文件夹内，并不包含这个文件，如果直接对修改后的文件在终端使用 git push，live-blog2 的 github 代码仓中的.github/workfolw/xxxx.yml 文件将会消失，而该文件是将 github 与 azure 的工作桥梁，消失后则无法实现自动更新网站内容。

1. 解决办法：命令行中键入“git pull” ，将 remote 仓库同步更新到本地

   ```
   git pull
   ```

2. 修改网页内容

   ![html](https://i.postimg.cc/4y7rmJB3/change-master.png)

3. “git push”将 commit 之后的文件上传至 master 分支中

   ```
   git add index.html
   git commit -m 'update index'
   git push -f blog2 master
   ```

4. 通过 github action 看到自动更新进程

   ![namecheap](https://i.postimg.cc/htTQVTfL/master-github-action.png "domain")

5. 验证网页

   ![网页](https://i.postimg.cc/0y0mL7P8/test-master.png "blog page")
