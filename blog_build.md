
# github 搭建博客

**简易原理**： 将博客当作repository，一篇博客就是一个markdown文件<br/>
0. 预置条件： 本地安装了ssh, git, 
1. 先要有一个github账户：https://github.com/  , 比如我的账户名为aprodigalson,
   创建一个repository 名字为<username>.github.io , aprodigalson.github.io
2. 在本地生成ssh 私钥 ssh-keygen -t rsa -b 4096 -C "你的邮箱", 
   将公钥拷贝, 添加到在github的settings的ssh key里, 用于在本地连接GitHub仓库
3. 在本地建个目录，和GitHub仓库中的repository对应, git clone或者git init ,git remote add 
4. 将写好的markdown文件push到远端仓库
5. 可以使用Jekyll进行博客配置。（todo）

`talk is cheap ,show me code`