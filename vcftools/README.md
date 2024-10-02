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
- --chr <chromosome> , --not-chr <chromosome> 指定过滤选择的染色体，可以多次使用
- --from-bp <integer>, --to-bp <integer>      指定区域，需要配合--chr使用
- --positions <filename>, --exclude-positions <filename> 接tab分割的多个坐标位置文件
- --bed <filename> , --exclude-bed <filename>            根据bed文件过滤

#### 2.根据指定ID位点过滤
- --snp <string> 根据VCF文件的第三列ID的snp名进行过滤
- --snps <filename>, --exclude <filename> 根据ID文件进行过滤
 
#### 3.变异类型过滤
- --keep-only-indels 保留INDEL
- --remove-indels    保留SNP

#### 4.根据VCF文件的第七列FILTER进行过滤
- --remove-filtered-all 保留FILTER列为PASS的位点
- --keep-filtered, --remove-filtered 保留或去除特定的FILTER标签，可多次使用

#### 5.根据VCF文件第八列INFO进行过滤
- --keep-INFO
- --remove-INFO 根据INFO列的指定tag进行过滤

#### 6.根据ALLEL进行过滤
- --maf <float>, --max-maf <float> MinorAllele Frequency二等位基因频率进行过滤，常为--maf 0.05，即保留大于0.05的位点
- --non-ref-af <float>，--non-ref-ac <integer> 保留都是ALT变异的位点
- --mac <integer>, --max-mac <integer>         保留Minor Allel Count 数大于integer数的位点
- --min-alleles 2, --max-alleles 2             筛选保留含有2个ALT变异的位点，常用

#### 7.根据基因型GENOTYPE数据进行过滤
- --min-meanDP <float>, --max-meanDP <float>，根据平均覆盖深度进行过滤。-min-meanDP 3
- --hwe <float>         哈温平衡检测，根据pvalue值进行过滤，保留值以内的。--hwe 0.01
- --max-missing <float> 常用，缺失率，0为接受完全缺失，1位接受数据全都存在，一般为0.8
- --max-missing-count <integer> 缺失的个体数目超过integer，即被过滤
- --phase          删除unpased位点
- --minQ <integer> 保留Quality值大于integer的位点
#### 8.对样品个体进行过滤
- --idv <string>, --remove-idv <string>       保留/删除指定的样本
- --keep <filename>, --remove <filename>      保留/删除多个样本的文件
- --max-idv <integer> 随机保留integer数目的样本
#### 9.基因型过滤
- --remove-filtered-geno-all, --remove-filtered-geno <string> 删除FILTER FLAG的位点
- --minGQ <float> 删除GQ值低于数值的位点
- --minDP <float>, --maxDP <float> 保留覆盖率min~max之间的位点


### 计算统计参数
#### 1.输出变异位点的计算统计
- --freq, --freq2 输出每个等位基因的频率
- --counts, 位点数目的统计

#### 2.位点覆盖深度Depth统计
- --depth 输出每个个体的平均覆盖度， 以idepth文件展示
- --site-depth, --site-mean-depth 每个位点的所有个体深度
- --geno-depth 每个基因型的覆盖深度文件

#### 3. LD计算
- --hap-r2    
使用分型的单倍型输出报告 r^2、D 和 D'统计数据的文件。这些是群体遗传学文献中经常报道的 LD 的传统测量方法。输出文件的后缀为“.hap.ld”。此选项假定 VCF 输入文件具有定相单倍型。
- --geno-r2  
计算编码为0、1和2的基因型之间的平方相关系数，以表示每个个体中非参考等位基因的数量。这与 PLINK 报告的 LD 测量相同。 D 和 D' 统计数据仅适用于分阶段基因型。输出文件的后缀为“.geno.ld”。
- --geno-chisq  
如果你的数据包含具有两个以上等位基因的位点，则此选项可用于通过卡方统计来测试基因型独立性。输出文件的后缀为“.geno.chisq”。
- --hap-r2-positions <positions list file>, --geno-r2-positions <positions list file>  
输出一个文件，报告所提供文件中包含的位点相对于所有其他位点的r2统计信息。输出文件的后缀为“.list.hap.ld”或“.list.geno.ld”，具体取决于使用的选项。
- --ld-window <integer>, --ld-window-min <integer>   
LD计算的最大SNP数目，即LD-window。  --ld-window-min最小数目。
- --ld-window-bp <integer>,--ld-window-bp-min <integer>   
LD计算窗口的实际物理距离。
- --min-r2 <float>   
小于r2相关系数值将不被展示
- --interchrom-hap-r2, --interchrom-geno-r2   
跨染色体的r2值计算。

