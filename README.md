# patch-saliency
This repository is part of the 2025-2026 run of the module "Human-Computer Interfaces" at the university of Leipzig, taught by Patrick Ebel.
The main goal of the project was to explore resolution independent saliency analysis. <br> <br>

Many existing models use one of the following mechanisms to combat differing resolutions in training data: <br>

- upscaling
- downscaling
- large-scale padding

This model explores a patching approach that utilizes minimal padding to cut each image into a varrying amount of patches. 
The patches are fed through a vision-transformer-like architecture consisting of: <br>

- a CNN-encoder
- a transformer encoder
- a linear decoder

It utilizes the cross-attention of the transformer as well as the global context of a cls token predict the heatmap of a patch. 
In a final step all patches are reconcatinated to form the final output-image.

This way this model is able to take input images of any size. <br>

The training of this model utilzied teh UEyes dataset available under: <br>
https://github.com/YueJiang-nj/UEyes-CHI2023

---

## Code:

The project consists mainly of two jupyter notebooks. <br> <br>
**train_model.ipynb** can be used to train a model of sparse architecture on the images present in dataset. <br> <br>
**load_mdoel.ipynb** then can be utilized to load any checkpoints present in the /models/checkpoints folder and feed an image to it. <br>

There are two model architectures present in the notebooks: 

- **sparse** -> a smaller architecture with the bare minimum of parameters
- **rich** -> a slightly larger architecture that extracts more features from patches

The existing folder structure of the repository can be used to run the model with **little to no further setup required**. <br> <br>

While the folders themselves only contain exemplary data, you can easily place your own data and models inside while only having change the file names within in the scripts. <br> <br>

If you want to try the model on data not present in the folder structure you will have to modify the paths in the import section of the notebooks. <br> <br>
If you want to save logs or checkpoints from training in a different place you will have to modify the paths in the epoch section of "train_model.ipynb". <br> <br>
**(It is advised to change the variable "model_name" in the epoch section when training a new model as the training would otherwise overwrite model data of the same name.)** <br> 

To run an image through the model you will have to execute the last block of **load_model.ipynb**.
The function needs a pre-existing model of sparse or rich architecture to be loaded in and handed over. <br> <br>
If you want to import a model not present in /models/checkpoints you will have to modify the paths in the "Loading the model weights" section. <br>

Pre-trained model checkpoints for 1s and 3s heatmaps can be found here: <br>
https://osf.io/fnv9q/files/osfstorage

---


