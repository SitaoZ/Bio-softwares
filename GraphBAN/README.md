## GraphBAN
[GraphBAN](https://github.com/HamidHadipour/GraphBAN)


## Install 
```bash
# create a new conda environment
$ conda create --name graphban python=3.11
$ conda activate graphban

# install requried python dependencies
$ conda install pytorch==1.7.1 torchvision==0.8.2 torchaudio==0.7.2 cudatoolkit=10.2 -c pytorch
$ conda install -c dglteam dgl-cuda10.2==0.7.1
$ conda install -c conda-forge rdkit==2022.09.5
$ pip install dgllife==0.2.8
$ pip install -U scikit-learn
$ pip install yacs
$ pip install transformers
$ pip install pyarrow

# clone the source code of GraphBAN
$ git clone https://github.com/HamidHadipour/GraphBAN
$ cd GraphBAN
```
