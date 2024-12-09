## AGAT
NBIS sweden : Another Gtf/Gff Analysis Toolkit [source](https://github.com/NBISweden/AGAT)

### 安装

```bash
$ conda install bioconda::agat
$ conda install -c bioconda agat
```

### 自动给gff添加5'utr和3'utr

```bash
$ agat_sp_manage_UTRs.pl --ref input.gff --three --five -p --out output_with_utr.gff

```
