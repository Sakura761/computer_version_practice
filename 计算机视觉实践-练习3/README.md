# 图像超分



## 结果

|low-resolution|high-resolution|
|:--:|:--:|
|<img src="https://raw.githubusercontent.com/learner-lu/picbed/master/QQ%E6%88%AA%E5%9B%BE20220112003016.png">|<img src = "https://raw.githubusercontent.com/learner-lu/picbed/master/2.png">|

## Requirements

- pytorch

- ```shell
  pip install -r requirements.txt
  ```
  
## Use

### Step1: Prepare the dataset

  download the standard dataset
  The 91-image(train set), Set5(test set) dataset converted to HDF5 can be downloaded from the links below.
  | Dataset | Scale | Type | Link |
  |---------|-------|------|------|
  | 91-image | 2 | Train | [Download](https://github.com/learner-lu/image-super-resolution/releases/download/v0.0.1/91-image_x2.h5) |
  | 91-image | 3 | Train | [Download](https://github.com/learner-lu/image-super-resolution/releases/download/v0.0.1/91-image_x3.h5) |
  | 91-image | 4 | Train | [Download](https://github.com/learner-lu/image-super-resolution/releases/download/v0.0.1/91-image_x4.h5) |
  | Set5 | 2 | Eval | [Download](https://github.com/learner-lu/image-super-resolution/releases/download/v0.0.1/Set5_x2.h5) |
  | Set5 | 3 | Eval | [Download](https://github.com/learner-lu/image-super-resolution/releases/download/v0.0.1/Set5_x3.h5) |
  | Set5 | 4 | Eval | [Download](https://github.com/learner-lu/image-super-resolution/releases/download/v0.0.1/Set5_x4.h5) |

  Download any one of 91-image and Set5 in the same Scale and then **move them under `./datasets` as `./datasets/91-image_x2.h5` and `./datasets/Set5_x2.h5`**

### Step2: Train the model

- easy run

  ```python
  python train.py
  ```

- about arguments
  - `train-file` `eval-file` 2/3/4, different datasets to choose
  - `batch-size`
  - `num-workers`
  - `lr` learning rate
  - `epoch`
  - `f` frequency to test the model
  - `model-dir` where the model was saved

  ```python
  python train.py --train-file 4 --eval-file 4 --batch-size 64 --lr 1e-5 --num-workers 8 --epoch 500 --f 10 
  ```

  All model will be saved under `./model` and the best model is `./model/best.pth`

### Step3: Download the pretrained model(**If you have trained your model, skip this part)

- [trained by x2](https://github.com/learner-lu/image-super-resolution/releases/download/v0.0.1/b.pth)
- [trained by x4](https://github.com/learner-lu/image-super-resolution/releases/download/v0.0.1/best.pth)

**Move the model weights under `./model` as `./model/best.pth` or `./model/b.pth`**

### Step4: Do super resolution

```python
python use.py --weights-file ./model/best.pth --image x/xx/xxx.jpg
```

By default, the weights file is `./model/best.pth`, if you want to use `b.pth` please replace it.
A picture will be created named as `xxx_srcnn.jpg`

输出后的结果将放在output文件夹下
