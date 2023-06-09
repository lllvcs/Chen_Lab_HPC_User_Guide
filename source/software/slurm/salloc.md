# salloc

申请计算节点，然后登录到申请到的计算节点上运行指令

----

## **一个简单的例子**

+ 申请一个计算节点6个核心，运行时间为2小时，并跳转到该节点上运行程序

   ```
   salloc -p compute -N 1 -n 1 -c 6 -t 2:00:00
   # salloc 申请成功后会返回申请到的节点和作业ID等信息，假设申请到的是c02节点，作业ID为1078858。如无法获取节点信息，请执行命令squeue进行查询。
   ssh c02      # 直接登录到刚刚申请到的节点c02调式作业
   scancel 1078858   # 计算资源使用完后取消作业
   squeue -j 1078858 # 查看作业是否还在运行，确保作业已经退出，避免产生不必要的费用
   ```

----

## **一个GPU节点的例子**

+ 申请一个gpu节点，16个核心，1块GPU卡，运行时间为2天，并跳转到节点上运行程序

   ```
   salloc -p gpu -N 1 -n 1 -c 16 --gres=gpu:1 -t 2-00:00:00
   # 假设申请成功后返回的作业号为1078859，申请到的节点是g05。如无法获取节点信息，请执行命令squeue进行查询。
   ssh g05 # 登录到gpu05上调式作业
   scancel 1078859  # 计算资源使用完后取消作业
   squeue -j 1078859 # 查看作业是否还在运行，确保作业已经退出，避免产生不必要的费用
   ```
+ **注意：** 由于GPU节点上的GPU卡是共享的，所以在申请GPU节点时，需要指定GPU卡的数量，否则会报错

----

## **一个跨节点使用案例**

+ 申请两个大内存节点，每个节点12个核心，运行时间为6小时20分钟

   ```
   salloc -p big -N 2 -n 12 -t 6:20:00
   # salloc 申请成功后会返回申请到的节点和作业ID等信息，假设申请到的是b[05-06]节点，作业ID为1078857。如无法获取节点信息，请执行命令squeue进行查询。
   # 这里申请两个节点，每个节点12个进程，每个进程一个核心
   
   # 根据需求导入MPI环境
   module load openmpi4/4.1.1
   module load mvapich2/2.3.6
   
   # 根据以下命令生成MPI需要的machine file
   srun hostname -s | sort -n > slurm.hosts
   
   mpirun -np 24 -machinefile slurm.hosts hostname
   
   scancel 1078857  # 计算资源使用完后取消作业
   squeue -j 1078857 # 查看作业是否还在运行，确保作业已经退出，避免产生不必要的费用
   ```
+ **注意：** 由于MPI的运行机制，需要在申请节点时指定每个节点的进程数，否则会报错