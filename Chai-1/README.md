## Chai-1

Chai-1: Decoding the molecular interactions of life.
[Chai-1](https://www.chaidiscovery.com/) enables unified prediction of proteins, small molecules, DNA, RNA, covalent modifications, and more.

### Install 

```bash
conda create -n Chai1
conda activate Chai1

conda install python=3.13
# rdkit-2024.09.6, 注意安装的软件和python版本的适配关系，python版本对了，
# 安装特定的软件比较快，查询对应关系可以去conda 上查看Files中软件与python的对应
conda install conda-forge::rdkit

# 解决下面的报错后，再进行安装
pip install chai_lab==0.6.1
```

- 报错1: GCC 版本太低
```bash
# meson.build:28:4: ERROR: Problem encountered: NumPy requires GCC >= 8.4
# gcc 14.2.0
conda install conda-forge::gcc
```

- 报错2：C++编译器
```bash
# ERROR: C++ Compiler does not support -std=c++17
# cxx-compiler 1.9.0
conda install conda-forge::cxx-compiler
```

- 报错3：kalign

```bash
# 使用--use-msa-server --use-templates-server提高模型的表现
# AssertionError: kalign is required for templates, but was not found in PATH. Try 'apt install kalign'?
conda install bioconda::kalign3
```
### Usage

```bash
chai-lab --help

Usage: chai-lab [OPTIONS] COMMAND [ARGS]...

Options:
  --install-completion [bash|zsh|fish|powershell|pwsh]
                                  Install completion for the specified shell.
  --show-completion [bash|zsh|fish|powershell|pwsh]
                                  Show completion for the specified shell, to
                                  copy it or customize the installation.
  --help                          Show this message and exit.

Commands:
  fold        Run Chai-1 to fold a complex.
  a3m-to-pqt  Convert all a3m files in a directory for a *single...
  citation    Print citation information

```


- fold
```bash
chai-lab fold --help

Usage: chai-lab fold [OPTIONS] FASTA_FILE OUTPUT_DIR

  Run Chai-1 to fold a complex.

Arguments:
  FASTA_FILE  [required]
  OUTPUT_DIR  [required]

Options:
  --use-esm-embeddings / --no-use-esm-embeddings
                                  [default: use-esm-embeddings]
  --use-msa-server / --no-use-msa-server
                                  [default: no-use-msa-server]
  --msa-server-url TEXT           [default: https://api.colabfold.com]
  --msa-directory PATH
  --constraint-path PATH
  --use-templates-server / --no-use-templates-server
                                  [default: no-use-templates-server]
  --template-hits-path PATH
  --recycle-msa-subsample INTEGER
                                  [default: 0]
  --num-trunk-recycles INTEGER    [default: 3]
  --num-diffn-timesteps INTEGER   [default: 200]
  --num-diffn-samples INTEGER     [default: 5]
  --num-trunk-samples INTEGER     [default: 1]
  --seed INTEGER
  --device TEXT
  --low-memory / --no-low-memory  [default: low-memory]
  --help                          Show this message and exit.

```

- 例子
```bash
# 注意输入fasta文件的格式：protein, ligand, rna, dna, glycan
cat input.fasta
>protein|name=HMGCR
MLSRLFRMHGLFVASHPWEVIVGTVTLTICMMSMNMFTGNNKICGWNYECPKFEEDVLSSDIIILTITRCIAILYIYFQFQNLRQLGSKYILGIAGLFTIFSSFVFSTVVIHFLDKELTGLNEALPFFLLLIDLSRASTLAKFALSSNSQDEVRENIARGMAILGPTFTLDALVECLVIGVGTMSGVRQLEIMCCFGCMSVLANYFVFMTFFPACVSLVLELSRESREGRPIWQLSHFARVLEEEENKPNPVTQRVKMIMSLGLVLVHAHSRWIADPSPQNSTADTSKVSLGLDENVSKRIEPSVSLWQFYLSKMISMDIEQVITLSLALLLAVKYIFFEQTETESTLSLKNPITSPVVTQKKVPDNCCRREPMLVRNNQKCDSVEEETGINRERKVEVIKPLVAETDTPNRATFVVGNSSLLDTSSVLVTQEPEIELPREPRPNEECLQILGNAEKGAKFLSDAEIIQLVNAKHIPAYKLETLMETHERGVSIRRQLLSKKLSEPSSLQYLPYRDYNYSLVMGACCENVIGYMPIPVGVAGPLCLDEKEFQVPMATTEGCLVASTNRGCRAIGLGGGASSRVLADGMTRGPVVRLPRACDSAEVKAWLETSEGFAVIKEAFDSTSRFARLQKLHTSIAGRNLYIRFQSRSGDAMGMNMISKGTEKALSKLHEYFPEMQILAVSGNYCTDKKPAAINWIEGRGKSVVCEAVIPAKVVREVLKTTTEAMIEVNINKNLVGSAMAGSIGGYNAHAANIVTAIYIACGQDAAQNVGSSNCITLMEASGPTNEDLYISCTMPSIEIGTVGGGTNLLPQQACLQMLGVQGACKDNPGENARQLARIVCGTVMAGELSLMAALAAGHLVKSHMIHNRSKINLQDLQGACTKKTA

chai-lab fold input.fasta output_folder
```

```bash
# 使用MSAs  提高模型表现
chai-lab fold --use-msa-server --use-templates-server input.fasta output_folder
```
