# sbatch
将整个计算过程，写到脚本中，通过`sbatch`指令提交到计算节点上执行

先介绍一个简单的例子，随后介绍例子中涉及的参数，接着介绍`sbatch`其他一些常见参数，最后再介绍GPU和MPI跨节点作业案例。

**首先是一个简单的例子**

+ 假设我们的计算过程为：在计算节点上运行`hostname`指令，那么就可以这么编写作业脚本；
```
#!/bin/bash
#SBATCH -o job.%j.out
#SBATCH -p compute
#SBATCH -J myFirstJob
#SBATCH --nodes=1 
#SBATCH --ntasks-per-node=1

hostname
```
+ 假设上面作业脚本的文件名为job.sh，通过以下命令提交 `sbatch job.sh`
+ **随后我们介绍脚本中涉及的参数**
```
-o job.%j.out       # 脚本执行的输出将被保存在当job.%j.out文件下，%j表示作业号;
-p compute       # 作业提交的指定分区为compute；
-J myFirstJob       # 作业在调度系统中的作业名为myFirstJob;
--nodes=1           # 申请节点数为1,如果作业不能跨节点(MPI)运行, 申请的节点数应不超过1;
--ntasks-per-node=1 # 每个节点上运行一个任务，默认一情况下也可理解为每个节点使用一个核心，如果程序不支持多线程(如openmp)，这个数不应该超过1；
```

其中：
+ `-p` 指定作业的运行分区，提交作业时必须指定分区，每个分区有不同的属性，如普通计算节点`compute`分区，每个节点核心数为32，内存为384G，通过以下命令可以查看对应集群可用分区，也可以通过`sinfo`查看分区的空闲状态；

除此之外，还有一些常见的参数；

```
--help    # 显示帮助信息；
-A <account>    # 指定计费账户；
-D, --chdir=<directory>      # 指定工作目录；
--get-user-env    # 获取当前的环境变量；
--gres=<list>    # 使用gpu这类资源，如申请两块gpu则--gres=gpu:2
-J, --job-name=<jobname>    # 指定该作业的作业名；
--mail-type=<type>    # 指定状态发生时，发送邮件通知，有效种类为（NONE, BEGIN, END, FAIL, REQUEUE, ALL）；
--mail-user=<user>    # 发送给指定邮箱；
-n, --ntasks=<number>    # sbatch并不会执行任务，当需要申请相应的资源来运行脚本，默认情况下一个任务一个核心，--cpus-per-task参数可以修改该默认值；
-c, --cpus-per-task=<ncpus>      # 每个任务所需要的核心数，默认为1；
--ntasks-per-node=<ntasks>    # 每个节点的任务数，--ntasks参数的优先级高于该参数，如果使用--ntasks这个参数，那么将会变为每个节点最多运行的任务数；
-o, --output=<filename pattern>    # 输出文件，作业脚本中的输出将会输出到该文件；
-p, --partition=<partition_names>    # 将作业提交到对应分区；
-q, --qos=<qos>    # 指定QOS；
-t, --time=<time>    # 允许作业运行的最大时间，目前未名一号和生科一号为5天，教学一号为两天；
-w, --nodelist=<node name list>  # 指定申请的节点；
-x, --exclude=<node name list>   # 排除指定的节点；
```

**接下来是一个GPU作业的例子**

**请注意，GPU节点请按照 GPU:CPU = 1:16 的比例提交任务**
+ 假设我们想要申请一块GPU卡，并通过指令nvidia-smi来查看申请到GPU卡的信息，那么可以这么编写作业脚本
```
#!/bin/bash
#SBATCH -o job.%j.out
#SBATCH --partition=gpu
#SBATCH -J myFirstGPUJob
#SBATCH --nodes=1             
#SBATCH --ntasks-per-node=16
#SBATCH --gres=gpu:1             

nvidia-smi
```
脚本中的一些参数说明如下
```
#SBATCH --partition=gpu      # 作业提交的指定分区为gpu;
#SBATCH --gres=gpu:1         # 每个节点上申请一块GPU卡
```

**最后是一个跨节点多核心的例子**
假设我们想用两个节点，每个节点32个核心来运行vasp，那么可以这么编写作业脚本
```
#!/bin/bash
#SBATCH -o job.%j.out
#SBATCH --partition=compute
#SBATCH -J myFirstMPIJob
#SBATCH --nodes=2
#SBATCH --ntasks-per-node=32

# 导入MPI运行环境
module load openmpi4/4.1.1

# 导入MPI应用程序
module load mvapich2/2.3.6

# 生成 machinefile
srun hostname -s | sort -n >slurm.hosts

# 执行MPI并行计算程序
mpirun -n 64 -machinefile slurm.hosts vasp_std > log
```


