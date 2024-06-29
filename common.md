# Basic
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

sar -P 0 1 1 # cpu 0, 1 sec, 1 time
sar -r 1 5 # memory, 1 sec, 5 times

ldd /usr/bin/python3

ps aux #pid, RSS=memory
ps ajx #session id
ps -eLF #LWP=thread

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

# Output

## -uname -a
```shell
smallcat at yaos-MacBook-Air.local in ~$uname -a
Darwin yaos-MacBook-Air.local 22.6.0 Darwin Kernel Version 22.6.0: Mon Apr 22 20:50:39 PDT 2024; root:xnu-8796.141.3.705.2~1/RELEASE_ARM64_T8103 arm64

smallcat@7be20bc9d22d:/$ uname -a
Linux 7be20bc9d22d 5.10.104-linuxkit #1 SMP PREEMPT Thu Mar 17 17:05:54 UTC 2022 aarch64 aarch64 aarch64 GNU/Linux

smallcat@raspberrypi:~ $ uname -a
Linux raspberrypi 6.1.21-v8+ #1642 SMP PREEMPT Mon Apr  3 17:24:16 BST 2023 aarch64 GNU/Linux

smallcat@raspberrypi2:~ $ uname -a
Linux raspberrypi2 6.6.20+rpt-rpi-v8 #1 SMP PREEMPT Debian 1:6.6.20-1+rpt1 (2024-03-07) aarch64 GNU/Linux

[z30130@wisteria04 ~]$ uname -a
Linux wisteria04 4.18.0-372.9.1.el8.x86_64 #1 SMP Fri Apr 15 22:12:19 EDT 2022 x86_64 x86_64 x86_64 GNU/Linux

总结
x86_64 和 aarch64 是两种不同的架构，适用于不同的市场和应用场景。
x86_64 更适合桌面和服务器环境，具有较高的功耗和性能。
aarch64 更适合移动和嵌入式设备，注重低功耗和高效能，逐步进入高性能计算市场。
```

## grep -c processor /proc/cpuinfo
```shell
smallcat@7be20bc9d22d:/$ grep -c processor /proc/cpuinfo
8

smallcat@raspberrypi:~ $ grep -c processor /proc/cpuinfo
4

smallcat@raspberrypi2:~ $ grep -c processor /proc/cpuinfo
4

[z30130@wisteria04 ~]$ grep -c processor /proc/cpuinfo
112
```

## grep Mem /proc/meminfo
```shell
smallcat@7be20bc9d22d:/$ grep Mem /proc/meminfo
MemTotal:       12249876 kB
MemFree:        11374876 kB
MemAvailable:   11458892 kB

smallcat@raspberrypi:~ $ grep Mem /proc/meminfo
MemTotal:        7999812 kB
MemFree:         5850264 kB
MemAvailable:    7594152 kB

smallcat@raspberrypi2:~ $ grep Mem /proc/meminfo
MemTotal:        7997480 kB
MemFree:         4437620 kB
MemAvailable:    7497080 kB

[z30130@wisteria04 ~]$ grep Mem /proc/meminfo
MemTotal:       394503348 kB
MemFree:        150251624 kB
MemAvailable:   287814728 kB
```

## sar -P 0 1 1
```shell
smallcat@7be20bc9d22d:/$ sar -P 0 1 1
Linux 5.10.104-linuxkit (7be20bc9d22d) 	06/25/24 	_aarch64_	(8 CPU)

14:21:09        CPU     %user     %nice   %system   %iowait    %steal     %idle
14:21:10          0      0.99      0.00      0.00      0.00      0.00     99.01
Average:          0      0.99      0.00      0.00      0.00      0.00     99.01

[z30130@wisteria04 ~]$ sar -P 0 1 1
Linux 4.18.0-372.9.1.el8.x86_64 (wisteria04) 	06/25/2024 	_x86_64_	(112 CPU)

02:35:49 PM     CPU     %user     %nice   %system   %iowait    %steal     %idle
02:35:50 PM       0      0.00      0.00      4.00      0.00      0.00     96.00
Average:          0      0.00      0.00      4.00      0.00      0.00     96.00
```

