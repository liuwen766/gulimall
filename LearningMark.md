# 项目启动顺序

step1：启动项目依赖的sql数据库服务器。【若未进行数据库的初始化，则进行sql文档的初始化】。

step2：启动nacos服务【我用的的是本地源码安装的nacos】，在nacos上按需配置后端服务的各种配置

step3：启动所有的后端服务。【所有的服务会自动注册在nacos中，并在nacos上发现所有注册在nacos上的服务，这就是[服务注册]与[服务发现]】

step4：启动前端服务。前端服务基于VUE框架。【前后端的通信统一会经过网关gateway服务，网关会重写路径，将请求路由到指定的后端服务】

step5：登录页面。登录账号admin/admin。

## sql文档

项目原始sql在./tools/sql初始化/；补充的sql在./tools/sql初始化/sql2更改表；

## naco源码 服务本地安装步骤

step1:

从github上，下载nacos最新的源码到本地:

git clone https://github.com/alibaba/nacos.git

step2:

本地编译(建议用阿里云的maven仓库):

mvn -Prelease-nacos -Dmaven.test.skip=true clean install -U

step3:

源码运行时，通常使用的是单机模式，因此需要在启动参数中进行设置，在jvm的启动参数中，添加

-Dnacos.standalone=true

step4:

编译完成的nacos源码导入到idea开发工具中；进入到nacos-console模块下，启动该模块下的com.alibaba.nacos.Nacos类

启动成功，请享用。

http://localhost:8848/nacos/index.html

登录名/密码 nacos/nacos


## 跨域

不同源的请求会引发跨域问题。

跨域问题可以简单理解为页面请求的url字符串对比。

——2021.2.27

解决跨域问题的办法：

方法一：使用nginx服务器，将前后端项目都部署在nginx服务器上，这样页面请求就会一致，不会引发跨域问题。

方法二：通过配置，允许可以跨域的请求。（全局配置或者注解配置）