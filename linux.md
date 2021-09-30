# Linux

## nginx

配置文件存放目录：`/etc/nginx`

主配置文件：`/etc/nginx/conf/nginx.conf`

管理脚本：`/usr/lib64/systemd/system/nginx.service`

模块：`/usr/lisb64/nginx/modules`

应用程序：`/usr/sbin/nginx`

程序默认存放位置：`/usr/share/nginx/html`

日志默认存放位置：`/var/log/nginx

#### 启动

```shell
#配置环境变量
nginx -c nginx配置文件地址
#通过包管理器安装nginx，比如yum，apt-get
service nginx start
```



#### 停止

```shell
ps -ef | grep nginx
#从容停止Nginx
kill -QUIT 主进程号

#快速停止Nginx
kill -TERM 主进程号

#强制停止Nginx
pkill -9 nginx
```



#### 重启

修改了nginx的配置文件，需要重启下nginx服务。

```shell
nginx -s reload
```



#### 查看日志

```shell
nginx -s reopen – 重新打开日志
```



## 文件和目录

#### 文件重命名

```shell
mv fileName newName
```

#### 删除文件

```shell
rm -f fileName
```

#### 创建目录

```shell
mkdir dir1 创建一个叫做 'dir1' 的目录' 
mkdir dir1 dir2 同时创建两个目录 
```

#### 删除目录

```shell
rmdir dir1 删除一个叫做 'dir1' 的目录' 
rm -rf dir1 删除一个叫做 'dir1' 的目录并同时删除其内容 
rm -rf dir1 dir2 同时删除两个目录及它们的内容 
```

## 关机 /重启/登出

#### 关机

```shell
shutdown -h now 关闭系统(1) 
init 0 关闭系统(2) 
telinit 0 关闭系统(3) 
shutdown -h hours:minutes & 按预定时间关闭系统 
shutdown -c 取消按预定时间关闭系统 
```

#### 重启

```shell
shutdown -r now 重启(1) 
reboot 重启(2) 
```

#### 登出

```shell
logout 注销 
```

