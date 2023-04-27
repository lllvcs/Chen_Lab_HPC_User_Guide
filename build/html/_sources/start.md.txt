# 快速入门

在开通邮件中获取账号后，Linux\Mac用户可通过命令行登录集群，Windows用户则可以通过ssh客户端登录集群；登录集群后，编写作业脚本，并通过sbatch指令将作业提交到计算节点上执行；此外，集群上安装了常见的计算软件，通过module指令导入计算环境。

----

## **请注意！**

**登录节点仅限用于以下用途：**
+ 提交作业 安装配置环境和软件
+ 利用SCP和SFTP传输文件
+ 当作跳板机连接集群内的计算节点
+ 其他不适当的用途可能会被随时终止或封号！

- **默认存储配额为 1TB 请合理规划使用**
- **GPU节点请按照 GPU:CPU=1:16 的比例提交任务**
- **请养成及时备份的良好习惯！**

----

## **登录集群，登录前确保网络环境为校园网**

+ Linux\Mac用户直接使用系统自带的终端通过ssh命令登录
   ```
   ssh user_name@ip_address
   ```
+ Windows用户可使用Xshell客户端进行登陆。为了方便文件传输，可同时下载并安装Xftp，安装完后点击软件左上角新建连接，输入IP和用户名密码即可登录；
+ 更多关于登录集群的内容，可参考 **[连接集群](./connect_node.html)** 部分内容。

----

## **登录后，编写作业脚本，并通过sbatch命令将作业提交到计算节点上执行**。
- 假设我们的计算过程为：在计算节点上运行hostname指令，那么就可以这么编写作业脚本；

```
#!/bin/bash
#SBATCH -o job.%j.out
#SBATCH --partition=compute
#SBATCH -J myFirstJob
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=1

hostname
```
- 假设上面作业脚本的文件名为job.sh，通过以下命令提交：`sbatch job.sh`

----

## **集群安装了常见的计算软件，可以通过module指令导入计算环境**
+ **[推荐使用module加载conda进行环境和软件包管理](./software/module/module.html#id3)，避免重复安装conda软件**
+ 可以通过module加载平台上装有的软件环境，也可以自行安装配置需要的计算环境，下面的作业脚本加载了`plink/1.90`的软件环境，具体可用的软件环境可使用命令`module avail`指令进行查看。

```
#!/bin/bash
#SBATCH -o job.%j.out
#SBATCH --partition=compute
#SBATCH -J myFirstPlinkJob
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=2

module plink/1.90
plink
```
