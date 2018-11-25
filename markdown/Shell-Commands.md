# Shell内建命令

---

---

### read —— 等同于Python的input

> 读取用户输入，并将输入作为指定变量的值，未指定变量的话自动赋值给特定变量**REPLY**

```shell
read (选项) (参数)
-p：向用户显示提示信息；
-t：指定读取值时等待的时间，单位秒(s)；

$ read					# 读取标准输入并赋值给特定变量REPLY
1
$ echo $REPLY
1

$ read name				# 读取标准输入并赋值给变量name
yj
$ echo $name
yj

$ read first last		# 读取多个标准输入（空格分隔），将第一个值放到变量first中，其他值放在last中
1 2 3
$ echo $first $last
1 2 3
$ echo $first
1
$ echo $last
2 3

$ read -p "text:"		# 打印提示信息，等待输入，并将输入存储在REPLY中
text:1
$ echo $REPLY
1

$ read -r line			# 允许输入包含反斜杠
1\2
$echo $line
1\2

$ read -t 3				# 指定读取等待时间为3秒
3						# 等待3秒没有按Enter确认的话本次输入无效
$ echo $REPLY
3

$ read -n 2 var			# -n参数设定输入两个字符（回车也是字符）就退出输入并将输入存入变量var
12
$ echo $var
12

$ read -d ":" var		# 用分界符“:”结束输入
111
222
333 444
$ echo $var
111 222 333 444

$ read -s				# 隐藏用户输入回显，但是REPLY变量可以打印出来
（这里是输入回显，但看不见）
```

