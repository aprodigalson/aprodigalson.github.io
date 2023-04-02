# docker 

## 原理
Linux cgroup 和 namespace  

##


docker deamon 启动时，根据启动参数决定是否创建docker网桥。 
还依赖iptables 和 net.ipv4.ip_forward

## docker 网络模式
1. Host
和主机共用root 网络命名空间
2. None 
启动容器时，创建一个命名空间，只有一个lo口
3. Bridge
docker 默认的网络模式
docker 守护进程启动时，会默认创建一个docker0 网桥。启动容器时，创建一个网络命名空间， 然后在创建一个veth对，将一端插入容器的网络命名空间，一端插到docker0上 
也可以指定使用用户自定义的linux桥
4. Container
启动容器时，和另外一个容器使用相同的网络命名空间



给None的容器加个端口
ip link add c_x_eth0 type veth peer name c_y_eth
docker inspect --format '{{.State.Pid}}' container_x
ip link set netns $(docker-pid container_x) dev c_x_eth0
nsenter -t $(docker-pid container_x) -n ip link set c_x_eth0 up
或者可以参考实现：https://github.com/cslev/add_veth_to_docker/blob/master/add_veth2container.sh


## docker端口映射
外访内：
是通过iptables的nat规则实现的， 在PREROUTING和OUTPUT链上加上DOCKER链，并在DOCKER 链上设置DNAT规则
内访外

iptables -I FORWARD -o docker0 -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
？ 内访问时因为这个吗？ 我理解时SNAT反向吧




# 参考链接：
https://www.qikqiak.com/k8s-book/docs/7.Docker的网络模式.html
https://klose911.github.io/html/docker/kubernates/network.html#org737467f
https://github.com/cslev/add_veth_to_docker/
https://www.kancloud.cn/infoq/docker-source-code-analysis/80530
https://www.kancloud.cn/infoq/docker-source-code-analysis/80531
https://www.kancloud.cn/infoq/docker-source-code-analysis/80532