##### 一：centos

1. 历史：1991年由托瓦兹(Linus Torvalds)

二：vmware虚拟软件

1. 

三：文件管理

1. linux的目录结构简介

   1. linux：以单杠的方式组织文件 / 

2. ```shell
   [root@localhost ~]# ls
   anaconda-ks.cfg
   [root@localhost ~]# pwd   （查看路径）
   /root
   [root@localhost ~]#  cd /  （这是/ 目录）
   [root@localhost /]# pwd
   /（根路径）
   [root@localhost /]# ls
   bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
   [root@localhost /]# ^C
   [root@localhost /]# ^C
   [root@localhost /]# 
   ```

3. 如果想要查看磁盘驱动器当前的可用空间，可以使用df命令     df

4. 同样，要显示可用内存，可以使用free命令。  free

5. ```shell
   -rw-r--r--. 1 root root 1864 May 4 18:01 initial-setup-ks.cfg <=范例说明处
   [ 1 ][ 2 ][ 3 ][ 4 ][ 5 ][ 6 ] [ 7 ]
   [ 权限 ][连结][拥有者][群组][文件容量][ 修改日期 ] [ 檔名 ]
   ```

   