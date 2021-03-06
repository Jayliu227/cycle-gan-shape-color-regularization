# Cycle-GAN with Shape-Color-Similarity Regularization

## Introduction

This project aims to figure out an effective method for constraining the generators and exploit the relationships between two unpaired image datasets based on the [CycleGAN paper](https://arxiv.org/pdf/1703.10593.pdf). Our approach is to add a new regularization term to the total loss, which penalizes the generators when the generated images G(X) or F(Y) have different shapes than the target images Y or X and the foreground colors are also different. For more details, please refer to the [paper](https://github.com/Jayliu227/cycle-gan-shape-color-regularization/blob/master/SCR.pdf). 

## Installation

Clone the repository
```
git clone https://github.com/Jayliu227/cycle-gan-shape-color-regularization.git
```
Download the pretrained model from [a-PyTorch-Tutorial-to-Object-Detection pretrained model](https://drive.google.com/file/d/1YZp2PUR1NYKPlBIVoVRO0Tg1ECDmrnC3/view)

Once finished, we can move the pretrained model into the directory 
```
mv BEST_checkpoint_ssd300.pth.tar cycle-gan-shape-color-regularization/src/object_detection/
```
Navigate into our repository and create two folders
```
cd cycle-gan-shape-color-regularization
mkdir output
mkdir save
mkdir data
```
where *output folder* is used to store the testing results of the model, *save folder* is used for storing the trained model, and *data folder* is the directory for the dataset

Dataset is organized as follows:
```
Data
    |---test <testing set>
        |---X <X image set>
        |---Y <Y image set>
    |---train <training set>
        |---X <X image set>
        |---Y <Y image set>
```
Overall project organization:
```
cycle-gan-shape-color-regularization
    |---data
        |---test <testing set>
            |---X <X image set>
            |---Y <Y image set>
        |---train <training set>
            |---X <X image set>
            |---Y <Y image set>
    |---save
        |---Dx.pth
        |---Dy.pth
        |---F.pth
        |---G.pth
    |---output
        |---X <generated from original Y set>
        |---Y <generated from original X set>
        |---recover <recovered image from x set>
    |---src
        |---object_detection
            |---BEST_checkpoint_ssd300.pth.tar <pretrained model>
        |---train.py
        |---test.py
        |---other utility scripts
```
Train model (in *model* folder)
```
python train.py
```
Test model (in *model* folder)
```
python test.py
```

For better and more stable experiments, it is recommened to test with the [source code](https://github.com/junyanz/pytorch-CycleGAN-and-pix2pix) provided by the author of the CycleGAN paper. Copy the *scripts* and *object_detection* folder to their repository and modify the loss function based on *train.py*.
