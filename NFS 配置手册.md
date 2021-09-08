# NFS 配置手册

yum install nfs-utils rpcbind -y #安装必要软件

* 服务端：

    + df -h #查看磁盘信息

    + mkdir zwzc #首先进入系统中最大的磁盘路径中，创建zwzc文件夹存放共享目录

    + chown -R nfsnobody.nfsnobody zwzc/ #修改文件夹权限

    + ll -d zwzc/ #验证是否生效

    + vi /etc/exports #配置权限 /home/zwzc *(rw,sync) *号修改成对应网段 如：192.168.3.0/24
    
    + systemctl start rpcbind.service #启动对应服务

    + systemctl start nfs.service #启动对应服务

* 客户端：
    + systemctl start rpcbind.service #启动对应服务

    + showmount -e 192.168.3.5 #替换成对应IP 测试是否正常连接

    + mount -t nfs 192.168.3.5:/home/zwzc /mnt/zwzc #替换成对应IP进行挂载

    + vi /etc/rc.local #修改开机自启 把上面这行命令复制进最后一行

    + df -h #查看是否挂载成功
