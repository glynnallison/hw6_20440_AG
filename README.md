# PS6: Reproducible, shareable code
Allison Glynn \
*Updated: April 6, 2024*

### Overview.
This repository contains code, data, and figures pertaining to the project **"Comorbidity and exclusion of neurological disorders predicted by human gastrointestinal microbiome compositions"**. The contents of this repository detail (1) the code used for consolidating and cleaning 16S sequencing data into a pooled, informative dataset and (2) the code used to perform dimensionality reduction and clustering using a linear dimensionality reduction technique: principal component analysis (PCA), and a nonlinear dimensionality reduction technique that uses the reduced dataset produced by PCA: T-distributed Stochastic Neighbor Embedding (TSNE). The included data and code produce 2 SVGs of figures detailing the diagnoses in comparison to the first two principal components and to the two TSNE components. The pooled data consists of relative abundance 16S sequencing data from five neurological disorders: Autism spectrum disorder (ASD), Alzheimer's Disease (AD), Epilepsy, Multiple sclerosis (MS) and Parkinson's Disease (PD). The documentation for performing PCA in Python can be found [here](https://scikit-learn.org/stable/modules/generated/sklearn.decomposition.PCA.html). The documentation for performing TSNE analysis in Python can be found [here](https://scikit-learn.org/stable/modules/generated/sklearn.manifold.TSNE.html).

### Data.

The data was accessed from the Data Repository for Human Gut Microbiota ([GMrepo](https://gmrepo.humangut.info/home)), described in [this paper](https://academic.oup.com/nar/article/50/D1/D777/6426060?login=true). Documentation for this repository can be found [here](https://evolgeniusteam.github.io/gmrepodocumentation/). GMrepo curates, consolidates, cleans, quality controls, and normalizes publicly available human 16S sequencing data from multiple human microbiome studies. It consolidates data and provides relative abundance measurements for each run accessed from each study, making it ideal for this project as all runs are quality controlled and converted from raw measurements to relative abundance, making them comparable across study and disorder. These runs are annotated by phenotype, and so we take all quality controlled runs for a given phenotype (one of the five described in the Overview) and consolidate them into a pooled dataset. 

The dataset used in this project for analysis is the pooled dataset, called "20440_cleaned_data.csv" in the Data folder. It contains the run ID, the relative abundance of each bacterial species, and a diagnosis. Species that are found in some runs but not others have a 0 filled in the case that the species was not found in a specific run. The data from GMrepo cannot be downloaded as one CSV, so code is necessary to consoldiate all of the runs for a particular phenotype and across phenotypes. Data accessed from GMrepo had to be individually downloaded by run as a txt file, after filtering through to ensure that it was quality controlled (QC=1), and that the Phenotype was entered as one of the five neurological disorders studied here. This produces five files, one for each disorder, with a text file for each run within that disorder. The code in "20440_project_data_cleanup.ipynb" in the Code folder in this repository serves to clean the data from the individual text files, removing any notes or markdowns that are not data, consolidate all data within the subfolder of the disorder and annotate it with the diagnosis, then repeat across disorders, finally concatenating all disorders into one csv file with all relative abundances, diagnoses, and runs. 

The produced dataset can be used for dimensionality reduction with PCA followed by TSNE.

### Folder structure.

At a high level, the repository contains:
* **Code:** This folder contains two ipynb notebooks, "20440_project_data_cleanup.ipynb," which can be used to clean the txt file run data found in the Data folder, and "TSNE_analysis.ipynb" which contains the code to perform PCA and TSNE analysis and produce two SVG figures of (1) the individual diagnoses along the first two principal components and (2) the individual diagnoses plotted against the two TSNE components. Note that the data cleanup folder is not necessary to produce the figures, as the cleaned dataset has already been provided in the "Data" folder. However, it is included for clarity. 
* **Data:** This folder contains all of the data required for this analysis. There are 5 folders labeled by their disorder that contain the txt files with relative abundances for each read within the dataset. The file "20440_cleaned_data.csv" is the consolidated and cleaned dataset used in the analyses within this repo, and can be used to reproduce the figures. 
* **Figures:** This folder contains two figures. One, "PCA_plot.svg" is the visualization of the individual diagnoses when plotted against the first and second principal components produced by PCA. The other, "TSNE_plot.svg" is a figure containing the graph of the diagnoses plotted with the two components produced by TSNE analysis for dimensionality reduction. 
* **.gitattributes:** Details how git should handle files in specific, default ways. Includes large file management.
* **.gitignore:** Details which files git should ignore when committing and pushing (OS-generated files, jupyter checkpoints). 

### Installation.

All analysis was performed in Python 3.11.8. Code was stored and executed in Jupyter notebooks. In order to reproduce code, a jupyter notebook interface such as Anaconda is recommended for download of the code notebooks. The following packages and versions are needed to run this code:

* JupyterLab: 4.0.11
* pandas: 2.1.4
* sklearn: 1.2.2
* numpy: 1.26.4
* matplotlib: 3.8.0

