# Linux实用命令

---

---

### tail —— 查看文件末尾内容

```shell
tail -f example.txt		# 持续追踪该文件内容变化
```

---

### tr —— 替换文本文件中的字符

```shell
cat example.txt | tr [a-z] [A-Z]	# 将该文件中所有英文全部替换为大写
```

---

### stat —— 显示指定文件/文件系统本身的详细信息

> 注意Linux所有对象都是文件
>
> `stat`输出的是文件本身的详细信息，而非文件内容的信息

```shell
$ stat ~   
  文件：/home/yj
  大小：4096      	块：8          IO 块：4096   目录
设备：808h/2056d	Inode：10485761    硬链接：85
权限：(0755/drwxr-xr-x)  Uid：( 1000/      yj)   Gid：( 1000/      yj)
最近访问：2018-10-11 16:16:00.136262391 +0800
最近更改：2018-10-11 16:19:52.515352672 +0800
最近改动：2018-10-11 16:19:52.515352672 +0800
创建时间：-
```

---

### file —— 显示指定文件内容的类型

> 不同于`stat`命令，`file`显示的是文件的内容的信息

```shell
$ file anaconda-ks.cfg
anaconda-ks.cfg: ASCII text
$ file /dev/sda
/dev/sda: block special
$ file bacpypes/       
bacpypes/: directory
```

---

### cut —— 按列提取文本文件里的字符

> 提取`/etc/passwd`文件以冒号作为分隔符的第一列字符（即所有账户名）

```shell
$ cut -d: -f1 /etc/passwd		# -d 指定分隔符 ； -f 指定操作的列数
root
daemon
bin
yj
systemd-coredump
glances
mpd
```

---

### dd —— 按块复制或转换文件

#### 复制

> 不指定`count`参数会导致一直写入，需要手动停止
>
> 参数`bs`默认大小是512bytes
>
> `count * bs = 需要的数据的大小`

```shell
$ dd if=/dev/zero of=hahaha count=1 bs=1000M
记录了1+0 的读入
记录了1+0 的写出
1048576000 bytes (1.0 GB, 1000 MiB) copied, 1.86953 s, 561 MB/s
```

| 参数  | 作用               |
| ----- | ------------------ |
| if    | 数据输入源         |
| of    | 数据输出端         |
| count | 要复制的 块 的个数 |
| bs    | 每个 块 的大小     |

#### 转换

> 将光盘中的数据制作成iso镜像文件

```shell
dd if=/dev/cdrom of=RHEL-server-7.0-x86_64-LinuxProbe.Com.iso
记录了7311360+0 的读入
记录了7311360+0 的写出
3743416320 bytes (3.7 GB) copied, 370.758 s, 10.1 MB/s
```

---

### find —— 按条件进行文件查找

| 参数               | 作用                                                         |
| ------------------ | ------------------------------------------------------------ |
| -name              | 按名称匹配                                                   |
| -size              | 按大小匹配（+50KB为查找大于50KB的文件，-50KB为查找小于50KB的文件） |
| -perm              | 按权限匹配（mode为完全匹配，-mode为包含匹配）                |
| -user              | 按属主匹配                                                   |
| -group             | 按属组匹配                                                   |
| -nouser            | 匹配无属主的文件                                             |
| -nogroup           | 匹配无属组的文件                                             |
| -prune             | 忽略某个目录                                                 |
| -exec ...... {} \; | 进一步处理搜索结果                                           |
| -mtime -n/+n       | 匹配修改内容的时间（-n 指 n 天以内， +n 指 n 天以前）        |
| -atime -n/+n       | 匹配访问文件的时间（-n 指 n 天以内， +n 指 n 天以前）        |
| -ctime -n/+n       | 匹配修改文件权限的时间（-n 指 n 天以内， +n 指 n 天以前）    |
| -newer f1 !f2      | 匹配比文件f1新但是比文件f2旧的文件                           |
| --type b/d/c/p/l/f | 匹配文件类型（后面的字母参数依次表示块设备、目录、字符设备、管道、链接文件、文本文件） |

#### -exec参数

> `-exec`参数用于把`find`命令搜索到的结果交由紧随其后的命令作进一步处理，类似于管道

```shell
$ find / -user yj -exec cp {} ~/Desktop \;
# 在整个文件系统中查找属主是"yj"的文件并复制到路径'~/Desktop'下
# 其中`{}`表示`find`搜索出的每个文件
# 带`-exec`参数的命令结尾必须是`\;`
```

---

### hostnamectl —— 查询或修改系统主机名及其他信息

```shell
$ hostnamectl
  Static hostname: YJ-Linux
         Icon name: computer-laptop
           Chassis: laptop
        Machine ID: 61d7a5cfa84345b5a3ba2715149b73c4
           Boot ID: e1cc7b8c8db24ddc8924638845c2468c
  Operating System: Deepin 15
            Kernel: Linux 4.15.0-29deepin-generic
      Architecture: x86-64
```

---

### id —— 显示真实有效的用户ID和组ID，可以用来判断指定的用户是否存在

> 显示指定用户的用户和用户组信息，在没有指定用户名的情况下显示当前用户的信息

```shell
$ id yj                
uid=1000(yj) gid=1000(yj) 组=1000(yj),7(lp),27(sudo),100(users),107(netdev),110(lpadmin),116(scanner),122(sambashare),996(bumblebee),1001(fuse)

$ id root
uid=0(root) gid=0(root) 组=0(root)

$ id backup
uid=34(backup) gid=34(backup) 组=34(backup)
```

---

### at —— 一次性计划任务

> `at`命令在设置计划任务时默认使用交互式方法

```shell
$ at 15:00				# 格式是：at <time>
at > 计划任务1
at > 计划任务2
......
at > 计划任务n
at > 计划任务完成同时按下 Ctrl + D 组合键来结束编写计划任务

# 使at非交互式写入任务
$ echo "systemctl restart httpd" | at 23:30

$ at -l					# 查看计划任务
5	Thu Oct 18 15:07:00 2018 a yj

$ atrm job_num			# 删除计划任务（根据任务编号）
```

---

### crontab —— 永久计划任务

> 其服务端是`cron`或者`crond`
>
> crontab配置语句的格式是：`分 时 日 月 星期 命令`

| 字段 | 说明                         | 备注           |
| ---- | ---------------------------- | -------------- |
| 分   | 取值范围：0~59的整数         |                |
| 时   | 取值范围：0~23的整数         |                |
| 日   | 取值范围：1~31的整数         |                |
| 月   | 取值范围：1~12的整数         |                |
| 星期 | 取值范围：0~7的整数          | 0和7都代表周日 |
| 命令 | 要执行的**命令**或者**脚本** |                |

- 定时采用24小时制

```shell
$ crontab -e				# 使用`$EDITOR`指定的编辑器编辑计划任务

$ crontab -l				# 查看已存在计划任务：每周1/3/5的3:25备份/home/wwwroot
25 3 * * 1,3,5 /usr/bin/tar -czvf wwwroot.tar.gz /home/wwwroot
```

