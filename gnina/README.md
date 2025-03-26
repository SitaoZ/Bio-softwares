## Gnina

## Install

```bash
conda create -n gnina
conda activate  gnina
conda install anaconda::cmake
conda install conda-forge::gcc
conda install conda-forge::cxx-compiler
conda install nvidia/label/cuda-12.4.0::cuda-compiler
conda install python=3.12
conda install conda-forge::openbabel
conda install anaconda::protobuf
conda install conda-forge::libprotobuf
conda install pytorch::pytorch
```


- 报错1

```bash
# ImportError: /home/zhusitao/miniconda3/envs/gnina/lib/python3.12/site-packages/torch/lib/libtorch_cpu.so: undefined symbol: iJIT_NotifyEvent
conda install conda-forge::mkl
```

- 报错2

```bash
# Could not find a package configuration file provided by "Torch" with any of
#  the following names:#

#    TorchConfig.cmake
#    torch-config.cmake

#  Add the installation prefix of "Torch" to CMAKE_PREFIX_PATH or set
#  "Torch_DIR" to a directory containing one of the above files.  If "Torch"
#  provides a separate development package or SDK, be sure it has been
#  installed.
export Torch_DIR= /home/zhusitao/miniconda3/envs/gnina/lib/python3.12/site-packages/torch/share/cmake/
```
