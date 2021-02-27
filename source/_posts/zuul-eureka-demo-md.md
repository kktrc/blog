---
title: zuul整合eureka实现路由转发
date: 2021-02-26 22:33:49
tags:
---

这篇文章将会教会你搭建一个zuul网关，并整合eureka，实现路由转发。也就是说当我们
调用网关的接口，网关会通过注册中心，找到相应的服务，转发给相应的服务。

比如网关的端口是http://localhost:8080

当我们调用http://localhost:8080/order-service/hello
网关会帮我们转发到order-service服务的 /hello接口上去，这篇文章就是记录下搭建的过程，最后分析下源码。


