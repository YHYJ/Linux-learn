# 查看子shell

---

---

## 环境变量

```shell
echo $BASH_SUBSHELL			# 返回 0 代表没有子shell
```

> 根据使用的shell不同，该环境变量可能是 `$ZSH_SUBSHELL`等其他名称

## 示例

- 一个命令列表

  ```shell
  $ pwd ; ls ; cd /etc ; pwd ; cd ; pwd ; ls ; echo $BASH_SUBSHELL
  /home/Christine
  Desktop Downloads Music Public Videos
  Documents junk.dat Pictures Templates
  /etc
  /home/Christine
  Desktop Downloads Music Public Videos
  Documents junk.dat Pictures Templates
  0				# 最后输出 0 ，代表没有生成子shell来运行这些命令
  ```

- 一个进程列表

  ```shell
  $ (pwd ; ls ; cd /etc ; pwd ; cd ; pwd ; ls ; echo $BASH_SUBSHELL)
  /home/Christine
  Desktop Downloads Music Public Videos
  Documents junk.dat Pictures Templates
  /etc
  /home/Christine
  Desktop Downloads Music Public Videos
  Documents junk.dat Pictures Templates
  1				# 最后输出 1 ，代表创建了子shell来运行这个进程列表
  ```


---

子shell的作用和优劣

> 在shell脚本中，经常使用子shell进行多进程处理
>
> 但是采用子shell的成本不菲，会明显拖慢处理速度
>
> 在交互式的CLI shell会话中，子shell同样存在问题，它并非真正的多进程处理，因为终端控制着子shell的I/O