# 修改hosts来正常访问github

* github是一个活跃度高、氛围很好的开源社区，里面有很多优秀的个人及企业级项目，也支持用git去管理自己的项目，便于团队共同开发。但是由于GFW的存在，访问github偶尔会出现资源无法完整加载或者加载很慢的状况，这时候就需要在hosts文件中添加一些域名映射来改善github的访问。windows系统的hosts文件放在C:\Windows\System32\drivers\etc路径下，而linux系统的hosts文件放在\etc路径下，具体要在hosts文件添加的内容如下:

```bash
# GitHub Start 
192.30.253.112 github.com 
192.30.253.113 github.com 
192.30.253.119 gist.github.com 
151.101.185.194 github.global.ssl.fastly.net
151.101.100.133 assets-cdn.github.com 
151.101.100.133 raw.githubusercontent.com 
151.101.100.133 gist.githubusercontent.com 
151.101.100.133 cloud.githubusercontent.com 
151.101.100.133 camo.githubusercontent.com 
151.101.100.133 avatars0.githubusercontent.com 
151.101.100.133 avatars1.githubusercontent.com 
151.101.100.133 avatars2.githubusercontent.com 
151.101.100.133 avatars3.githubusercontent.com 
151.101.100.133 avatars4.githubusercontent.com 
151.101.100.133 avatars5.githubusercontent.com 
151.101.100.133 avatars6.githubusercontent.com 
151.101.100.133 avatars7.githubusercontent.com 
151.101.100.133 avatars8.githubusercontent.com 
# GitHub End
```





==END==