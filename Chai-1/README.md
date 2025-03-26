## Chai-1

### Install 

```bash
conda create -n Chai1
conda activate Chai1

conda install python=3.13
conda install conda-forge::rdkit
pip install chai_lab==0.6.1
```

- 报错1: GCC 版本太低
```bash
# meson.build:28:4: ERROR: Problem encountered: NumPy requires GCC >= 8.4
conda install conda-forge::gcc
```
