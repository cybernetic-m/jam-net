# JAM-net: a KAN-based Deep Neural Network for Pneumonia Detection in Chest X-Rays 

JAM-net (**Jacopo and Massimo Network**) is a deep neural network for pneumonia detection in **Chest X-Rays** [1]. It's based on **FA-net** [2] architecture and on **KAN (Kolmogorov–Arnold Networks)** [3].
In particular, it's composed by the "**Fuzzy Channel Selective Spatial Attention Module**" of the FA-net [2] and the KAN architecture [3] that substitute the MLP layer at the end.
![Alt Text](images/architecture.png)

# Installation
1. Clone the repository:  
 ```sh 
 git clone "https://github.com/cybernetic-m/cv-project.git"
 cd cv-project
 ```
# Project Structure 

```sh 
cv-project
├── README.md
├── images
│   ├── Filtering.jpg
│   ├── acc.png
│   ├── architecture.png
│   ├── cm.png
│   ├── data_aug.jpg
│   ├── loss.png
│   ├── resizing.jpg
│   └── tab_no_prep.png
├── models
│   ├── jam_net_gaussian.pt => Trained model in Gaussian preprocessing
│   ├── jam_net_gaussian_he.pt => Trained model in Gaussian+He preprocessing
│   └── jam_net_noprep.pt => Trained model without preprocessing
├── notebook
│   ├── notebook_FA_exam.ipynb => Notebook python that implement FA-net training
│   └── notebook_JAM_exam.ipynb => Notebook python that implement JAM-net training
└── references
    ├── A_Deep_Feature_Learning_Model .pdf
    ├── KAN- Kolmogorov-Arnold Networks.pdf
    ├── SOTA_chest_ray.pdf
    └── fa_net.pdf
```
    
# Dataset
For the training phase, we have used the [Kermany dataset](https://data.mendeley.com/datasets/rscbjbr9sj/2). It's formed by **5856** chest X-Rays images divided in “**Normal**” and “**Pneumonia**” classes.
The images are of different sized and the dataset is unbalanced, for this reason the code firstly resize the image and after augment the dataset.

![Alt Text](images/resizing.jpg)
![Alt Text](images/data_aug.jpg)

# Filtering
As in the literature [1], we have performed a preprocessing operation on images applying **Gaussian**, **Gaussian + Histogram Equalization** filtering and **Colormap** application to the images.
![Alt Text](images/Filtering.jpg)

# Results
The training of the network is done with a **batch_size=48**, **early_stopping** monitoring the validation loss with a **threshold = 1e-4** and a **patience = 2**, the optimizer is **AdamW** with a **lr = 0.0001** and finally the loss function is the **Binary Cross Entropy Loss**. The metrics that we measure to validate the model are **Accuracy**, **Precision**, **Recall**, **AUROC** and **F1-Score**. We compare the results with the SOTA model [2] without preprocessing:

**Performances comparison**

<img src="images/tab_no_prep.png" alt="Alt Text" width="300">


**Confusion Matrix**

<img src="images/cm.png" alt="Alt Text" width="400">


**Loss Function**

<img src="images/loss.png" alt="Alt Text" width="400">


**Accuracy**

<img src="images/acc.png" alt="Alt Text" width="400">


# References
[1]. [Review on chest pathogies detection systems using deep learning techniques](https://link.springer.com/article/10.1007/s10462-023-10457-9#Abs1).

[2]. [FA-Net: A Fuzzy Attention-aided Deep Neural Network for Pneumonia Detection in Chest X-Rays](https://arxiv.org/pdf/2406.15117).

[3]. [KAN: Kolmogorov–Arnold Networks](https://arxiv.org/pdf/2404.19756).
