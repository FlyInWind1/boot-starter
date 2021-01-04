### 本脚本利用了 nginx 的负载均衡功能。upstream 里配置里两个 server 但是同一时间只有一个 server 是工作的

### 更新应用时启动之前不使用的那个 server ，然后关闭之前使用的。以达到用户无感觉便升级后台系统的效果


## 配置脚本

1. 将 boot-starter,boot-starter.conf 拷贝到项目的目录下。也就是和jar包同级目录
2. 修改 boot-starter.conf 配置文件，主要修改启动命令
3. chmod +x boot-starter 给脚本执行权限

## 配置nginx

1. 将 backend.conf 拷贝到 nginx 配置目录的 conf.d 目录下 (配置内容按自己的需要自行修改)
2. 确保 nginx.conf 中的 http 节中(与server同级)有 include conf.d/*.conf;

- 以上我提供的配置方案只是参考，实际使用中可随意配置

## 命令使用方法

boot-starter [deploy|deployBackend|deployFront|restart|stop|status]

参数     | 说明
--- | :---
deploy  | 部署项目，使用两个端口交替
deployBackend | 部署后端，使用两个端口交替
deployFront   | 部署前端
restart | 重启项目，重启现已监听端口的项目。没有监听的话，启动第一个
stop    | 关闭所有项目
status  | 查看项目状态

## TODO

- [x] 重启后端，更新前端文件
- [x] 备份老文件功能，将老的文件移动到 backup 下，然后将新的文件移动到工作区
- [ ] 一个压缩包中有前端和后端的文件，当这个压缩包放到 new 目录下后，运行 ./boot-starter deploy 可以自动将其中文件解压
- [ ] 使用python监听 new 目录下的文件变化，当发现有可部署的文件时自动执行部署功能
- [ ] 使用python自动执行sql增量脚本
- [ ] 当新的 boot-starter 和配置文件放到 new 下面时可以自动更新
- [ ] 写一个systemd开机自启service
- [ ] 部署完成后删除 backup 下有那些年头的文件
- [ ] 解决nginx负载均衡对于关闭的那个server一直报错的问题
- [ ] 提供一个配置，允许两个后端同时运行，这也是解决nginx报错的解决方案之一
