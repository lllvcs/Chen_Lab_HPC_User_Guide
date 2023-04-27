# Screen

screen为多重视窗管理程序。此处所谓的视窗，是指一个全屏幕的文字模式画面。通常只有在使用ssh登入主机或是使用老式的终端机时，才有可能用到screen程序

----

## Screen基本使用

```
# 新建一个会话
screen -S session_name

# 退出但不关闭当前会话
crtl+a+d

# 退出并关闭当前会话
exit
## 或者
ctrl+d

# 列出所有的会话
screen -ls
## 会话的状态有'Detached','Attached', 前者为后台挂起状态，后者为连接状态

# 远程挂起会话，会话状态为'Attached'时表示有窗口正在连接该会话，远程挂起指定会话后，连接该会话的窗口将被退出
screen -d session_name

# 连接指定的会话
screen -r session_name
## 如果需要连接的会话状态为'Attached'
## 则会返回There is no screen to be resumed matching xxx
## 这时候需要先远程挂起该会话后再连接
screen -d -r session_name
```