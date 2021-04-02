# Ubuntu18.04_Init
Ubuntu18.04-初始设置



## 1. 开启root用户

```shell
# 开启root用户
zhou@ubuntu:~$ sudo passwd
Enter new UNIX password: 
Retype new UNIX password: 
passwd: password updated successfully
# 切换至root用户
zhou@ubuntu:~$ su
Password: 
root@ubuntu:/home/zhou# ls
```



## 2. 换源

```shell
# 进入/etc/apt/目录
root@ubuntu:/home/zhou# cd /etc/apt/
root@ubuntu:/etc/apt# ls
apt.conf.d   preferences.d  sources.list    trusted.gpg.d
auth.conf.d  sources.bak    sources.list.d
# 备份原源列表
root@ubuntu:/etc/apt# cp sources.list sources.list_bak
# 编辑源列表
root@ubuntu:/etc/apt# vi sources.list
# 在文件顶部增加以下任意一个内容
```

```shell
#  阿里源
deb http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
```

```shell
#  中科大源
deb https://mirrors.ustc.edu.cn/ubuntu/ bionic main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-security main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-security main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
```

```shell
# 163源
deb http://mirrors.163.com/ubuntu/ bionic main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ bionic-security main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ bionic-updates main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ bionic-backports main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ bionic main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ bionic-security main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ bionic-updates main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ bionic-backports main restricted universe multiverse
```

```shell
# 清华源
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
```

```shell
# 更新文件后，刷新源
root@ubuntu:/etc/apt# sudo apt-get update
root@ubuntu:/etc/apt# sudo apt-get upgrade
root@ubuntu:/etc/apt# sudo apt-get install build-essential
```



## 3. 安装Vim

系统默认安装了vi，卸载后，安装vim。

```shell
# 卸载vi
root@ubuntu:/# apt-get remove vim-common

# 安装Vim
root@ubuntu:/# apt-get install vim

# 安装完成
root@ubuntu:/# vim -version
VIM - Vi IMproved 8.0 (2016 Sep 12, compiled Oct 13 2020 15:49:09)
Garbage after option argument: "-version"
More info with: "vim -h"
```

配置Vim(可选)。使用命令 $ vim /etc/vim/vimrc 修改vim配置文件 (修改该文件对所有用户都生效)，在该文件最后添加如下代码：

```
set ai                          " 自动缩进，新行与前面的行保持—致的自动空格
set aw                          " 自动写，转入shell或使用：n编辑其他文件时，当前的缓冲区被写入
set flash                       " 在出错处闪烁但不呜叫(缺省)
set ic                          " 在查询及模式匹配时忽赂大小写
set nu
set number                      " 屏幕左边显示行号
set showmatch                   " 显示括号配对，当键入“]”“)”时，高亮度显示匹配的括号
set showmode                    " 处于文本输入方式时加亮按钮条中的模式指示器
set showcmd                     " 在状态栏显示目前所执行的指令，未完成的指令片段亦会显示出来
set warn                        " 对文本进行了新的修改后，离开shell时系统给出显示(缺省)
set ws                          " 在搜索时如到达文件尾则绕回文件头继续搜索
set wrap                        " 长行显示自动折行
colorscheme evening            " 设定背景为夜间模式
filetype plugin on              " 自动识别文件类型，自动匹配对应的, “文件类型Plugin.vim”文件，使用缩进定义文件
set autoindent                  " 设置自动缩进：即每行的缩进值与上一行相等；使用 noautoindent 取消设置
set cindent                     " 以C/C++的模式缩进
set noignorecase                " 默认区分大小写
set ruler                       " 打开状态栏标尺
set scrolloff=5                 " 设定光标离窗口上下边界 5 行时窗口自动滚动
set shiftwidth=4                " 设定 << 和 >> 命令移动时的宽度为 4
set softtabstop=4               " 使得按退格键时可以一次删掉 4 个空格,不足 4 个时删掉所有剩下的空格）
set tabstop=4                   " 设定 tab 长度为 4
set wrap                        " 自动换行显示
syntax enable
syntax on                       " 自动语法高亮
```



## 4. 开启ssh

```shell
# 安装openssh-server
root@ubuntu:/# apt-get install openssh-server

# 启动ssh服务
root@ubuntu:/# sudo service ssh start

# 查看是否启动成功
root@ubuntu:/# ps -aux | grep ''ssh''
zhou       1747  0.0  0.0  11300   316 ?        Ss   21:40   0:00 /usr/bin/ssh-agent /usr/bin/im-launch env GNOME_SHELL_SESSION_MODE=ubuntu gnome-session --session=ubuntu
root      33021  0.0  0.1  72304  5832 ?        Ss   22:18   0:00 /usr/sbin/sshd -D
root      33132  0.0  0.0  14432  1056 pts/0    R+   22:19   0:00 grep --color=auto ssh

# 允许root用户登录，编辑sshd_config
root@ubuntu:/# vi /etc/ssh/sshd_config
# 修改内容
PermitRootLogin prohibit-password
# 改为
PermitRootLogin yes

# 重启ssh服务
root@ubuntu:/# systemctl restart sshd
```



## 5. 安装net-tools

```shell
# 安装 net-tools
root@ubuntu:/# apt-get install net-tools

# 验证
root@ubuntu:/# ifconfig
```

