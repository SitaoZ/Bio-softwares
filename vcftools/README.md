## VCFtools 使用手册

vcftools 可以处理vcf/bcf文件，包括数据的过滤，格式转换，变异统计，比较，合并。
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
- --snp 根据VCF文件的第三列ID的snp名进行过滤
- --snps FILE, --exclude 根据ID文件进行过滤
 
#### 3.变异类型过滤
- --keep-only-indels 保留INDEL
- --remove-indels 保留SNP

#### 4.根据VCF文件的第七列FILTER进行过滤
- --remove-filtered-all 保留FILTER列为PASS的位点
- --keep-filtered, --remove-filtered 保留或去除特定的FILTER标签，可多次使用

#### 5.根据VCF文件第八列INFO进行过滤
- --keep-INFO
- --remove-INFO 根据INFO列的指定tag进行过滤

#### 6.根据ALLEL进行过滤
- --maf, --max-maf MinorAllele Frequency 二等位基因频率进行过滤，常为--maf 0.05，即保留大于0.05的位点
- --non-ref-af，--non-ref-ac 保留都是ALT变异的位点
- --mac INT, --max-mac 保留Minor Allel Count 数大于INT数的位点
- --min-alleles 2, --max-alleles 2 筛选保留含有2个ALT变异的位点，常用

#### 7.根据基因型GENOTYPE数据进行过滤
- --min-meanP, --max-meanDP，根据平均覆盖深度进行过滤。-min-meanDP 3
- --hwe 哈温平衡检测，根据pvalue值进行过滤，保留值以内的。--hwe 0.01
- --max-missing 常用，缺失率，0为接受完全缺失，1位接受数据全都存在，一般为0.8
- --max-missing-count INT 缺失的个体数目超过INT，即被过滤
- --phase 删除unpased位点
- --minQ INT 保留Quality值大于INT的位点
#### 8.对样品个体进行过滤
- --idv, --remove-idv 保留或删除指定的样本
- --keep FILE, --remove FILE 保留/删除多个样本的文件
- --max-idv INT 随机保留INT数目的样本
#### 9.基因型过滤
- --remove-filtered-geno-all, --remove-filtered-geno 保留、删除FILTER FLAG的位点
- --minGQ 删除GQ值低于数值的位点
- --minDP, --maxDP 保留覆盖率min~max之间的位点


### 计算统计参数
#### 1.输出变异位点的计算统计
- --freq, --freq2 输出每个等位基因的频率
- --counts, 位点数目的统计

#### 2.位点覆盖深度Depth统计
- depth 输出每个个体的平均覆盖度， 以idepth文件展示
- --site-depth, --site-mean-depth 每个位点的所有个体深度
- --geno-depth 每个基因型的覆盖深度文件

#### 3. LD计算
- --hap-r2 同时输出r^2值，D值和D'值
- --geno-r2 
  


