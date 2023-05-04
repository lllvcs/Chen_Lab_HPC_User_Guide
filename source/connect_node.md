# 连接集群

<font size=5>

**请注意！**
</font>
<font size=5>

**登录节点仅限用于以下用途：**
</font>

+ 提交作业 安装配置环境和软件
+ 利用SCP和SFTP传输文件
+ 当作跳板机连接集群内的计算节点
+ 其他不适当的用途可能会被随时终止或封号！

- **默认存储配额为 1TB 请合理规划使用**
- **GPU节点请按照 GPU:CPU=1:16 的比例提交任务**
- **请养成及时备份的良好习惯！**

----

<font size=5>
连接登录节点
</font>

+ 登录节点地址为：`10.20.252.1`和`10.20.252.2`，端口号为`22`
+ Linux\Mac用户直接使用电脑自带的命令行终端通过ssh登录，通过scp或者rsync传输文件
+ Windows用户可以通过Xshell+Xftp或WinSCP进行登录和传输数据
+ Mac用户可以通过Cyberduck传输数据(需在创建书签时设置"传输文件"类型为"使用浏览器连接")
+ 需要用到图形界面的Windows用户可以使用MobaXterm等客户端
+ Xshell需要在登录的时候，选择验证方式为Password。平台支持密钥登录的方式
+ 您也可以访问`https://10.20.252.1`和`https://10.20.252.2`（请忽略浏览器证书错误或不安全报错），进入交互式网站进行提交任务、上传下载文件等操作

**请注意：所有计算节点不可联网，登录节点仅用于提交任务、安装配置环境和软件**

----

<font size=5>
Linux\Mac登录和传输数据
</font>

+ Linux\Mac用户通过自带的命令行终端，以ssh的方式登录
+ 打开终端后通过以下命令连接，连接前请确保在校园网内

```
# user_name为账号，ip_address为所要连接的IP
ssh user_name@ip_address
```

通过scp或者rsync传输数据

```
scp [-r] file username@ip_address:~/
# 该命令将会把本地的名为file的文件上传到集群的home目录下,如果file是一个目录的话还需要加上参数r
scp [-r] username@ip_address:~/file ./
# 该命令将会把服务器上home目录下名为file的文件下载到本地当前文件夹下
rsync [-Pr] file username@ip_address:~/
# 该命令将会把本地的名为file的文件同步到集群的home目录下,如果file是一个目录的话还需要加上参数r
rsync [-Pr] username@ip_address:~/file ./
# 该命令将会把服务器上home目录下名为file的文件同步到本地当前文件夹下
```
<font size=5>
Windows用户使用客户端
</font>

Windows用户可以使用客户端登录集群、上传数据，常见的客户端有Xshell+Xftp和WinSCP，下载Xshell+Xftp时选择免费许可版，安装后通过以下方式登录集群
+ 首先，打开Xshell客户端后，点击左上角 "文件" >> "新建"，输入连接的名称和集群的IP地址
+ 然后，点击连接按钮，输入用户名和密码，此处验证方式选择Password
+ 下次登录集群时，点击"文件">>"打开"，找打对应的连接名称，选择连接即可
+ 最后，登录后，在安装Xftp的前提下，打开文件传输按键（工具栏绿色Xftp图标），即可进行文件传输
