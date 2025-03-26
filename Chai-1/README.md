## Chai-1

### Install 

```bash
conda create -n Chai1
conda activate Chai1

conda install python=3.13
conda install conda-forge::rdkit
# 解决下面的报错后，再进行安装
pip install chai_lab==0.6.1
```

- 报错1: GCC 版本太低
```bash
# meson.build:28:4: ERROR: Problem encountered: NumPy requires GCC >= 8.4
conda install conda-forge::gcc
```

- 报错2：C++编译器
```bash
# ERROR: C++ Compiler does not support -std=c++17
conda install conda-forge::cxx-compiler
```
