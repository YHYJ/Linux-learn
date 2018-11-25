# bash作为登录默认shell

---

---

bash作为登录默认shell启动的时候会从5个启动文件里读取命令：

- `/etc/profile`				# bash默认的主启动文件，系统上每个用户登录时都会执行这个文件
- `$HOME/.bash_profile`                  # 某个用户专属的启动文件，读取权重1
- `$HOME/.bash_login`                      # 某个用户专属的启动文件，读取权重2
- `$HOME/.profile`                            # 某个用户专属的启动文件，读取权重3
- `$HOME/.bashrc`                              # 一般通过其他启动文件启动

