# Tmux

tmux是一个terminal multiplexer（终端复用器），它可以启动一系列终端会话。

----

## 安装

```
git clone https://github.com/tmux/tmux.git
cd tmux
sh autogen.sh
./configure && make
```

----

## 使用

自行安装或者直接加载集群上已经安装好的tmux

新建一个会话

```
tmux new -s test1
```

分离会话，退出会话但不结束会话，先按下`Ctrl+b`，再按下`d`，或者直接在命令行输入

```
tmux detach
```

查看现有会话

```
tmux ls
```

重新接入会话

```
tmux attach -t test1
```

结束会话

```
tmux kill-session -t test1
# 或者在当前的会话窗口输入exit
# 或者在当前会话窗口输入Ctrl+d
```

重命名会话

```
tmux rename-session -t test1 test2
```

简单的使用流为：

```
# 首先,新建会话
tmux new -s test1
# 随后再会话里运行指令，入cp,rsync等需要长时间等待的指令
# 分离会话
tmux detach
# 重新接入会话看执行结果
tmux attach -t test1
# 结束会话
exit
```

窗口操作：

```
# 在tmux窗口执行
#划分上下两个窗格
tmux split-window
# 划分左右两个窗格
tmux split-window -h
```

移动光标：

```
tmux select-pane -U
tmux select-pane -D
tmux select-pane -L
tmux select-pane -R
```

或者`Ctrl+b`后再输入上下左右的箭头键
