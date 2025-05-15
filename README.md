# capsid-eyes
***A pipeline for preprocessing and classifying Cryo-TEM Adeno Associated Virus capsid image data.***

This pipeline can be used for every step of the classification process from preprocessing your image data to training a CNN that distinguishes between capsids and debris. The pipline in this repo was used to train the model used in the Capsidize App, as seen [here](https://github.com/lcgutier/Capsidize). Capsidize was developed to provide an accessible and standardized method of titer measurements to aid in reducing the dosage requirements for gene therapy treatments. 

Here I will walk you though how to use the pipeline for preprocessing and training. For ease of use, some of the original code has been restructured for this repo and assembled into different notebooks. 

## Getting Started

### Step 1: Clone the Repo
```
git clone https://github.com/lcgutier/capsid-eyes.git
```
### Step 2: Navigate to the Main Directory
```
cd capsid-eyes
```
### Step 3: Set Up The Environment

You can set up the environment in 4 different ways: with the requirements.txt, the environment.yml, the environment.txt, or with the below command line prompts

#### Option 1: Set up env with the requirements.txt
```
conda create --name capsidize1_env python=3.9 
conda activate capsidize1_env
pip install -r requirements.txt
```
#### Option 2: Set up env with the environment.yml
```
conda env create -f environment.yml
conda activate capsidize1_env
```
#### Option 3: Set up env with the below command line prompts
```
conda create --name capsidize1_env --file environment.txt
conda activate capsidize1_env
```
#### Option 4: Set up env with the below command line prompts
```
conda create --name capsidize1_env python=3.9 
conda activate capsidize1_env
conda install -c conda-forge tensorflow
conda install -c conda-forge opencv
conda install scikit-learn
pip install git+https://github.com/facebookresearch/segment-anything.git
pip install torch
pip install torchvision
pip install matplotlib
pip install supervision
pip install opencv-rolling-ball
pip install numpy==1.24.4
pip install pandas
```
### Step 4: Download the Segment Anything Model Checkpoint
The Capsidize app uses the SAM to segment the objects in the images before classification. To use the source code for the Capsidize app you will need to download the **ViT-H SAM model**. This can be found on their github at the link below:

Information on the Segment Anything Model can be found here: https://github.com/facebookresearch/segment-anything

### Step 5: Open and Run the Notebooks
The notebooks have been named in order from notebook (nb) 0 to notebook 5, but can be run in any needed order. 

***Note: to use the notebooks you will need to change the paths to the files where you see***
```
your_path_here/
```
Below is a description of the notebooks included:

1) **nb0_Synthetic_Data_Creation.ipynb**

    This notebook can be used to create, display, and save synthetic capsid data.

2) **nb1_Normalize.ipynb**

    This notebook is used to normalize whole raw cryo TEM images and save them to a new file. 

3) **nb2_Segmenting.ipynb**

    Here you can use the Segment Anything Model to segment all objects in each of your normalized images and save those resulting annotations to a COCO style JSON file. Using Supervision you can also view the annotated images.

4) **nb3_Split_Data.ipynb**

    This is where you will create patches for later classification as well as split the data into training and testing sets. 

5) **nb4_Image_Analysis.ipynb**

    This notebook allows you to perform feature extraction using different methods and use those features for training a support vector machine, a decision tree, or a k-means classifier. 

6) **nb5_CNN.ipynb**

    This notebook used to train a Basic, leNet and AlexNet model.

    ***Note: Tensorflow-Metal is needed to run this notebook on mac M1 devices. It is not needed for the other notebooks in this repo***

### Optional: Here is the Recommended Folder Structure:

```
.
└── Cryo_Data/
    ├── JSON_annotations
    ├── Model_Checkpoints
    ├── Percent_Combinations/
    │   └── AAV_Image_Folders_Here
    ├── Preprocessed_Data/
    │   ├── Corrected_Images/
    │   │   └── Corrected_Image_Folders_Here
    │   ├── Patches/
    │   │   └── Patches_Image_Folders_Here
    │   └── Split_Data/
    │       └── Train_Test_Split_Folders_Here
    ├── Sam_annotations
    └── Synthetic_Data
```
