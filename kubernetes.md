# K8S组件



## pod

一般来说,一个pod只允许一个容器



* pod内部存在内部IP地址,自动分配的

> 可以使用`service`去管理一个组的pod
>
> 把相同的一个pod组变成一个service,只需要访问service,就可以实现访问pod
>
> **service会自动转发请求到健康的pod上**



## ingress

编写规则,可以使用域名设置,使得可以访问服务

控制来自外部的访问请求



## ConfigMap

封装配置信息



* 注意,是明文保存的



## secret

封装信息



* 做了base64编码,但不是加密,需要配合别的方式



## volumes

把容器内部的数据挂载到外部中,实现数据的持久化



## deployment

可以控制

1. 副本数量

> pod的个数,当有pod出错时候,可以自动创建新的pod



2. 滚动更新

> 定义和管理应用程序的更新策略
>
> 确保应用程序的平缓升级



* 数据库的副本是有状态的,一般不适用deployment控制,使用statefulset控制



## node

包含pod,service,ingress



提供`node:port`的服务,可以访问内部的`service:port`服务



* master node含有api server,控制来自外部的请求并且提供服务



# kubectl

用来控制K8S的命令行工具	

> 安装集群工具的时候,也会随便安装kubectl



# K3S

