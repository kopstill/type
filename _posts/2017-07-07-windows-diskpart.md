---
layout: post
title: Windows diskpart
image: '/images/posts/2.jpg'
permalink: '/windows-diskpart'
---

#### Windows diskpart 命令集合

> 进入Windows操作系统安装界面按Shift+F10输入diskpart回车  
> 所有命令都可以通过diskpart -h获取帮助

##### 常用命令 #####
~~~~
clean
list
select
create
format
exit
~~~~

---

##### 常规步骤
```
list disk
select disk 0
convert gpt
list disk
detail disk
create partition efi size 1024
create partition msr size 1024
list partition
create partition primary size=71681
active
format fs=ntfs quick
(assign letter(=)C)
(list volume)
create partition extended
list partition
(select partition 0)
create partition logical size=102407
(delete partition)
format fs=ntfs quick
exit
```

---

##### 常用整数分区 #####
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
