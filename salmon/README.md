# Salmon 
[Salmon](https://salmon.readthedocs.io/en/latest/salmon.html) 是RNA-Seq中快速进行转录本定量的比对工具。支持FASTQ/FATSA文件输入，也支持BAM/SAM文件输入。


### 安装
安装可以参考[官网](https://salmon.readthedocs.io/en/latest/building.html#installation)。
也可以使用conda安装
```bash
conda install bioconda::salmon
```

### mapping-based mode
Salmon的映射模式，分为两个阶段索引`index`和定量`quant`。索引只需要一个转录本集合，定量就是将read比对会索引的转录本。
- index
```bash
salmon index -t transcripts.fa -i transcripts_index --decoys decoys.txt -k 31
```

- quant
```bash
# pair-end 
salmon quant -i transcripts_index -l <LIBTYPE> -1 reads1.fq -2 reads2.fq --validateMappings -o transcripts_quant

# single-end
salmon quant -i transcripts_index -l <LIBTYPE> -r reads.fq --validateMappings -o transcripts_quant
```
选择性比对最初由 salmon 中的 `--validateMappings` 标志引入，现在是默认映射策略（从 1.0.0 版本开始），是 salmon 最新版本中引入的一项主要功能增强。

定量结果文件为`quant.sf`，包括`Name`，`Length`，`EffectiveLength`，`TPM`，`NumReads`五列。

- 多文件定量
通常，一个文库可能会被拆分成多个 FASTA/Q 文件。此外，有时用户可能希望同时定量多个重复样本或多个样品，并将它们视为一个文库。  
Salmon 允许用户为其所有需要输入文件的选项（例如 -r、-1、-2）提供一个以空格分隔的读长文件列表。  
当输入为双端读长时，左右列表中文件的顺序必须相同。有多种方法可以为 Salmon 提供多个读长文件，并将它们视为一个文库。  

```bash
# fastq
salmon quant -i transcripts_index -l IU -1 lib_1_1.fq lib_2_1.fq -2 lib_1_2.fq lib_2_2.fq --validateMappings -o out
salmon quant -i transcripts_index -l IU -1 <(cat lib_1_1.fq lib_2_1.fq) -2 <(cat lib_1_2.fq lib_2_2.fq) --validateMappings -o out

# fastq.gz
salmon quant -i transcripts_index -l IU -1 lib_1_1.fq.gz lib_2_1.fq.gz -2 lib_1_2.fq.gz lib_2_2.fq.gz --validateMappings -o out
salmon quant -i transcripts_index -l IU -1 <(gunzip -c lib_1_1.fq.gz lib_2_1.fq.gz) -2 <(gunzip -c lib_1_2.fq.gz lib_2_2.fq.gz) --validateMappings -o out
```
- 交错fastq
Salmon目前不支持Interleaved FASTQ files。但是提供了一个[脚本](https://github.com/COMBINE-lab/salmon/blob/master/scripts/runner.sh)用于将Interleaved FASTQ files文件拆分成pair-end数据。

- 文库类型
[文库类型](https://salmon.readthedocs.io/en/latest/library_type.html)`--libType`，文库类型字符串由三部分组成：read的相对方向、文库的链特异性和read的方向性。
  - 仅当文库为双端文库时，才会提供文库字符串的第一部分（相对方向）。选项包括:
    ```bash
    I = inward
    O = outward
    M = matching
    ```
  - 文库类型第二部分是链的方向性，是链特异性还是链非特异性。选项包括：
    ```bash
    S = stranded
    U = unstranded
    ```
  - 文库类型的第三部分是read的方向性
    如果文库是链非特异性建库，那么就不需要指定第三部分。链特异性建库需要指定。选项包括：
    ```bash
    F = read 1 (or single-end read) comes from the forward strand
    R = read 1 (or single-end read) comes from the reverse strand
    ```
  - 使用例子
    ```bash
    IU (an unstranded paired-end library where the reads face each other)
    SF (a stranded single-end protocol where the reads come from the forward strand)
    OSR (a stranded paired-end protocol where the reads face away from each other,
     read1 comes from reverse strand and read2 comes from the forward strand)
    ```
- meta
支持宏基因组转录本定量，使用`--meta` 参数。
    
### alignment-based mode
Salmon的比对模式，不需要建立索引，直接提供转录本文件和比对文件(SAM/BAM)就可以进行定量。

```bash
salmon quant -t transcripts_fasta --libType A --ont -a xxx.bam -o ./salmon_bulk
```

