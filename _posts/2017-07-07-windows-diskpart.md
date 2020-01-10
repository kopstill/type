---
layout: post
title: Windows diskpart
permalink: '/windows-diskpart'
---

#### Windows diskpart 命令

> 进入Windows安装程序界面按Shift+F10唤起命令提示符窗口，输入diskpart回车进入分区工具  
> 所有命令均可通过diskpart -h获取帮助  
> 官方文档：[中文](https://docs.microsoft.com/zh-cn/windows-server/administration/windows-commands/diskpart){:target="_blank"} | 
           [英文](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/diskpart){:target="_blank"}

##### 常用命令
~~~~
list
select
create
delete
format
convert
clean
~~~~

---

##### 常规步骤
```
list disk
select disk 0
clean
convert gpt
detail disk
create partition efi size 1024
create partition msr size 1024
create partition primary size 71681
list partition
select partition 0
format fs=ntfs quick
assign letter C
create partition extended
create partition logical size 102407
list partition
select partition 0
format fs=ntfs quick
assign letter D
exit
```

---

##### 常用整数分区
~~~
Size     NTFS         FAT32
70 G     71681 MB     71956 MB
80 G     81926 MB     82236 MB
90 G     92162 MB     92516 MB
100 G    102407 MB    102796 MB
150 G    153606 MB    154196 MB
200 G    204806 MB    205596 MB
300 G    307204 MB    308396 MB
500 G    512002 MB    513996 MB
1000 G   1024003 MB   1027996 MB
1024 G   1048579 MB   1052668 MB
~~~
