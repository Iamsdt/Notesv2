1. Install Miniconda

```bash
mkdir -p ~/miniconda3
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh
bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
rm ~/miniconda3/miniconda.sh
```

Load `conda init --all` and update `source ~/miniconda3/bin/activate`

Install Jupyter Notebook:
```
conda install -c conda-forge jupyterlab
```

Install nbgrader
```
conda install -c conda-forge nbgrader
```