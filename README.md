# DSNet
# Dynamic Selection Network for Image Inpainting
## Requirements

scipy==1.1.0

numpy==1.16.2

torch==1.1.0

torchvision==0.3.0

imageio==2.9.0

Pillow==8.0.1

This is the environment for our experiments. Later versions of these packages might need a few modifications of the code.

## Pretrained Models

<!--
The link to the pretrained model. (Currently, Paris StreetView, CelebA datasets)

https://drive.google.com/drive/folders/1EbRSL6SlJqeMliT9qU8V5g0idJqvirZr?usp=sharing
-->

We strongly encourage the users to retrain the models if they are used for academic purpose, to ensure fair comparisons (which has been always desired). Achieving a good performance using the current version of code should not be difficult.


## Running the program

To perform training, fine-tune or testing, use 
```
sh train.sh

sh finetune.sh

sh test.sh 
```
There are several arguments that can be used, which are
```
--data_root +str #where to get the images for training/testing
--mask_root +str #where to get the masks for training/testing
--model_save_path +str #where to save the model during training
--result_save_path +str #where to save the inpainting results during testing
--model_path +str #the pretrained generator to use during training/testing
--target_size +int #the size of images and masks
--mask_mode +int #which kind of mask to be used, 0 for external masks with random order, 1 for randomly generated masks, 2 for external masks with fixed order 
 (It will be better to use mask_mode 2 during testing for fairness)
--batch_size +int #the size of mini-batch for training
--n_threads +int
--gpu_id +int #which gpu to use
--finetune #to finetune the model during training
--test #test the model
```
For example, to train the network using gpu 1, with pretrained models
```
python run.py --data_root data --mask_root mask --model_path checkpoints/g_10000.pth --batch_size 6 --gpu 1
```
to test the network
```
python run.py --data_root data/images --mask_root data/masks --model_path checkpoints/g_10000.pth --test --mask_mode 2
```

To fully exploit the performance of the network, we suggest to use the following training procedure, in specific

1. Train the network, i.e. use the command
```
python run.py
```

2. Finetune the network, i.e. use the command
```
python run.py --finetune --model_path path-to-trained-generator
```

3. Test the model
```
python run.py --test
```
## How long to train the model for

All the descriptions below are under the assumption that the size of mini-batch is 6

For Paris Street View Dataset, train the model for 400,000 iterations and finetune for 200,000 iterations. (600,000 in total)

For CelebA Dataset, train the model for 350,000 iterations and finetune for 150,000 iterations. (500,000 in total)

For Places2 Dataset, train the model for 2,000,000 iterations and finetune for 1,000,000 iterations. (3,000,000 in total)

<!--
## Improving the code
This code will be improved constantly. More functions for visualization are still to be developed.
-->

## Citation
If you find the article or code useful for your project, please refer to
```
@article{wang2021dynamic,
  title={Dynamic Selection Network for Image Inpainting},
  author={Wang, Ning and Zhang, Yipeng and Zhang, Lefei},
  journal={IEEE Transactions on Image Processing},
  volume={30},
  pages={1784--1798},
  year={2021},
  publisher={IEEE},
  doi={10.1109/TIP.2020.3048629}
}
```
## Paper
See the Paper folder
