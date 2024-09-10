## VCFtools 使用手册

vcftools 可以处理vcf/bcf文件，包括数据的过滤，格式转换，变异统计，比较。合并。
vcftools [github](https://vcftools.github.io/index.html)  
vcftools [ --vcf FILE | --gzvcf FILE | --bcf FILE] [ --out OUTPUT PREFIX ] [ FILTERING OPTIONS ] [ OUTPUT OPTIONS ]

# 输入参数

- --vcf
- --gvcf
- --bcf  

### 输出参数
- --out    输出前缀
- --stdout 标准输出，用于管道中
- --temp   临时文件


### 过滤参数
#### 1.根据位置过滤
- --chr, --not-chr 指定过滤选择的染色体，可以多次使用
- --from-bp INT, --to-bp 指定区域，需要配合--chr使用
- --positions FILE， --exclude-positions 接tab分割的多个坐标位置文件
- --bed FILE, --exclude-be 根据bed文件过滤
#### 2.根据指定ID位点过滤

