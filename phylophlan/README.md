## PhyloPhlAn

PhyloPhlAn is an integrated pipeline for large-scale phylogenetic profiling of genomes and metagenomes.

Most likely the easiest way to understand how you can use PhyloPhlAn in your analysis is to check out the examples in the PhyloPhlAn [tutorial](https://github.com/biobakery/biobakery/wiki/PhyloPhlAn3).


### 安装

```bash
conda install -c bioconda phylophlan
phylophlan --version

```

### 基本使用
```bash 
phylophlan -i <input_folder> \
    -d <database> \
    --diversity <low-medium-high> \
    -f <configuration_file>

```
- input_folder
<input_folder> is the folder containing your input genomes and/or proteomes, a detailed description is available here.
PhyloPhlAn 3 takes FASTA files (also compressed in Gzip, .gz and/or Bzip2, .bz2) as input. Inputs can be both genomes and proteomes, also mixed, and by default genomes and proteomes are distinguished by the .fna and .faa extension, respectively.

If needed, genomes and proteomes file extensions can be specified using the --genome_extension and --proteome_extension params, respectively.



- database  
<database> is the name of the database of markers to use, a detailed description is available here.
PhyloPhlAn 3 is able to automatically download two databases of universal markers for prokaryotes:

PhyloPhlAn (-d phylophlan, 400 universal marker genes) presented in Segata, N et al. NatComm 4:2304 (2013)
AMPHORA2 (-d amphora2, 136 universal marker genes) presented in Wu M, Scott AJ Bioinformatics 28.7 (2012)
Moreover, in addition to the two databases provided, as explained in the following database setup section, it is possible to retrieve a set of core proteins of a specific species, or even build custom databases starting from either a folder containing marker files or a multi-fasta file containing the marker sequences (e.g., multi-fasta file with the core genes sequences from Roary).

- diversity  
--diversity takes value in {low, medium, high} and it's used to automatically set the analysis to the type of phylogeny to build, a detailed description is available here
  
- configure_file
<configuration_file> is the path to the configuration file necessary to properly run PhyloPhlAn 3, a detailed description is available here
