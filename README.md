# Vagrant + VirtualBox + docker搭建php开发环境

> 基于vagrant + VirtualBox + docker搭建的php开发环境

## 集成的环境

- ngnix
- php7.2
- mysql 8.0.17
- redis
- phpmyadmin
- phpredisadmin

## 使用方法

- 1、clone项目到本地
```bash
git clone https://github.com/CavinHuang/phpdevelopenv.git
```

- 2、下载virtualBox和vagrant，这里推荐virtualbox5.24+vagrant2.0.1，更高版本目前我这边试出无法完美启动虚拟机

- 3、初始化虚拟机
```bash
vagrant up
```
这个过程会视你的网络情况，可能会需要大量的时间，主要是下载虚拟机的box和进入虚拟安装docker和需要的环境

- 4、初始化完成后进入虚拟机
```bash
vagrant ssh

cd projects

```

- 5、启动所有的服务
```bash
docker-compose up
```
此过程会pull docker image，所以网络不好花的时间会很长

- 6、启动部分的服务
比如只需要ngnix
```bash
docker-compose up ngnix
```
只需要ngnix+mysql+php
```bash
docker-compose up php nginx php
```

- 7、此时你访问`localhost:8040`应该是可以看到tp项目的首页了

## Q & A
1、无法远程连接mysql
 - 1> docker ps 查看mysql的容器id
 - 2> docker -i -t 容器ID bash
 - 3> mysql -uroot -p #进入mysql
 - 4> ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY '123456'; # 赋予root账户远程权限

2、更改配置去哪里改？
    所有的配置都在`config`目录下
   
3、新建项目怎么操作
  - 1> 在`apps`目录下新建项目        
  - 2> 在`config/ngnix/conf.d/`下建立相应的conf文件
  - 3> 加入需要暴露新的端口到本地，请在vagrantfile中添加
    
## 资料   

- [Docker — 从入门到实践](https://yeasy.gitbooks.io/docker_practice/content/)