## Shell中的协程

---

---

协程可以同时做两件事。它在后台生成一个子shell，并在这个子shell中执行命令

要进行协程处理，得使用`coproc`命令，还有要在子shell中执行的命令

---

## coproc

```shell
$ coproc sleep 10		# coproc 命令创建一个协程
[1] 2544
$						# 生成一个子shell，并将`sleep 10`命令放到这个子shell中运行

$ jobs
[1]+ Running coproc COPROC sleep 10 &		# jobs命令能够显示出协程的处理状态
$
# bash 中会显示这个后台作业是`coproc`创建的一个协程，名字是‘COPROC’；zsh 显示其是一个普通后台作业
```

```shell
$ coproc My_Job { sleep 10; }	# bash 中可以自定义协程名字（严格按照该示例的格式）
[1] 2570

$ jobs
[1]+ Running coproc My_Job { sleep 10; } &
$
```

---

## 协程自定义命名的要求

自定义协程名字的语法要求（严格）：

```shell
coproc COPROC_NAME { command; }
```

1. 必须确保在第一个花括号`{`和`command`之间有一个空格
2. 必须保证`command`以分号`;`结尾
3. 分号和闭花括号`}`之间有一个空格

---

> 协程能够让你尽情发挥想象力，发送或接收来自子shell中进程的信息
>
> 只有在拥有多个协程的时候才需要对协程进行命名，因为此时需要和它们进行通信
>
> 否则的话，让coproc命令将其设置成默认的名字COPROC就行了