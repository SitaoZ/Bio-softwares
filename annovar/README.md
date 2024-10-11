## Annovar 
Annovar 是一款高效的软件工具，用来对变异进行注释 [annovar paper](!https://academic.oup.com/nar/article/38/16/e164/1749458)。
Annovar可利用最新信息对从不同基因组（包括人类基因组 hg18、hg19、hg38、hs1 (T2T-CHM13) 以及小鼠、蠕虫、苍蝇、酵母等）中检测到的遗传变异进行功能注释。
给定一个包含染色体、起始位置、终止位置、参考核苷酸和观察到的核苷酸的变异列表，ANNOVAR 可以执行：

- 基于基因的注释   
确定 SNP 或 CNV 是否导致蛋白质编码变化以及受影响的氨基酸。用户可以灵活使用 RefSeq 基因、UCSC 基因、ENSEMBL 基因、GENCODE 基因、AceView 基因或许多其他基因定义系统。

- 基于区域的注释
识别特定基因组区域中的变异，例如，44 个物种中的保守区域、预测的转录因子结合位点、节段重复区域、GWAS 命中、基因组变异数据库、DNAse I 超敏位点、ENCODE H3K4Me1/H3K4Me3/H3K27Ac/CTCF 位点、ChIP-Seq 峰、RNA-Seq 峰或基因组间隔上的许多其他注释。

- 基于过滤器的注释
识别特定数据库中记录的变体，例如，变体是否在 dbSNP 中报告，1000 基因组计划、NHLBI-ESP 6500 外显子组或外显子组聚合联盟 (ExAC) 或基因组聚合数据库 (gnomAD) 中的等位基因频率是多少，计算 SIFT/PolyPhen/LRT/MutationTaster/MutationAssessor/FATHMM/MetaSVM/MetaLR 分数，查找 GERP++ 分数 <2 或 CADD>10 的基因间变体，或特定突变的许多其他注释。


