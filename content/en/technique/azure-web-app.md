---
title: "Build static blogs with Azure Static Web Apps"
date: 2022-12-20T19:27:37+10:00
draft: false
weight: 4
featured_image: "/images/original-url-page.png"
---

> Prerequisite: You need to use GitHub to deploy web pages, you need to write HTML, CSS, JavaScript code yourself, this method is not suitable for zero-code basic whites to build their own blogs
> Advantages of this method: directly linked to the GitHub repository, when the changes in the repository are completed, the pull request can automatically update the website content; Support for HTTPS; Have complete control over the web design of your blog.

 <!--more-->

### The first step is to upload your own blog content code

1. Upload your own code in GitHub, take this article as an example, upload to the master branch of the live-blog2 repository, and create another branch named "demo", the reason for creating another branch will be explained in the fourth step.

### The second step is to deploy the website with Azure Static Web Apps

1. Landing page: https://portal.azure.com -> After logging in with your own Microsoft account light, choose the subscription method: free trail (physical credit card verification is required) or self-pay (physical credit card or debit card is required); Or sign in with Azure for Students by https://azure.microsoft.com/en-us/free/students/->, and both Azure for Students and free trail get $200 in free credits for Azure products and services, as well as 12 months of popular free services
   (GitHub provides students with free resource libraries for current students that contain the Azure for Students student pack, how to get it)
2. Create Resource - > Static Web Apps
3. Fill out the form

   - ![选择自己的订阅方式](https://i.postimg.cc/mgt4QHSp/azure-static-web-app1.png "subscribe01")
   - subsription: Choose how you want to subscribe
     Free trail or Purchase Options or Azure for Students
   - resouce group：You can create a resource group that you created earlier, or you can create a new resource group
   - name：Give your app a name
   - hosting plan：a) free, b) standard
     For just building a blog, the free plan is sufficient
     The difference between the two is that standard can add user authentication (custom authentication) to its web pages, as well as private endpoints (which can use private IPs to access local resources such as databases, etc., instead of accessing resources over the Internet through public IPs)
     ![选择自己的订阅方式](https://i.postimg.cc/hjbRSbSv/azure-static-web-app2.png "subscribe02")
   - function api：Select the name of the region where the server is located, and prefer a location close to you
   - deployment detail：This article uses GitHub as the deployment method, and chooses your own GitHub account, repository, and branch
   - ![选择自己的订阅方式](https://i.postimg.cc/50fkmcV9/azure-static-web-app3.png "subscribe03")

   - build details：
     build presets：Choose your own website building framework, this article takes the html, CSS, JavaScript written by yourself as an example, and selects "Custom"
     app location，The built code is in the location of the code warehouse, if it is in the root directory, the space is filled with "/"
     API location and output location are not filled in by default
   - review+create：Click review + Create

4. After the creation is completed, there will be the following interface, click browse, you can preview the built website
   - ![界面](https://i.postimg.cc/qR7xRprK/azure-static-web-app4.png "subscribe04")

### Step 3: Modify the domain name

> The URL column will display the auto-generated URL, for example, the initial URL in this article is "https://happy-bush-0d4cdbc00.2.azurestaticapps.net", but this article adds "custom domain" to bind your own domain name, the specific operation is as follows

1. Buy a domain of your own, this article is eligible for a free domain through namecheap.com in the GitHub Student Pack (how do I get it?) ）
2. namecheap After logging in to your account, find your domain name in the "Domain List" menu bar, select "manage", click "Advanced DNS", and add a new "CNAME record"
   ![namecheap](https://i.postimg.cc/przhXCBm/namecheap1.png "namecheap1")
   ![namecheap](https://i.postimg.cc/yd9YFd35/namecheap.png "namecheap2")
   ![namecheap](https://i.postimg.cc/fRrwpXxp/namecheap2.png "namecheap3")

   - host is the host domain name, which can be "www", or other words named by yourself, such as "blog2" in this article
   - value is the result "green-bay-076566700.2.azurestaticapps.net" after removing the "https://" from the initial URL, TTL can be understood as setting the maximum load time of the web page, this article sets 1min.

3. Click "custom domain" in the figure below, click the add button "add", there are two options: "Azure DNS" and "other DNS", this article uses the DNS provided by namecheap, so click the second one.
   ![namecheap](https://i.postimg.cc/FzWqzbsQ/domain-DNS.png "domain")

4. Fill in the pop-up form with "domain name", because the host domain name added in namecheap is "blog2", and the purchased subdomain is "liuliuwu.me", so the blank can be filled in as "blog2.liuliuwu.me", click add in the next step, wait for authentication (the authentication process needs to turn off services such as network proxy VPN, there may be a delay, if the verification fails, You can wait an extra ten minutes and repeat Step 4 to reverify)
   ![namecheap](https://i.postimg.cc/MTh5FsTH/domain1.png "domain")
   ![namecheap](https://i.postimg.cc/PrKZL3jD/domain-DNS2.png "domain")

5. After the certificate is successful, two records are displayed on the Custom Domain page
   ![namecheap](https://i.postimg.cc/PrKZL3jD/domain-DNS2.png "domain")

6. Enter https://blog2.liuliuwu.me on the web page to verify that the domain name is bound

### Step 4: Update the web content

> Since when using static web apps for website deployment, it will automatically create a new .github/workfolw/xxxx.yml file in the github repository of live-blog2, and the local live-blog2 folder does not contain this file, if you directly use git push for the modified file in the terminal, .github/ in the github code repository of live-blog2 The workfolw/xxxx.yml file, which is a working bridge between GitHub and Azure, disappears, and automatically updates website content will not be possible.

1. solution: Type "git pull" on the command line to synchronize the remote repository to the local sync

   ```
   git pull
   ```

2. Modify the content of the page
   ![html](https://i.postimg.cc/4y7rmJB3/change-master.png)

3. "git push" uploads the file after the commit to the master branch

   ```
   git add index.html
   git commit -m 'update index'
   git push -f blog2 master
   ```

4. See the auto-update process through GitHub Action
   ![namecheap](https://i.postimg.cc/htTQVTfL/master-github-action.png "domain")

5. Verify the web page（reload the page）
   ![网页](https://i.postimg.cc/0y0mL7P8/test-master.png "blog page")