### 4. Ts/Tv计算 (Transition & Transversion)
- --TsTv <integer> 计算此选项定义的大小的窗口中的转换/颠换比率。仅使用双等位基因 SNP。生成的输出文件具有后缀“.TsTv”。
- --TsTv-summary   计算所有转换和颠换的简单摘要。输出文件的后缀为“.TsTv.summary”。
- --TsTv-by-count  计算作为替代等位基因计数函数的转换/颠换比率。仅使用双等位基因 SNP。生成的输出文件具有后缀“.TsTv.count”。
- --TsTv-by-qual   计算转换/颠换比率作为 SNP 质量阈值的函数。仅使用双等位基因 SNP。生成的输出文件具有后缀“.TsTv.qual”。
- --FILTER-summary 生成每个 FILTER 类别的 SNP 数量和 Ts/Tv 比率的摘要。输出文件的后缀为“.FILTER.summary”。

### 5. 核酸多样性统计 (Nucleotide divergence statistic)
- --site-pi
测量每个位点的核苷酸差异。输出文件的后缀为“.sites.pi”。
- --window-pi <integer>, --window-pi-step <integer>
测量窗口中的核苷酸多样性，提供的数字作为窗口大小。输出文件的后缀为“.windowed.pi”。后者是一个可选参数，用于指定窗口之间的步长。

### 6. FST 计算
- --weir-fst-pop <filename>  
此选项用于计算Weir和 Cockerham 1984 年论文中的 Fst 估计值。这是 Fst 的首选计算。提供的文件必须包含 VCF 文件中与一个群体相对应的个体列表（每行一个个体）。该选项可以多次使用来计算两个以上群体的 Fst。这些文件也将作为“--keep”选项包含在内。默认情况下，计算是基于每个站点进行的。输出文件的后缀为“.weir.fst”。
- --fst-window-size <integer>, --fst-window-step <integer>
这些选项可以与“--weir-fst-pop”一起使用，在窗口基础上而不是在每个站点基础上进行 Fst 计算。这些参数指定所需的窗口大小和窗口之间的所需步长。

### 7. 其他计算 (OUTPUT OTHER STATISTICS)
- --het
计算每个个体的杂合性度量。具体来说，使用矩量法估计每个个体的近交系数 F。生成的文件具有后缀“.het”。
- --hardy
报告Hardy-Weinberg平衡检验中每个位点的p值（由 Wigginton、Cutler 和 Abecasis (2005) 定义）。生成的文件（后缀为“.hwe”）还包含纯合子和杂合子的观察数以及 HWE 下相应的预期数。
- --TajimaD <integer>
在指定数量大小的箱中输出 Tajima 的 D 统计量。输出文件的后缀为“.Tajima.D”。
- --indv-freq-burden
此选项计算特定频率的每个个体内的变体数量。生成的文件具有后缀“.ifreqburden”。
- --LROH
此选项将识别并输出纯合性的计算。输出文件的后缀为“.LROH”。此函数是实验性的，如果应用于大型数据集，将使用大量内存。
- --relatedness
此选项用于根据Yang等人，Nature Genetics 2010 (doi:10.1038/ng.608) 的方法计算和输出相关性统计数据。具体来说，计算未调整的 Ajk 统计量。对于群体内的个体，Ajk 的期望为零，对于自身的个体，Ajk 的期望为 1。输出文件的后缀为“.relatedness”。
- --relatedness2
此选项用于根据 Manichaikul 等人，BIOINFORMATICS 2010 (doi:10.1093/bioinformatics/btq559) 的方法计算和输出相关性统计数据。输出文件的后缀为“.relatedness2”。
- --site-quality
生成包含每个位点 SNP 质量的文件，如 VCF 文件的 QUAL 列中所示。该文件的后缀为“.lqual”。
- --missing-indv
生成一个文件，报告每个人的缺失情况。该文件的后缀为“.imiss”。
- --missing-site
生成一个文件，报告每个站点的缺失情况。该文件的后缀为“.lmiss”。
- --SNPdensity <integer>
计算此选项定义的大小窗口中 SNP 的数量和密度。生成的输出文件具有后缀“.snpden”。
- --kept-sites
生成一个文件，列出过滤后保留的所有站点。该文件的后缀为“.kept.sites”。
- --removed-sites
生成一个文件，列出过滤后已删除的所有位点。该文件的后缀为“.removed.sites”。
- --singletons
此选项将生成一个文件，详细说明单例的位置以及它们出现的个体。该文件报告真正的单例和私有双例（即次要等位基因仅出现在单个个体中且该个体对该等位基因是纯合的 SNP） ）。输出文件的后缀为“.singletons”。
- --hist-indel-len
此选项将生成所有 indel（包括 SNP）长度的直方图文件。它显示输入文件中至少出现一次的 indel 长度的所有 indel 的计数和百分比。 SNP 被视为长度为零的插入缺失。输出文件的后缀为“.indel.hist”。
- --hapcount <BED file>
此选项将输出用户指定的窗口内唯一单倍型的数量，如 BED 文件所定义。输出文件的后缀为“.hapcount”。
- --mendel   <PED file>
此选项用于报告trios中识别的孟德尔错误。该命令需要 PLINK 样式的 PED 文件，前四列指定家庭 ID、孩子 ID、父亲 ID 和母亲 ID。该命令的输出具有后缀“.mendel”。
- --extract-FORMAT-info <string>
从 VCF 文件中与指定格式标识符相关的基因型字段中提取信息。生成的输出文件具有后缀“.<FORMAT_ID>.FORMAT”。例如，以下命令将提取所有 GT（即基因型）条目：`vcftools --vcf file1.vcf --extract-FORMAT-info GT`
- --get-INFO <string>
该选项用于从 VCF 文件中的 INFO 字段中提取信息。 <string> 参数指定要提取的 INFO 标记，并且可以多次使用该选项以提取多个 INFO 条目。生成的文件带有后缀“.INFO”，在制表符分隔的表中包含所需的 INFO 信息。例如，要提取 NS 和 DB 标志，可以使用以下命令：`vcftools --vcf file1.vcf --get-INFO NS --get-INFO DB`

