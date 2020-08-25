# 3D-Pokemon-Generator

## Introduction

This is the final project of the computer vision course, 蔡政倫, 李意筑 and I improved and trained a generative-adversarial model [1], which can produce whole new Pokémons.

Based on code of [simple-pytorch-3dgan](https://github.com/xchhuang/simple-pytorch-3dgan), we implemented three kinds of models, 3D-GAN, Info-3D-GAN and 3D-VAE-GAN, as different Pokémon generators, which could randomly creates new Pokémon 3D models.

### Prerequisites

* Python 3.6.5 | Anaconda
* Pytorch 0.4.1
* tensorboardX
* visdom (optional)

### Folder structure (TBC)
```
.
├── src                     # Source files (alternatively `lib` or `app`)
├── results                    # Automated tests (alternatively `spec` or `tests`)
└── README.md
```
In `src`
```
main.py                     # maintains parameters and runs trainer()/tester()
trainer.py                  # define training process
model.py                    # define models
```

## Data
From Pokémon 3D model website, we convert DAE- format model files into 70× 70× 70 voxel cubes represented by 3D tensors with binary values.

![data_preprocessing](/images/data_preprocessing.png)

## Models

### 3D-GAN
We use the generator G of 3D-GAN to map the latent variable z to 3D voxel G(z) in 3D voxel space. The discriminator D outputs a confidence value D(x) of whether a 3D object input x is real or synthetic.

![3d_gan](/images/3d_gan.png)

### Info-3D-GAN
To control the characteristics of Pokémons, we use a Q network to improve the relationship between outputs of the generator and the fix latent variable c.

![info_3d_gan](/images/info_3d_gan.png)

### 3D-VAE-GAN
We add an image encoder to the generator, which is also the decoder, to enable further applications: latent variables z can be generated from images instead of noise.

![3d_vae_gan](/images/3d_vae_gan.png)

## Results
### 3D-GAN
Our model has learnt some specific structures and can generate something different as shown below.

![r_origin_exist](/images/r_origin_exist.png)

![r_origin_new](/images/r_origin_new.png)

### Info-3D-GAN
Fixed c can control distinct features, such as 4 legs and wings.

![r_info](/images/r_info.png)

### 3D-VAE-GAN
Put an image and the model generates 3D model according to the image.

![r_vae](/images/r_vae.png)

## Reference
1.  Jiajun Wu, Chengkai Zhang, Tianfan Xue, William T. Freeman and Joshua B. Tenenbaum. Learning a Probabilistic Latent Space of Object Shapes via 3D Generative-Adversarial Modeling.

### Data resource
1. The Models resource, at least 300 Pokémon’s 3D models, DAE file format: 
https://www.models-resource.com/3ds/pokemonxy/
2. Online Mesh Converter, DAE ⇒ OBJ
https://www.meshconvert.com
3. Online Voxelizer,  OBJ ⇒ voxel in python
http://drububu.com/miscellaneous/voxelizer