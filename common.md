# Basics
```shell
lsblk # tree
lsblk -l # list

tar -zxvf abc.tar.gz
tar -jxvf abc.tar.bz2

find -name *.sh
find -iname *.SH # case-insensitive

grep tecmint /etc/passwd
grep -i TECMINT /etc/passwd
ps -A | grep -i ssh

df -h # human-readable
du -h # human-readable

sudo ss -tuln # -t TCP, -u UDP, -l listening, -n numerical address

free -k # kilobyte
free -m # megabyte
free -g # gigabyte

#https://cloud.tencent.com/developer/article/1725841
#文件的创建者为默认的所有者，默认的所属组也是文件创建者
chmod [{ugoa}{+-=}{rwx}] [文件或目录] #u:所有者, g:所属组, o:其他人, a:所有人, r:可以查看文件内容,可以列出目录中的内容, w:可以修改文件内容,可以在目录中创建和删除文件, x:可以执行文件,可以进入目录

#linux中只有root能改变文件所有者,即便是创建者都不可以
chown [用户] [文件或目录]

#执行权限:所有用户
chgrp [用户组] [文件或目录]

#linux中文件夹的缺省权限时rwxr-xr-x,文件的缺省权限是rw-r–r–,新建文件不具备可执行权限.使用umask改变新建文件或目录的缺省权限
umask 
```
