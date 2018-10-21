# 10yue21
### linux yuma rz 安装  
sudo&ensp;yum&ensp;install&ensp;lrzsz&ensp;-y  
### 实验：源码编译安装httpd-2.4.25.tar.bz2  
1&ensp;yum&ensp;groupinstall&ensp;"development&ensp;tools"&ensp;yum&ensp;install&ensp;&ensp;apr-devel&ensp;&ensp;apr-util-devel&ensp;&ensp;pcre-devel&ensp;openssl-devel  
2&ensp;useradd&ensp;-r&ensp;-u&ensp;80&ensp;-d&ensp;/data/www/&ensp;-s&ensp;/sbin/nologin&ensp;httpd  
3&ensp;tar&ensp;xf&ensp;httpd-2.4.25.tar.bz2  
cd&ensp;cd&ensp;httpd-2.4.25/  
4&ensp;cat&ensp;README  
cat&ensp;INSTALL  
5&ensp;./configure&ensp;--help  
./configure&ensp;--prefix=/app/httpd&ensp;--sysconfdir=/etc/httpd24&ensp;--enable-ssl&ensp;--disable-status  
6&ensp;make&ensp;&ensp;&&&ensp;make&ensp;install  
7&ensp;PATH变量  
echo&ensp;'PATH=/app/httpd/bin:$PATH'&ensp;>&ensp;/etc/profile.d/httpd.sh  
. /etc/profile.d/httpd.sh  
8&ensp;apachectl&ensp;start  

# 设备文件  
- I/O&ensp;Ports:I/O设备地址  
- 一切皆文件：open(),read(),write)(),close()
- 设备类型：  
&ensp;&ensp;&ensp;&ensp;块设备：block,存取单位“块”，磁盘  
&ensp;&ensp;&ensp;&ensp;字符设备：char，存取单位“字符”，键盘  
- 设备文件：关联至一个设备驱动程序，进而能够跟与之对应硬件设备机型通信  
- 设备号码：  
&ensp;&ensp;主设备号：major&ensp;numbei,标识设备类型  
&ensp;&ensp;次设备号：minor&ensp;number,标识同一类型下的不同设备  
## 创建ext文件系统  
- mke2fs:ext系列文件系统专用管理工具  
-t&ensp;{ext2|ext3|ext4}&ensp;&ensp;&ensp;&ensp;指定文件系统类型  
-b{1024|2048|4096|}&ensp;&ensp;&ensp;&ensp;&ensp;指定块大小  
-L&ensp;&ensp;‘LABEL'&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;设置卷标  
-j&ensp;&ensp;&ensp;&ensp;相当于&ensp;&ensp;&ensp;-t&ensp;&ensp;ext3  
&ensp;&ensp;&ensp;mkfs.ext3&ensp;=&ensp;mkfs&ensp;-t&ensp;ext3&ensp;=&ensp;mke2fs&ensp;-j&ensp;=&ensp;make2fs&ensp;-t&ensp;ext3  
-i&ensp;#&ensp;为数据空间中每多少个字节创建一个inode；不应该小于block大小  
-N #指定分区中创建多少个inode  
-l&ensp;&ensp;&ensp;一个inode记录占用的磁盘空间大小，128---4096  
-m&ensp;#&ensp;默认5%，为管理人员预留空间占总空间的百分比  
-O&ensp;FEATURE[,...]&ensp;&ensp;&ensp;QQ启用指定特性  
-O&ensp;^&ensp;FEATURE&ensp;&ensp;&ensp;关闭指定特性  
# parted命令  
- parted的操作都是实时生效的，小心使用  
- 用法：parted[选项]...[设备[命令[参数]...]...]  
parted/dev/sdb&ensp;mklabel&ensp;gpt&ensp;|&ensp;msdos  
parted&ensp;/dev/sdb&ensp;print  
parted&ensp;/dev/sdb&ensp;mkpart&ensp;primary&ensp;1&ensp;200&ensp;(默认M)  
parted&ensp;/dev/sdb&ensp;rm&ensp;1  
parted&ensp;-l&ensp;列出分区信息  
# 管理分区  
- 列出块设备  
lsblk  
- 创建分区使用：  
&ensp;&ensp;fdisk&ensp;创建MBR分区  
gdisk创建GPT分区  
parted&ensp;高级分区操作  
- 重新设置内存中的内核分区表版本  
partprobe  
一个设备可以同时挂载到多个目录。  
一个目录不可以挂载多个设备。  
1分区  
2创建文件系统  
3挂载  
例如&ensp;gdisk&ensp;/dev/sdc&ensp;&ensp;分区
mkfs.ext4&ensp;/dev/sdc4&ensp;&ensp;给sdc4系统  
mount&ensp;/dev/sdc4&ensp;/mnt&ensp;&ensp;&ensp;挂载到/mnt  
