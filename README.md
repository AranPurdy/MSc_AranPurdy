# MSc_AranPurdy
This repository contains the various scripts used in the MSc Dissertation "Uncovering the Limitations of Cell-free Protein Synthesis Through Metabolomic Analysis"
Each script is intended to be executed within Jupyter Notebooks

## Conda 
To run this project, you will need to have [Conda](https://www.anaconda.com/products/distribution) installed on your system.

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/AranPurdy/MSc_AranPurdy.git
    cd MSc_AranPurdy
    ```

2.  **Create and activate the Conda environment:**
    The provided `environment.yml` file contains all necessary dependencies.
    ```bash
    # Create the conda environment
    conda env create -f environment.yml

    # Activate the environment
    conda activate Msc_AranPurdy
    ```

3.  **Launch Jupyter Notebook:**
    ```bash
    jupyter notebook
    ```

The scripts are intended to be used as follows: 

# Missing Data Analysis and imputation
1. Apply thresholding to datafile **(Missing_Thresholds.ipynb)** to produce multiple outputs with varying levels of missingness with associated figures. Select one threshold for further analysis based on optimal signal:noise for your data.

2. Apply Little's MCAR test **(Little_MCAR_Test.ipynb)**: This should be done in parallel with other methods (missing data histogram from Missing_Thresholds / Imputomics missing data heatmap) to determine missing data patterns.

3. Manually impute the data **(Manual_Impute.ipynb)**: Use a subset of the data with low missing % to perform a simple imputation (mean per replicate group) this will be used to compare MVIAs (Missing Value Imputation Algorithms) against this "ground truth" data. T=0 is removed due to high missingness rate (some replicate groups have 5/5 missing values).

4. Generate artificial missingness patterns **(Generate_missingness)**: Will introduce MAR/MNAR/MCAR patterns to the manually imputed data, generating three output files: mcar_data.xlsx, mnar_data.xlsx, mar_data.xlsx

5. Use Imputomics website (https://imputomics.umb.edu.pl/) to impute the previously generated data files (mcar_data.xlsx, mnar_data.xlsx, mar_data.xlsx) according to their "5 most accurate methods for MCAR/MNAR/MAR" to produce three imputed data files, each with 5 sheets for each imputation algorithm. These should all be saved to the same directory.

6. Assess the performance of the imputations **(MVIA_Test)**: This script uses the ground truth data from step 4 (Manual_Impute), artificial missingness pattern data from step 5 (Generate_Missingness), and imputomics results from step 6 to compare imputations using NMRSE, MAE, and biological validity (number of negative values).

7. Based on the User's missing data pattern, they should select the imputation with lowest NMRSE, MAE, and fewest (ideally 0) negative values for further analysis. 

8. To compare two high-performing imputations and to inform data pretreatment approach **(Imputation_Concordance)**: Extract the sheets for two imputations and create two new excel files (KNN and RF are used here) (eg. KNN_Imputed.xlsx and RF_Imputed.xlsx) Applies log transform, pareto scale, autoscale, log+pareto, log+auto. Quantifies the similarity of PC scores and loadings between imputations across pretreatments using Pearson correlation and R-squared values. Displays plots showing variance explained of first 3 PCs across pretreatments.  

**By this point, the User will have selected an imputation and pretreatment that best suits their data**

## Pathway mapping 

## PCA 
- timepoint-specific
- PCA of mapped metabolites

## Metabolite trajectory 

