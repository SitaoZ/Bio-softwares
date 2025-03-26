## Chai-1

Chai-1: Decoding the molecular interactions of life.
[Chai-1](https://www.chaidiscovery.com/) enables unified prediction of proteins, small molecules, DNA, RNA, covalent modifications, and more.

### Install 

```bash
conda create -n Chai1
conda activate Chai1

conda install python=3.13
# rdkit-2024.09.6, 注意安装的软件和python版本的适配关系，python版本对了，
# 安装特定的软件比较快，查询对应关系可以去conda 上查看Files中软件与python的对应
conda install conda-forge::rdkit

# 解决下面的报错后，再进行安装
pip install chai_lab==0.6.1
```

- 报错1: GCC 版本太低
```bash
# meson.build:28:4: ERROR: Problem encountered: NumPy requires GCC >= 8.4
# gcc 14.2.0
conda install conda-forge::gcc
```

- 报错2：C++编译器
```bash
# ERROR: C++ Compiler does not support -std=c++17
# cxx-compiler 1.9.0
conda install conda-forge::cxx-compiler
```

### Usage

```bash
chai-lab --help
```


