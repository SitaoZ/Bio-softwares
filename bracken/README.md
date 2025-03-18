## Bracken 

Bracken (Bayesian Re-estimation of Abundance with KrakEN)是用来计算宏基因组样本物种丰度的软件。

[Bracken](https://ccb.jhu.edu/software/bracken/index.shtml?t=manual)（使用 KrakEN 进行丰度贝叶斯重估）是一种高度精确的统计方法，用于计算宏基因组样本 DNA 序列中物种的丰度。
Bracken 使用 Kraken（一种高度精确的宏基因组分类算法）分配的分类标签来估计样本中每个物种的read数量。Kraken 将read分类到分类树中最佳匹配的位置，但不估计物种的丰度。
我们使用 Kraken 数据库本身来得出描述每个基因组中有多少序列与数据库中其他基因组相同的概率，并将此信息与特定样本的分配相结合，以估计物种级别、属级别或更高级别的丰度。
与 Kraken 分类器结合使用时，即使样本包含两个或更多近乎相同的物种，Bracken 也能产生准确的物种和属级别丰度估计值。

[为什么不使用Kraken进行丰度计算，而要使用Bracken](https://microbe.net/2017/04/27/why-use-bracken-instead-of-kraken/)
## Bracken 安装

```bash
sh install_bracken.sh
```

## Bracken 使用

0. 提前安装好kraken数据库，参考kracken软件的使用
```bash
kraken-build --db=${KRAKEN_DB} --threads=10

kraken2-build --db=${KRAKEN2_DB} --threads=10
```

1. 建立bracken数据库
  - 一步法
```bash
bracken-build -d ./20250313 -t 96 -k 35 -l 151 -x /data/zhusitao/pipeline/Metagenome/software/Kraken2/kraken2/
```
一步法执行报错`bracken-build: line 179: kraken2: Argument list too long`，使用三步法

  - 三步执行法
```bash
KRAKEN_DB=/data/zhusitao/database/Microbes/kraken2/20250313
READ_LEN=150
KMER_LEN=35
THREADS=48

#1
kraken2 --db=${KRAKEN2_DB} --threads=${THREADS} <( find -L ${KRAKEN_DB}/library \( -name "*.fna" -o -name "*.fasta" -o -name "*.fa" \) -exec cat {} + ) > ${KRAKEN2_DB}/database.kraken
#2
kmer2read_distr --seqid2taxid ${KRAKEN_DB}/seqid2taxid.map --taxonomy ${KRAKEN_DB}/taxonomy --kraken ${KRAKEN2_DB}/database.kraken --output ${KRAKEN2_DB}/database${READ_LEN}mers.kraken -k ${KMER_LEN} -l ${READ_LEN} -t ${THREADS}
#3
python generate_kmer_distribution.py -i ${KRAKEN2_DB}/database${READ_LEN}mers.kraken; -o ${KRAKEN2_DB}/database${READ_LEN}mers.kmer_distrib
```
2. kraken2 计算
```bash
kraken2 --db ${KRAKEN2_DB} \
        --paired --threads ${THREADS} \
        --confidence 0.8 \
        --report ${sample}_kraken_taxonomy.txt \
        --output ${sample}_kraken_output.txt \
        --gzip-compressed \
        ../01.fastp/${sample}_R1.clean.fq.gz ../01.fastp/${sample}_R2.clean.fq.gz
```
3. bracken 计算
```bash
bracken -d ${KRAKEN2_DB} -i ../02.kraken2/L1_A_kraken_taxonomy.txt -o L1_A.bracken -r 150 -l S -t 1
```

4. 合并结果
```bash
/data/zhusitao/pipeline/Metagenome/software/Bracken/Bracken/analysis_scripts/combine_bracken_outputs.py  --files s1.bracken s2.bracken s3.bracken --names A,B,C -o merge.bracken.result
```