### 8. 输出格式
- --recode, --recode-bcf
这些选项用于在应用用户指定的过滤选项后从输入 VCF 或 BCF 文件生成 VCF 或 BCF 格式的新文件。输出文件的后缀为“.recode.vcf”或“.recode.bcf”。默认情况下，INFO 字段将从输出文件中删除，因为 INFO 值可能会因重新编码而失效（例如，如果删除个体，则可能需要重新计算总深度）。此行为可能会被以下选项覆盖。默认情况下，BCF 文件被写为 BGZF 压缩文件。
- --recode-INFO <string>, --recode-INFO-all
这些选项可以与上述重新编码选项一起使用来定义要保留在输出文件中的 INFO 键名称。该选项可以多次使用以保留更多的 INFO 字段。第二个选项用于保留原始文件中的所有 INFO 值。
- --contig <string>
当输入文件没有任何 contig 声明时，此选项可以与 --recode-bcf 结合使用。此选项需要一个每行包含一个重叠群标头的文件名。这些行包含在输出文件中。

### 9. 格式转换
- --012  
此选项将基因型输出为大矩阵。生成三个文件。第一个带有后缀“.012”，在单独的行中包含每个个体的基因型。基因型表示为0、1 和 2，其中数字表示`非参考等位基因的数量`。缺失的基因型用-1表示。第二个文件的后缀为“.012.indv”，详细介绍了主文件中包含的个人。第三个文件的后缀为“.012.pos”，详细说明了主文件中包含的站点位置。

- --IMPUTE  
此选项以 IMPUTE 参考面板格式输出分阶段单倍型。由于 IMPUTE 需要分阶段数据，因此使用此选项也意味着 --phased。因此，未定相的个体和基因型被排除在外。输出中仅包含双等位基因位点。使用此选项会生成三个文件。 IMPUTE 单倍型文件具有后缀“.impute.hap”，IMPUTE 图例文件具有后缀“.impute.hap.legend”。第三个文件的后缀为“.impute.hap.indv”，详细介绍了单倍型文件中包含的个体，尽管 IMPUTE 不需要此文件。

- --ldhat
- --ldhat-geno  
这些选项以 LDhat 格式输出数据。此选项还需要使用“--chr”过滤器选项。第一个选项仅输出分阶段数据，因此也意味着使用“--phased”，导致排除非分阶段个体和基因型。第二个选项将所有数据视为非定相数据，因此以基因型/非定相格式输出 LDhat 文件。生成两个带有后缀“.ldhat.sites”和“.ldhat.locs”的输出文件，分别对应于 LDhat“sites”和“locs”输入文件。
