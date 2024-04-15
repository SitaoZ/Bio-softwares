## Cutadapt 
[Cutadapt](https://cutadapt.readthedocs.io/en/stable/installation.html) is a software tool designed to identify and eliminate adapter sequences, primers, poly-A tails, and other undesired sequences from high-throughput sequencing reads.
Cleaning your reads in the manner is frequently necessary due to specific reasons:
 - Small-RNA sequencing reads encompass the 3' sequencing adapter , as the read is longer than the sequenced molecule.
 - Amplicon reads initiate with a primer sequence.
 - Although ploy(A)tails are beneficial for extracting RNA from your sample, they are often unwanted in your reads.


### Trim a 3' adapter
- fastq/fasta
- gz/no-gz

```bash
cutadapt -a CTGTAGGCACCATCA -o SRR18079087_1.clean.fastq SRR18079087_1.fastq # compressed in and output are also supported
tail -n 4 SRR18079087_1.fastq | cutadapt -a CTGTAGGCACCATCA - > output.fastq  # - is input stream
```


### Adapter type 

| Adapter type | Command-line option |
| :---         |     :---:      |
| Regular 3’ adapter   | -a ADAPTER    |
| Regular 5’ adapter     | -g ADAPTER  |
| Non-internal 3’ adapter| -a ADAPTERX |
| Non-internal 5’ adapter| -g XADAPTER |
| Anchored 3’ adapter | -a ADAPTER$ |
| Anchored 5’ adapter | -g ^ADAPTER |
| 5’ or 3’ (both possible)| -b ADAPTER |
| Linked adapter | -a ^ADAPTER1...ADAPTER2 <br> -g ADAPTER1...ADAPTER2|


































