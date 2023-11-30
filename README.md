# Prerequisites
### Software
+ Install python 3.9.12
+ Install packages
```
pip install -r requirements.txt 
```
+ Install pytorch
```
pip install torch==1.9.0+cu111 torchvision==0.10.0+cu111 torchaudio==0.9.0 -f https://download.pytorch.org/whl/torch_stable.html
```
### Hardware
+ ResNet50 (25M parameters), GPU momory >= 4GB is guaranteed work

# File structure
+ main.py # modes include train, valid, infer
+ utils.py # common utilities e.g. dataset, model, plot, etc.
+ training_set/training_set/ # dataset
    + cats/*.jpg
    + dogs/*.jpg
+ test_set/test_set/ # dataset
    + cats/*.jpg
    + dogs/*.jpg
+ save_models/ # auto-generated by main.py
    + exp1/
        + *.pt # trained model weights
+ save_results/ # auto-generated by main.py
    + exp1/
        + *_args.json # arguments
        + *_pred.csv # prediction results
        + *.jpg # result curve
        + train.json # training history 

Please download dataset from [here](https://www.kaggle.com/datasets/tongpython/cat-and-dog) 

# Quick start
### train
```
python main.py [--options]
```
arguments:
+ mode: 'train', 'valid' or 'infer'
+ batch-size: default=16
+ output-dim: default=2
    (for binary classification, you can set 1 and loss is BCE or set 2 and loss is CE)
+ resume: default='', load checkpoint path if specified
+ epochs: default=50
+ results: default="./results/exp1"
+ background-cls: default=0, num of bg-cls for concat last n to 1 column, metrics 
+ threshold-opt: threshold opt refers last col as bg (only do if has bg-cls and only in valid mode)

# More
+ Coding style: as precise and comprehensive as possible
+ Improvement than usual:
    + learning rate scheduler which is widely use in SOTA CV
    + more complete metrics
    + for improve image quality
        + output worst predicted images based on loss while validation
        + output worst predicted images based on max confidence while inference
+ Output prediction results for further post-analysis if needed.
+ Feel free to contact me if you have any question. Thanks.
