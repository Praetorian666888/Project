## Prerequisites
Code is intended to work with ```Python 3.6.x```,  it hasn't been tested with previous versions

## [PyTorch & torchvision](http://pytorch.org/)
Follow the instructions in [pytorch.org](http://pytorch.org) for your current setup

## Data preparation
### 1. Dataset directory structure
You will need to prepare your dataset in the following directory structure:

    ..
    ├── datasets                   
    |   ├── <dataset_name>         # i.e. train; validation; cluster; CAM
    |   |   ├── pat-id             # Patients' id
    |   |   |   ├── slide-id       # Slides' id
    |   |   |   |   └── 10         # Magnification-10X
    |   |   |   |   └── 20         # Magnification-20X
    |   |   |   |   └── n          # Magnification-nX
	
#### 2. WSIs images
All the images (patches) of different magnification will save as .jpeg

#### 3. Data labels
You will need to make the labels of dataset in the following json structure:

{
	"Pat-id-1": {"patient-label": 1},
	"Pat-id-2": {"patient-label": 0}
}

The id of the first patient is "Pat-id-1" and label is 1

## Training
```
cd Module1-Training
sh MILTrain.sh
```
This command will start training the WSIs data under the path set in .sh file "--path" parameter on GPUs. In each epoch of the training processing, all the model weights will be saved under the new created address model saving directory.

In the .sh file, you are able to setup the hyper-parameters of training like the number of epoch, feature extraction model etc.

## Testing
```
cd Module2-Evaluation
sh MILEval.sh
```
This command will start testing the WSIs data under the path set in .sh file "--path" parameter on GPUs. This script will also save the original prediction value as .csv file after testing.

## Clustering
Please follow the source implement in (https://github.com/sKamiJ/DCCS) for details in code.
Please follow the source paper in:
@inproceedings{zhao2020deep,
  title={Deep Image Clustering with Category-Style Representation},
  author={Zhao, Junjie and Lu, Donghuan and Ma, Kai and Zhang, Yu and Zheng, Yefeng},
  booktitle={European Conference on Computer Vision (ECCV)},
  year={2020}
}
for details in algorithm.
```
cd Module3-Clustering
sh Cluster.sh
```
This command will start clustering on the patch images under the path that "--dataset-path" have set. After clustering, it will save both cluster model and images classified by the cluster model. You are able to adjust the number of clusters by changing "--dim-zc" parameter. 

## Grad-CAM
```
cd Module4-CAM
sh CAM_all.sh
```
This commend will start drawing the CAM map of patch images.
