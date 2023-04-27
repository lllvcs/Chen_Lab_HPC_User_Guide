# sacct

通过`sacct`和`scontrol show job`显示作业信息

先介绍通过`scontrol show job`显示作业信息；随后介绍通过`sacct`显示作业信息；最后介绍通过`saact`按指定格式输出作业信息。

----

## **通过`scontrol show job`显示作业信息**

`scontrol show job` 只能显示正在运行或者刚结束没多久的作业信息；

```
# 查看作业7454119的详细信息
scontrol show job 7454119
```

## **通过`sacct`显示作业信息**

通过`sacct`查询已经结束作业的相关信息

```
sacct -j 7454119
```

输出内容会包括，作业号，作业名，分区，计费账户，申请的CPU数量，状态，结束代码

```
JobID   JobName   Partition   Account   AllocCPUS   State ExitCode
```

## **通过sacct按照指定格式输出作业信息**

```
squeue -o "%.18i %.9P %.12j %.12u %.12T %.12M %.16l %.6D %R" -u $USER
```

如下所示，指定输出内容为：作业号，作业名，分区，运行节点，申请核数，状态，作业结束时间
```
format=jobid,jobname,partition,nodelist,alloccpus,state,end
sacct --format=$format -j 7454119
```
