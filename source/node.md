# 现有节点

国科大杭高院 Chen Lab 高性能计算集群现有66个不同功能的节点，其中包括登录节点、普通计算节点、大内存节点、胖节点、GPU节点等。

在存储和网络配置方面，共有2.1PB (RAID 6) 阵列存储，100G Infiniband 集群内互联，10G光纤直连学校中心机房。

<font size=5>
具体节点如下表所示
</font>

|节点名|型号|数量|CPU|内存|GPU型号|GPU显存|GPU驱动|
| :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | 
| login | SR650 | 2 | 2*Intel(R) Xeon(R) Silver 4210R CPU @ 2.40GHz | 128G | 无 | 无 | 无 |
| compute | SD530 | 30 | 2*Intel(R) Xeon(R) Gold 6226R CPU @ 2.90GHz | 384G | 无 | 无 | 无 |
| big | SD530 | 24 | 2*Intel(R) Xeon(R) Gold 6226R CPU @ 2.90GHz | 768G | 无 | 无 | 无 |
| fat | SR950 | 1 | 8*Intel(R) Xeon(R) Platinum 8260 CPU @ 2.40GHz | 8192G | 无 | 无 | 无 |
| gpu | SR650 | 5 | 2*Intel(R) Xeon(R) Gold 6226R CPU @ 2.90GHz | 512G | 2*NVIDIA GeForce RTX 3080 Ti | 2*12G | 550.54.15 with CUDA12.4 |
| private-gp01 | MicroStar | 1 | 1*AMD EPYC 7542 32-Core Processor @ 2.90GHz | 256G | 4*NVIDIA GeForce RTX 4090 D | 4*24G | 550.54.15 with CUDA12.4 |
