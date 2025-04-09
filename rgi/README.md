# RGI 
Resistance Gene Identifier(RGI) 根据同源性和 SNP 模型从蛋白质或核苷酸数据预测抗生素抗性基因。
数据来源于[The Comprehensive Antibiotic Resistance Database](https://card.mcmaster.ca/)（CARD）数据库。


# 安装

```bash
# 查询安装包
mamba search --channel conda-forge --channel bioconda --channel defaults rgi

# 安装
mamba install --channel conda-forge --channel bioconda --channel defaults rgi

# 指定版本
mamba install --channel conda-forge --channel bioconda --channel defaults rgi=6.0.3

# 移除
mamba remove rgi

# pip
pip install git+https://github.com/arpcard/rgi.git
```

## 使用

```bash
rgi --help

```
