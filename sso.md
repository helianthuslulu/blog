**http://fm.qq.com如何检测到本地qq登陆的？**

这个问题分为两个部分

>* 如何检测到本地客户端qq登陆的?

>* 如何检测到webqq登陆的?


这个问题也就是***sso***技术Single Sign On

sso技术是在多个应用系统中用户只需一次登录就可以登陆多个信任的系统中。

webqq是共用一个sso的domain做session验证啦。。。都有一个qq.com域名含有相同的session所有的cookie都有一个范围，叫domain，如“.sun.com”。这个范围规定了只有在访问相同domain的时候，浏览器才会将此cookie带上

所以对于webqq检测比较简单。。






****
