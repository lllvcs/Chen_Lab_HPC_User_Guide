# Pytorch

PyTorch是一个开源的Python机器学习库，基于Torch，用于自然语言处理等应用程序。

----

## 安装

1. 导入conda环境；

   通过module导入需要的torch模块或通过module导入conda环境进行安装

   **建议使用module导入torch模块**

   ```
   module load pytorch(对应版本号)
   ```

2. （若选择conda安装）创建虚拟环境并安装pytorch
   
   CUDA11.7版本
   ```
   conda create -n pytorch_cuda11.7 pytorch torchvision torchaudio pytorch-cuda=11.7 -c pytorch -c nvidia
   ```

   CPU版本
   ```
   conda create -n pytorch_cpu pytorch torchvision torchaudio cpuonly -c pytorch
   ```

1. （若选择conda安装）进入和退出创建好的虚拟环境
   ```
   source activate pytorch_(对应版本号)
   conda deactivate
   ```

----

## 使用与提交作业
1. 创建工作目录并进入
   ```
   mkdir pytorchJob1
   cd pytorchJob1
   ```

2. 将运行pytorch需要的相关文件上传到该文件夹下，这里创建一个简单的`test.py`程序，用于检测GPU是否可用
   ```
   import torch
   print(torch.cuda.is_available())
   torch.zeros(1).cuda()
   ```
3. 在该文件夹下编写作业脚本，命名为pytorchJob1.sh，脚本内容如下

+ 使用torch模块
   ```
   #!/bin/bash
   #SBATCH -o job.%j.out
   #SBATCH --partition=GPU
   #SBATCH -J pytorch_job_1
   #SBATCH -N 1
   #SBATCH --ntasks-per-node=2
   #SBATCH --gres=gpu:1
   #SBATCH --qos=low

   module load torch/cuda_11.7
   python test.py
   ```

+ 使用conda环境
   ```
   #!/bin/bash
   #SBATCH -o job.%j.out
   #SBATCH --partition=GPU
   #SBATCH -J pytorch_job_1
   #SBATCH -N 1
   #SBATCH --ntasks-per-node=2
   #SBATCH --gres=gpu:1
   #SBATCH --qos=low

   source activate pytorch_cuda11.7
   python test.py
   ```

4. 提交作业
   ```
   sbatch pytorchJob1.sh
   ```
