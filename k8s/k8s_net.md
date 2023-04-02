

# k8s 网络模型
基本原则：
每个pod有独一无二的IP

# 解决的问题
1. pod内容器间通信  lo
2. pod间通信
3. pod和节点间通信
4. pod对外暴露服务

# 网络规范
CNI
https://github.com/containernetworking/cni

# 解决方案


## 隧道 overlay

## 路由

# flannel
https://github.com/flannel-io/flannel#deploying-flannel-manually

# 参考链接

https://kubernetes.io/zh-cn/docs/concepts/services-networking/
https://kubernetes.io/zh-cn/docs/concepts/cluster-administration/networking/
