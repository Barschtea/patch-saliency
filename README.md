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
**load_model.ipynb** then can be utilized to load any checkpoints present in the /models/checkpoints folder and feed an image to it. <br>

To run the notebooke you need the packages listed in **requirements.txt**. <br>
**Make sure that your torch installation has the necessary cuda components, if you want utilize a GPU.**

There are two model architectures present in the notebooks: 

- **sparse** -> a smaller architecture with the bare minimum of parameters
- **rich** -> a slightly larger architecture that extracts more features from patches

The existing folder structure of the repository can be used to run the model with **little to no further setup required**. <br> <br>

While the folders themselves only contain exemplary data, you can easily place your own data and models inside, while only having to change the file names within in the scripts. <br> <br>

**Depending on script environment, some paths in the scripts may need to be changed.** <br> 
**They are marked by a "ATTENTION" comment within the script.** <br>

Sections that potentially need to be changed:
- The import section of the notebooks. (Specify data that should be loaded.)
- The epoch section of "train_model.ipynb". (Specify paths to save logs and checkpoints.)
- The "Loading the model weights" section of load_model.ipynb. (Specify which model / architecture to load)
- **"model_name" in the epoch section when training a new model** (Otherwise existing checkpoints might get overridden. 

If you want to import a model not present in /models/checkpoints you will have to modify the paths in the "Loading the model weights" section. 

Pre-trained model checkpoints for 1s and 3s heatmaps can be found here: <br>
https://osf.io/fnv9q/files/osfstorage

---


