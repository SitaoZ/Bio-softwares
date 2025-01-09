## Pear
[Pear](https://github.com/tseemann/PEAR) 用于合并双端测序的两条read合并，原理是使用forward和reverse read的重叠区域进行合并。


## 安装 
```bash
https://anaconda.org/bioconda/pear
conda install bioconda::pear
```
## 使用
PEAR  can  robustly  assemble most of the data sets with default parameters. The
basic command to run PEAR is

```bash
pear -f forward_read.fastq -r reverse_read.fastq -o output_prefix
```
The forward_read file usually has "R1" in the name, and the reverse_read
file usually has "R2" in the name.

## 输出文件 
PEAR 生成 4 输出文件:

1. output_prefix.assembled.fastq - the assembled pairs
2. output_prefix.unassembled.forward.fastq - unassembled forward reads
3. output_prefix.unassembled.reverse.fastq - unassembled reverse reads
4. output_prefix.dicarded.fastq  - reads which did not meet criteria specified in options



## 注意

1. 输入文件必须为FASTQ format
2. PEAR  不检查paired-end reade 的名称， PEAR假定输入paired文件是一一对应的，两个文件中的读段出现在相同的行号上，则它们位于相同的流动池位置


## Citation 

J. Zhang, K. Kobert, T. Flouri, A. Stamatakis. PEAR: A fast and accurate Illimuna Paired-End reAd mergeR (https://doi.org/10.1093/bioinformatics/btt593)
