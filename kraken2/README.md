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

### 数据库建立
生成`hash.k2d`, `opts.k2d`, `taxo.k2d`三个文件
- hash.k2d: Contains the minimizer to taxon mappings
- opts.k2d: Contains information about the options used to build the database
- taxo.k2d: Contains taxonomy information used to build the database

```bash
kraken2-build --build --db kraken_db --threads 24

```


### 系统分类

```bash
# 单个序列
kraken2 --db kraken_db seqs.fa
```

```bash
# 双端测序
kraken2 --db /data/zhusitao/database/Microbes/kraken2/20250313 \
        --paired --threads 48 --report aH1_B_kraken_taxonomy.txt --output aH1_B_kraken_output.txt \
        ../01.fastp/aH1_B_R1.clean.fq.gz ../01.fastp/aH1_B_R2.clean.fq.gz
# 生成 aH1_B_kraken_output.txt和aH1_B_kraken_taxonomy.txt 文件
# 其中
```
#### kraken_output.txt
[output格式](https://github.com/DerrickWood/kraken2/wiki/Manual#output-formats)
- 1."C"/"U": a one letter code indicating that the sequence was either classified or unclassified.

- 2.The sequence ID, obtained from the FASTA/FASTQ header.

- 3.The taxonomy ID Kraken 2 used to label the sequence; this is 0 if the sequence is unclassified.

- 4.The length of the sequence in bp. In the case of paired read data, this will be a string containing the lengths of the two sequences in bp, separated by a pipe character, e.g. "98|94".

- 5.A space-delimited list indicating the LCA mapping of each k-mer in the sequence(s). For example, "562:13 561:4 A:31 0:1 562:3" would indicate that:

  - the first 13 k-mers mapped to taxonomy ID #562
  - the next 4 k-mers mapped to taxonomy ID #561
  - the next 31 k-mers contained an ambiguous nucleotide
  - the next k-mer was not in the database
  - the last 3 k-mers mapped to taxonomy ID #562
Note that paired read data will contain a "|:|" token in this list to indicate the end of one read and the beginning of another.

When Kraken 2 is run against a protein database (see [Translated Search]), the LCA hitlist will contain the results of querying all six frames of each sequence. Reading frame data is separated by a "-:-" token.

#### kraken_taxonomy.txt  

[taxonomy格式](https://github.com/DerrickWood/kraken2/wiki/Manual#sample-report-output-format)
- 1.Percent of fragments at that taxonomic level
- 2.Number of fragments at that taxonomic level (the sum of fragments at this level and all those below this level)
- 3.Number of fragments exactly at that taxonomic level
- 4.A taxonomic level code: `U`nclassified, `R`oot, `D`omain, `K`ingdom, `P`hylum, `C`lass, `O`rder, `F`amily, `G`enus, or `S`pecies. If the taxonomy is not one of these the number indicates the levels between this node and the appropriate node. See the docs for more information.
- 5.NCBI Taxonomic name
- 6.Scientific name
