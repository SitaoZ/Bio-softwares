## Cell Ranger 

CellRanger是10X genomics开发用于单细胞测序数据分析的软件。Cell Ranger是一组分析管道，用于处理Chromium Next GEM单细胞数据，read比对生成特征条形码矩阵，聚类分析和其他二次分析等。Cell Ranger包括5个与3‘单细胞基因表达、5’免疫谱分析和Flex检测相关的管道：


- 下载安装

[下载网址](https://www.10xgenomics.com/support/software/cell-ranger/downloads)


```bash
wget -O cellranger-9.0.1.tar.gz "https://cf.10xgenomics.com/releases/cell-exp/cellranger-9.0.1.tar.gz?Expires=1751485501&Key-Pair-Id=APKAI7S6A5RYOXBWRPDA&Signature=giX06Yx6gK8Gf3BKO~sPhn6O6h3lomSNouh~oqZr05~QEmT9QEwYkcCHHwORNSoaF4bCDvN3G6hNh4yLUUd9lWceb1p3q9qBh2~BVWHVgQjG3YXpYCYfdOabzBjX9fXgNmoWB4GjeL62K4aLwCfQxl5RpqnS9BWw9DdLGndQrHgHDb2A10IJ-fLWSIlO8NfgmZMCPt5iX-1pkamvIhHLlLiWtqTC2R0mQjSwhokZ95ONwQxNFliimRKOizN5tOn3HlHWKZM12KvUoX4BqUiO~631P2S5jCAaJIeNY1~SA~0vgMqZb-MeYNPjQucK4wvlBOBeaxuK-yANVQ1LFLZkpw__"
```

```bash
cellranger -h

cellranger cellranger-9.0.1

Process 10x Genomics Gene Expression, Feature Barcode, and Immune Profiling data

Usage: cellranger <COMMAND>

Commands:
  count           Count gene expression and/or feature barcode reads from a single sample and GEM well
  multi           Analyze multiplexed data or combined gene expression/immune profiling/feature barcode data
  multi-template  Output a multi config CSV template
  vdj             Assembles single-cell VDJ receptor sequences from 10x Immune Profiling libraries
  aggr            Aggregate data from multiple Cell Ranger runs
  annotate        Annotate cell-types from outputs of a CellRanger run
  reanalyze       Re-run secondary analysis (dimensionality reduction, clustering, etc)
  mkvdjref        Prepare a reference for use with CellRanger VDJ
  mkfastq         Run Illumina demultiplexer on sample sheets that contain 10x-specific sample index sets
  testrun         Execute the 'count' pipeline on a small test dataset
  cloud           Invoke cloud commands
  mat2csv         Convert a feature-barcode matrix to CSV format
  mkref           Prepare a reference for use with 10x analysis software. Requires a GTF and FASTA
  mkgtf           Filter a GTF file by attribute prior to creating a 10x reference
  upload          Upload analysis logs to 10x Genomics support
  sitecheck       Collect Linux system configuration information
  telemetry       Configure and inspect telemetry settings and data
  help            Print this message or the help of the given subcommand(s)

Options:
  -h, --help     Print help
  -V, --version  Print version


```

- cellranger mkfastq 流程已弃用，并将在未来版本中移除。请使用 Illumina 的 BCL Convert 生成与 Cell Ranger 兼容的 FASTQ 文件。有关详细指导，请参阅生成 FASTQ 页面。


- **cellranger count**
count程序使用FASTQ文件进行比对，过滤，barcode计数，UMI计数。使用barcode构建特征矩阵，进而聚类，基因表达量分析。

- **cellranger multi**

- **cellranger vdj**
- **cellranger aggr**
- **cellranger reanalyze**
- **cellranger annotate**
- 
