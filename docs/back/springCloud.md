**Eureka--注册中心**
================
![](../_v_images/_1582725557_29830.png)
启动类上添加
![](../_v_images/_1582725561_8275.png)
****注册中心服务器配置文件****
-------------------
![](../_v_images/_1582725572_24220.png)
****服务配置文件****
--------------
![](../_v_images/_1582725577_24550.png)
****Ribbon****
==============

****调用远程方法方式****
----------------
![](../_v_images/_1582725606_10236.png)![](../_v_images/_1582725610_21847.png)
![](../_v_images/_1582725615_6896.png)
****自定义负载均衡策略****
-----------------

Product-service是你要调用的服务的application-name
![](../_v_images/_1582725619_31767.png)
****Feign****
=============

****使用步骤****
------------
![](../_v_images/_1582725625_12795.png)
![](../_v_images/_1582725632_30387.png)mapping一定要和sprduct-service里的一样，参数也是
![](../_v_images/_1582725636_24084.png)
****Hystrix****
===============

****引入****
----------
![](../_v_images/_1582725642_3399.png)
****添加注解（2个都可以）****
-------------------
![](../_v_images/_1582725646_32220.png)
****使用（参数名称一定要一致）--->降级****
---------------------------
![](../_v_images/_1582725652_26369.png)
****与feign整合--->熔断****
----------------------

### ****添加配置****
![](../_v_images/_1582725658_6806.png)
### ****声明熔断方法****
![](../_v_images/_1582725663_5051.png)
熔断方法继承feign接口，一旦调用findbyid失败就会熔断，然后抛出异常，之后降级处理
![](../_v_images/_1582725670_2509.png)
****Feigin设置的超时时间不生效的原因--hystrix的超时时间没有设置****
---------------------------------------------

![](../_v_images/_1582725678_27527.png)不能起到作用

### ****解决方法--对hystrix也设置超时时间****
![](../_v_images/_1582725685_307.png)
****Zuul网关---暴露在公网中，其他服在内网，相当于nginx****
=======================================

****依赖****
----------
![](../_v_images/_1582725690_15249.png)
****配置文件****
------------

### **1. ******向eureka注册网关****
![](../_v_images/_1582725697_22148.png)
### **2. ******在启动类上添加注解 enablezuulproxy****
![](../_v_images/_1582725702_13045.png)
### **3. ******通过网关访问规则****

例如有一个order-service的服务--端口是8781
![](../_v_images/_1582725709_13168.png)
现在通过zuul访问--zuul端口是9000  order-service就是服务在eureka注册的名字
![](../_v_images/_1582725714_22409.png)
****自定义访问规则和拒绝访问****
--------------------

自定义规则路径不能完全一样不能都是/apigateway/**，会覆盖

如果觉得/order-service写起来麻烦
![](../_v_images/_1582725723_1492.png)
访问就变成了192.168.0.107:9000/apigateway/api/v1/xxxxxxxxxxx

### ****拒绝访问****

Ignored-services：指定在eureka的服务名字

Ignored-patterns：正则表达式指定

****Cookie过滤****
----------------

默认过滤以下内容
![](../_v_images/_1582725733_18851.png)
解决方法
![](../_v_images/_1582725739_30416.png)
****自定义过滤器--extends ZuulFilter，实现4个方法****
-----------------------------------------

### ****FilterType****
![](../_v_images/_1582725744_5990.png)
### ****FilterOrder****
![](../_v_images/_1582725749_18302.png)
### ****ShouldFilter****
![](../_v_images/_1582725754_8987.png)
### ****Run****
![](../_v_images/_1582725762_10314.png)
****限流处理--也是基于zuulfilter实现****
------------------------------

采用guava---就是生产100个令牌，每个线程进来都会拿一个，如果拿不到就不让他运行，从而限流

****集群部署****
------------

直接启动多个相同的节点就行了，只要名字一样就行

****Sleuth----打印日志****
======================
![](../_v_images/_1582725773_32152.png)
****Zipkin****
==============
![](../_v_images/_1582725779_2121.png)
添加地址
![](../_v_images/_1582725783_23767.png)
****Config-Server****
=====================

****引入&添加注解****
---------------
![](../_v_images/_1582725789_1018.png)
![](../_v_images/_1582725794_22553.png)
****配置****
----------

基础配置
![](../_v_images/_1582725798_5973.png)
添加git配置
![](../_v_images/_1582725804_7756.png)
****访问****
----------

如果要访问配置服务提交的application.yml
![](../_v_images/_1582725816_5399.png)
### ****访问的多种形式****
![](../_v_images/_1582725823_16533.png)
![](../_v_images/_1582725828_13740.png)返回master（默认），以json格式

![](../_v_images/_1582725833_14887.png)以properties格式

****使用****
----------

### ****引入依赖****
![](../_v_images/_1582725839_25125.png)
****配置--配置到bootstrap.yml****
----------------------------
![](../_v_images/_1582725844_26573.png)
这样就会去读取  服务器的名称-profile   product-service-test