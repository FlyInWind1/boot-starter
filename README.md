### 本脚本利用了 nginx 的负载均衡功能。upstream 里配置里两个 server 但是同一时间只有一个 server 是工作的
### 更新应用时启动之前不使用的那个 server ，然后关闭之前使用的。以达到用户无感觉便升级后台系统的效果

## 配置脚本
1. 将 boot-starter,boot-starter.conf 拷贝到项目的目录下。也就是和jar包同级目录
2. 修改 boot-starter.conf 配置文件，主要修改启动命令
3. chmod +x boot-starter 给主脚本执行权限

## 配置nginx
1. 将 backend.conf 拷贝到 nginx 配置目录的 conf.d 目录下
2. 确保 nginx.conf 中的 http 节中(与server同级)有 include conf.d/*.conf;

- 以上我提供的配置方案只是参考，实际使用中可随意配置

## 命令使用方法
boot-starter [deploy|restart|stop|status]

参数     | 说明 
--- | :---
deploy  | 部署项目，使用两个端口交替
restart | 重启项目，重启现已监听端口的项目。没有监听的话，启动第一个
stop    | 关闭所有项目
status  | 查看项目状态