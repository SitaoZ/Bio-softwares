## Metawrap
[metawrap](https://github.com/bxlab/metaWRAP)

## 安装
[参考](https://blog.csdn.net/Asa12138/article/details/139424634)

```bash
conda create -n metawrap python=2.7
source activate metawrap

# 添加channel的顺序很重要 !!!
conda config --add channels defaults
conda config --add channels conda-forge
conda config --add channels bioconda
conda config --add channels ursky

conda install -c ursky metawrap-mg

```

```bash
metawrap -h

MetaWRAP v=1.3.2
Usage: metaWRAP [module]

        Modules:
        read_qc         Raw read QC module (read trimming and contamination removal)
        assembly        Assembly module (metagenomic assembly)
        kraken          KRAKEN module (taxonomy annotation of reads and assemblies)
        kraken2         KRAKEN2 module (taxonomy annotation of reads and assemblies)
        blobology       Blobology module (GC vs Abund plots of contigs and bins)

        binning         Binning module (metabat, maxbin, or concoct)
        bin_refinement  Refinement of bins from binning module
        reassemble_bins Reassemble bins using metagenomic reads
        quant_bins      Quantify the abundance of each bin across samples
        classify_bins   Assign taxonomy to genomic bins
        annotate_bins   Functional annotation of draft genomes

        --help | -h             show this help message
        --version | -v  show metaWRAP version
        --show-config   show where the metawrap configuration files are stored

```


conda 安装并不下载metawrap使用需要的数据库，需要手动安装数据库。[数据库下载](https://github.com/bxlab/metaWRAP/blob/master/installation/database_installation.md).

1. CheckM数据库
```bash
# 创建存储目录
cd ~/db
mkdir checkm
# 设置CheckM数据存储位置
checkm data setRoot ~/db/checkm
# 手动下载数据库
cd ~/db/checkm
wget https://data.ace.uq.edu.au/public/CheckM_databases/checkm_data_2015_01_16.tar.gz
# 解压下载的数据库
tar -xvf checkm_data_2015_01_16.tar.gz
# 删除压缩文件
rm checkm_data_2015_01_16.tar.gz

```
