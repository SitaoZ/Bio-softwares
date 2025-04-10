# RGI 
Resistance Gene Identifier(RGI) 根据同源性和 SNP 模型从蛋白质或核苷酸数据预测抗生素抗性基因。
数据来源于[The Comprehensive Antibiotic Resistance Database](https://card.mcmaster.ca/)（CARD）数据库。


## 安装
- 方法一
```bash
# 查询安装包
mamba search --channel conda-forge --channel bioconda --channel defaults rgi

# 安装
mamba install --channel conda-forge --channel bioconda --channel defaults rgi

# 指定版本
mamba install --channel conda-forge --channel bioconda --channel defaults rgi=6.0.3

# 移除
mamba remove rgi
```bash

- 方法二
```bash 
# pip
git clone https://github.com/arpcard/rgi
conda env create -f conda_env.yml
conda activate rgi
pip install git+https://github.com/arpcard/rgi.git
# 或者
python setup.py build
python setup.py test
python setup.py install

```

## 使用

```bash
rgi --help

```

## 数据库

```bash
wget https://card.mcmaster.ca/latest/data
tar -xvf data ./card.json
rgi load --card_json ./card.json --local
rgi database --version --local
rgi load --card_json ./card.json # 将数据库放入Python的site-packages
rgi database --version


# 删除老版本数据库
rgi clean --local # 本地删除
rgi clean # 系统删除
```