## sar -r 1 5
```shell
smallcat@7be20bc9d22d:/$ sar -r 1 5
Linux 5.10.104-linuxkit (7be20bc9d22d) 	06/25/24 	_aarch64_	(8 CPU)

15:03:43    kbmemfree   kbavail kbmemused  %memused kbbuffers  kbcached  kbcommit   %commit  kbactive   kbinact   kbdirty
15:03:44     11374120  11459328    259512      2.12     11940    551036   2953148     17.96    151704    579860         4
15:03:45     11373868  11459076    259732      2.12     11940    551036   2953148     17.96    151724    580240         4
15:03:46     11373868  11459076    259728      2.12     11940    551036   2953148     17.96    151724    580240         4
15:03:47     11373868  11459076    259716      2.12     11940    551040   2953148     17.96    151724    580240         8
15:03:48     11373868  11459076    259716      2.12     11940    551040   2953148     17.96    151724    580240         8
Average:     11373918  11459126    259681      2.12     11940    551038   2953148     17.96    151720    580164         6

[z30130@wisteria04 ~]$ sar -r 1 5
Linux 4.18.0-372.9.1.el8.x86_64 (wisteria04) 	06/25/2024 	_x86_64_	(112 CPU)

03:04:03 PM kbmemfree   kbavail kbmemused  %memused kbbuffers  kbcached  kbcommit   %commit  kbactive   kbinact   kbdirty
03:04:04 PM 183361880 244127180 211141468     53.52     75720  57868684  49374944     11.58  31053888  58715944     27004
03:04:05 PM 183304572 244094732 211198776     53.54     75720  57893528  49374944     11.58  31053880  58770156     19324
03:04:06 PM 183173356 243988208 211329992     53.57     75720  57918624  49504080     11.61  31053924  58902024     27784
03:04:07 PM 183250292 244089200 211253056     53.55     75720  57943196  49388924     11.58  31053876  58826104     19088
03:04:08 PM 183224420 244087340 211278928     53.56     75720  57967520  49388924     11.58  31053876  58853092     26924
Average:    183262904 244077332 211240444     53.55     75720  57918310  49406363     11.58  31053889  58813464     24025
```

## ldd /usr/bin/python3
```shell
smallcat@7be20bc9d22d:/$ ldd /usr/bin/python3
	linux-vdso.so.1 (0x0000ffff9f226000)
	libc.so.6 => /lib/aarch64-linux-gnu/libc.so.6 (0x0000ffff9f074000)
	libpthread.so.0 => /lib/aarch64-linux-gnu/libpthread.so.0 (0x0000ffff9f044000)
	libdl.so.2 => /lib/aarch64-linux-gnu/libdl.so.2 (0x0000ffff9f030000)
	libutil.so.1 => /lib/aarch64-linux-gnu/libutil.so.1 (0x0000ffff9f01c000)
	libm.so.6 => /lib/aarch64-linux-gnu/libm.so.6 (0x0000ffff9ef71000)
	libexpat.so.1 => /lib/aarch64-linux-gnu/libexpat.so.1 (0x0000ffff9ef3a000)
	libz.so.1 => /lib/aarch64-linux-gnu/libz.so.1 (0x0000ffff9ef10000)
	/lib/ld-linux-aarch64.so.1 (0x0000ffff9f1f6000)

smallcat@raspberrypi:~ $ ldd /usr/bin/python3
	/usr/lib/arm-linux-gnueabihf/libarmmem-${PLATFORM}.so => /usr/lib/arm-linux-gnueabihf/libarmmem-v8l.so (0xf795b000)
	libpthread.so.0 => /lib/arm-linux-gnueabihf/libpthread.so.0 (0xf7916000)
	libdl.so.2 => /lib/arm-linux-gnueabihf/libdl.so.2 (0xf7902000)
	libutil.so.1 => /lib/arm-linux-gnueabihf/libutil.so.1 (0xf78ef000)
	libm.so.6 => /lib/arm-linux-gnueabihf/libm.so.6 (0xf7880000)
	libexpat.so.1 => /lib/arm-linux-gnueabihf/libexpat.so.1 (0xf784c000)
	libz.so.1 => /lib/arm-linux-gnueabihf/libz.so.1 (0xf7824000)
	libc.so.6 => /lib/arm-linux-gnueabihf/libc.so.6 (0xf76d1000)
	/lib/ld-linux-armhf.so.3 (0xf7970000)
	libgcc_s.so.1 => /lib/arm-linux-gnueabihf/libgcc_s.so.1 (0xf76a4000)

smallcat@raspberrypi2:~ $ ldd /usr/bin/python3
	linux-vdso.so.1 (0x0000007fa163a000)
	libm.so.6 => /lib/aarch64-linux-gnu/libm.so.6 (0x0000007fa1560000)
	libz.so.1 => /lib/aarch64-linux-gnu/libz.so.1 (0x0000007fa1520000)
	libexpat.so.1 => /lib/aarch64-linux-gnu/libexpat.so.1 (0x0000007fa14d0000)
	libc.so.6 => /lib/aarch64-linux-gnu/libc.so.6 (0x0000007fa1320000)
	/lib/ld-linux-aarch64.so.1 (0x0000007fa15fd000)

[z30130@wisteria04 ~]$ ldd /usr/bin/python3
	linux-vdso.so.1 (0x00007ffe6e1a2000)
	libcrypto.so.1.1 => /lib64/libcrypto.so.1.1 (0x00007f00bcc50000)
	libpython3.6m.so.1.0 => /lib64/libpython3.6m.so.1.0 (0x00007f00bc70e000)
	libpthread.so.0 => /lib64/libpthread.so.0 (0x00007f00bc4ee000)
	libdl.so.2 => /lib64/libdl.so.2 (0x00007f00bc2ea000)
	libutil.so.1 => /lib64/libutil.so.1 (0x00007f00bc0e6000)
	libm.so.6 => /lib64/libm.so.6 (0x00007f00bbd64000)
	libc.so.6 => /lib64/libc.so.6 (0x00007f00bb99f000)
	libz.so.1 => /lib64/libz.so.1 (0x00007f00bb787000)
	/lib64/ld-linux-x86-64.so.2 (0x00007f00bd33e000)
```
