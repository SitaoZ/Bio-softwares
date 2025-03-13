## Kraken2

[Kraken2](https://github.com/DerrickWood/kraken2/blob/master/docs/MANUAL.markdown)是基于`kmer`进行分类的软件，将`kmer`精确比对回最低共同祖先(lowest common ancestor, LCA), 实现物种分类。

### 软件安装

```bash
./install_kraken2.sh $KRAKEN2_DIR
```


### 数据库下载

```bash
k2 build --db kraken_db \
         --kmer-len 35 --minimizer-len 31 \
         --threads 24 \
         --standard

# plasmid 可能会下载失败，需要使用ftp
kraken2-build --download-library plasmid \
  --db kraken_db \
  --threads 36 \
  --use-ftp

# 下载分类
k2 download-taxonomy 、
   --db kraken_db \
   --threads 36 
```


### 系统分类

```bash
# 单个序列
kraken2 --db kraken_db seqs.fa

# 双端测序
kraken2 --paired --classified-out cseqs#.fq seqs_1.fq seqs_2.fq
```
