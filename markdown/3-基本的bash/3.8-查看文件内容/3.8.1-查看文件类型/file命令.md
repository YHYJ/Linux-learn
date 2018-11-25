# file——判断文件类型 状态

---

---

## 普通文本文件

```bash
$ file file命令.md
>>> file命令.md: UTF-8 Unicode text	# 文件名: 字符编码 文件类型
```
## 链接文件

```bash
$ file sl_data_file
>>> sl_data_file: symbolic link to 'data_file'		# 文件名: 链接文件 所链接的文件
```

## shell脚本文件

```bash
$ file my_script
>>> my_script: Bourne-Again shell script, ASCII text executable		# 文件名: shell脚本 字符编码 文件类型 可执行
```

## 二进制文件

```bash
$ file /bin/ls
>>> /bin/ls: ELF 64-bit LSB pie executable x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 2.6.32, BuildID[sha1]=2589c6a3d284b02b08c483d4ffc8a3c4b764b773, stripped
# 文件名: 编译时面向的平台 ………………
```

