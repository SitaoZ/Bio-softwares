## Rvtests

Rare variant tests


## 下载

```bash
# 下载仓库的代码，使用make安装可能会存在问题
git clone https://github.com/zhanxw/rvtests

# 解决方案是直接下载可执行程序
https://github.com/zhanxw/rvtests/releases

```

## 快速测试

```bash
rvtest --inVcf input.vcf --pheno phenotype.ped --out output --single wald,score
```
- 表型文件是`ped`格式（PLINK format）；对于有无的二元性状使用case=2,control=1,缺失表型为0或者-9

### 分组测试 (groupwise tests)
分组测试包括三种主要的测试：  
- 压力测试  
这些变异通常是小于1%或者5%的稀有变异，类别包括，`CMC test`, `Zeggini test`, `Madsen-Browning test`, `CMAT test`, `rare-cover test`

- 变量阈值测试  
使用不同的频率阈值下的类别变量

- 核方法  
适用于测试具有不同方向效应的罕见变异。这些包括`SKAT test`和`KBAC test`

上面所有的测试都需要将分组变异看成一个整体， 最简单的方法是将同一个基因的看成一个类别

```bash
rvtest --inVcf input.vcf --pheno phenotype.ped --out output --geneFile refFlat_hg19.txt.gz --burden cmc --vt price --kernel skat,kbac
# --geneFile 使用refFlat格式指定基因区间
# --gene 指定特定的基因 e.g. --gene CFH,ARMS2
# 如果没有指定--gene, 则全部的基因都会用于检验
```

### 关联个体检验（related individual tests）
为了测试有关联的个体，首先需要计算亲缘关系矩阵`kinship matrix`
```bash
vcf2kinship --inVcf input.vcf --bn --out output

# --bn : 表示使用 Balding-Nicols 方法计算经验亲属关系
# --ibs : 使用IBS亲缘关系矩阵
# --pedigree input.ped : 使用已知的pedigree计算亲缘关系矩阵

rvtest --inVcf input.vcf --pheno phenotype.ped --out output --kinship output.kinship --single famScore,famLRT,famGrammarGamma
# 计算完亲缘关系后再进行关联分析
```

### 荟萃分析（Meta-analysis）
meta-analysis模型输出的关联分析结果和基因型协方差矩阵

```bash
rvtest --inVcf input.vcf --pheno phenotype.ped --meta score,cov --out output
```

```bash
rvtest --inVcf input.vcf --pheno phenotype.ped --covar example.covar --covar-name age,bmi --inverseNormal --useResidualAsPhenotype  --meta score,cov --out output
# --covar : 指定特定的协方差文件
# --covar-name : 指定那个协方差用于分析
```

### 表型文建 Phenotype file 

```bash
fid iid fatid matid sex y1 y2 y3 y4
P1 P1 0 0 0 1.7642934435605 -0.733862638327895 -0.980843608339726 2
P2 P2 0 0 0 0.457111744989746 0.623297281416372 -2.24266162284447 1
P3 P3 0 0 0 0.566689682543218 1.44136462889459 -1.6490100777089 1
P4 P4 0 0 0 0.350528353203767 -1.79533911725537 -1.11916876241804 1
P5 P5 0 0 1 2.72675074738545 -1.05487747371158 -0.33586430010589 2
```
使用`--pheno`指定表型文件，  
使用`--mpheno` 和 `--pheno-name` 指定特定的性状, 
`--mpheno指定特定的列编号`，`--pheno-name` 指定特定的列名。  
默认的表型文件的列名为`y1`，如果你想指定特定的列名，例如使用`y2`，可以使用下面两种方法

- --mpheno 2
- --pheno-name y2

**注意**，使用`--pheno-name`,头文件一定是PLINK要求的`fid iid`开头

在表型文件中，缺失值使用NA或者非零的值。有缺失值的个体在后续的关联分析中会被丢弃。对于每个缺失的表型值，warning信息会被记录在log文件中。
如果表型文件是0,1,2, rvtests会自动将他看做二元性状（binary traits）, 但是，如果你想它们被看做连续性状，则需要指定`--qtl`参数。
### 协方差文件格式 covariate file 
可以使用--covar和--covar-name指定特定的协方差用于单个变异的关联分析，这是可选参数，如果你的数据中没有协变量，这个参数将会被忽略。
协变量文件如下所示，`example.covar`和表型文件格式类似。

```bash
fid iid fatid matid sex y1 y2 y3 y4
P1 P1 0 0 0 1.911 -1.465 -0.817 1
P2 P2 0 0 0 2.146 -2.451 -0.178 2
P3 P3 0 0 0 1.086 -1.194 -0.899 1
P4 P4 0 0 0 0.704 -1.052 -0.237 1
P5 P5 0 0 1 2.512 -3.085 -2.579 1
```
正对上面的协方差文件，我们使用`--covar`指定`--covar example.covar`,指定特定的协变量我们需要使用`--covar-name`,这里指定年龄，bmi和三个主成分用于关联分析。
具体参数如下：`--covar example.covar --covar-name age,bmi,pc1,pc2,pc3`


### 性状转化 Trait transformation 
