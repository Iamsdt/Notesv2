---
Created by: Shudipto Trafder
Created time: 2023-10-18T20:15
Last edited by: Shudipto Trafder
Last edited time: 2024-01-01T19:19
tags:
  - cloud
  - pytorch
---


# Deploy Pytorch Model with TorchServe

### Install TorchServe and torch-model-archiver

Clone TorchServe repo

```Plain
git clone <https://github.com/pytorch/serve.git>
```

1. Install dependencies

Note: For Conda, Python 3.8 is required to run Torchserve.

### For Debian Based Systems/ MacOS

- For CPU
    
    ```Plain
    python ./ts_scripts/install_dependencies.py
    ```
    
- For GPU with Cuda 10.2. Options are `cu92`, `cu101`, `cu102`, `cu111`, `cu113`
    
    ```Plain
    python ./ts_scripts/install_dependencies.py --cuda=cu116
    ```
    

Note: PyTorch 1.9+ will not support cu92 and cu101. So TorchServe only supports cu92 and cu101 up to PyTorch 1.8.1.

1. Install torchserve, torch-model-archiver and torch-workflow-archiver

```Plain
conda install torchserve torch-model-archiver torch-workflow-archiver -c pytorch
```

For Pip

```Plain
pip install torchserve torch-model-archiver torch-workflow-archiver
```

### Model Archiver

```Plain
torch-model-archiver --model-name "BertCvMain" --version 1.0 --handler "./scripts/bert_cv_main_model.py" --export-path model_store -f
```

Create torchserve.config file

```Plain
inference_address=http://0.0.0.0:7000
default_workers_per_model=1
initial_workers=1
```

Start torchserve

```Plain
torchserve --start --ncs --model-store ./model_store --models BertCvMain=BertCvMain.mar --ts-config torchserve.config 2>&1 >torchserve.log
```

## Restapi

```Plain
curl <http://127.0.0.1:7000/ping>
```

```Plain
curl -X OPTIONS <http://localhost:7000>
```

```Plain
/predictions/{model_name}/{model_version}

/predictions/{model_name}
```

```Plain
curl --header "Content-Type: application/json" \\
  --request POST \\
  --data '{"inputs": ["hey how are you", "yeah I am fine", "Thats ok, it's fine"]}' \\
  <http://127.0.0.1:7000/predictions/BertCvMain>
```

```Plain
<http://127.0.0.1:7000/predictions/BertCvMain>
```

# Stop

```Plain
torchserve --stop
```