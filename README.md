# UK Used Cars Analysis: From Multivariate Data Analysis to Predictive Modeling

This report documents an in‐depth analytical journey using a UK used car dataset. We begin by thoroughly validating the data, then explore univariate and multivariate relationships, and finally build predictive models. Throughout, we explain each method and calculation to ensure clarity and reproducibility.


## 1. Introduction

The dataset consists of 100,000 UK used car records covering four major manufacturers: Audi, BMW, Mercedes, and Volkswagen. For manageability, we work with a random sample of 5,000 records. Key variables include:
- **Car Model**
- **Registration Year**
- **Price**
- **Gearbox Type**
- **Mileage**
- **Engine Fuel**
- **Tax**
- **Miles per Gallon (MPG)**
- **Engine Size**

The goal is to clean, explore, and model the data so that both numeric outcomes (e.g., price) and categorical outcomes (e.g., brand identification) can be accurately predicted.

## 2. Data Preparation and Validation

### 2.1 Data Loading and Subsetting
- **Libraries & Packages:** We begin by loading essential R packages (e.g., `missMDA`, `mvoutlier`, `corrplot`) and libraries for data manipulation.
- **Subsetting:** The full dataset is subsampled to 5,000 records while retaining all original variables.
- **Overview:** We inspect the structure, variable types, and summary statistics to understand the range and distribution of values.

### 2.2 Quality Checks: Missing Values, Errors, and Outliers
- **Missing Values:** We assess missing data using functions like `is.na()` and create vectors to count missings by variable and by individual.
- **Error Detection:** Checks are performed to flag any data entry mistakes (e.g., engine size of 0 for non‐electric vehicles).
- **Outlier Detection:** Visual tools such as boxplots and histograms help us identify extreme values. We also compute quantile-based thresholds to mark outliers in variables like price, mileage, tax, and MPG.


## 3. Exploratory Data Analysis (EDA)

### 3.1 Univariate Analysis
- **Descriptive Statistics:** Each variable’s central tendency and spread (mean, median, quartiles) are summarized.
- **Visualizations:**  
  - **Barplots** are used for categorical variables (e.g., car model, transmission type, manufacturer).
  - **Histograms and Boxplots** display the distribution and highlight potential outliers for numerical variables.
- **Data Quality Summary:** For each variable, we tabulate the number of missing values, errors, and outliers to gauge data reliability.

### 3.2 Multivariate Analysis
- **Correlation Analysis:**  
  - A correlation matrix is computed for numeric variables.  
  - For instance, the strong correlation between “year” and “mileage” is intuitively expected as newer cars have lower mileage.
- **Visualization:** The `corrplot` package is used to graphically display relationships between variables.


## 4. Data Imputation and Discretization

### 4.1 Imputation
To ensure the dataset is complete and unbiased before modeling, we impute missing values as follows:

#### 4.1.1 Numerical Variables
- **Method:** PCA-based imputation (via the `missMDA` package) is applied to numerical variables such as year, price, mileage, tax, MPG, and engine size.
- **Rationale:** PCA imputation preserves the underlying structure of the data by using latent components to predict missing values.

#### 4.1.2 Categorical Variables
- **Method:** Multiple Correspondence Analysis (MCA) is used for categorical data imputation.
- **Rationale:** MCA efficiently handles categorical data by capturing associations among categories, ensuring that imputed values are consistent with observed patterns.

### 4.2 Discretization
Transforming continuous variables into categorical bins enhances interpretability for profiling and further analysis:
- **Year:** Binned into yearly categories (e.g., 2008, 2009, …, 2020).
- **Price:** Categorized into ranges (e.g., Low-priced, Affordable, Moderately priced, Expensive) based on quartiles.
- **Mileage, Tax, MPG, and Engine Size:** Similar discretization is performed by calculating quantiles and assigning descriptive labels.
- **Visual Confirmation:** Barplots are generated for each discretized variable to verify the binning process.


## 5. Advanced Multivariate Techniques

### 5.1 Principal Component Analysis (PCA)
- **Objective:** Reduce dimensionality while preserving most of the variability.
- **Process:**  
  - Eigenvalues are computed to identify the dominant axes.
  - Variables are projected onto principal components to observe the main sources of variance.
- **Interpretation:** Contributions of each variable to the principal components are analyzed and visualized with biplots.

### 5.2 Multiple Correspondence Analysis (MCA)
- **Objective:** Explore relationships among categorical variables.
- **Process:**  
  - MCA decomposes the data into factors that explain the pattern of relationships.
  - Factor maps help visualize the clustering of categories.
- **Interpretation:** The proximity of points on the factor map indicates similarity between categories.


## 6. Clustering Analysis

### 6.1 K-Means Clustering
- **Objective:** Segment the dataset into homogeneous groups based on feature similarities.
- **Methodology:**  
  - The optimal number of clusters is determined (using methods such as the elbow method).
  - Clustering is performed on both PCA-reduced data and original features.
- **Profile:** Each cluster is characterized by both categorical (e.g., manufacturer, transmission) and numerical variables (e.g., price, mileage).

### 6.2 Hierarchical Clustering
- **Objective:** Provide an alternative grouping method using dendrograms.
- **Comparison:** Results are compared with K-Means clustering to evaluate consistency.
- **Validation:** Clustering quality is assessed using within-cluster variability and other metrics.


## 7. Predictive Modeling

### 7.1 Predicting the Numeric Target (Price)
- **Initial Model:**  
  - A basic regression model (e.g., price ~ engineSize + mpg) serves as the starting point.
- **Model Expansion:**  
  - Additional predictors (mileage, year, etc.) are added stepwise.
  - **Transformations:** Box-Cox and BoxTidwell transformations are applied to stabilize variance and linearize relationships.
  - **Interactions:** The inclusion of interaction terms is explored to capture joint effects among predictors.
- **Validation:**  
  - Model fit is assessed using diagnostic plots and influential point detection.
  - Cross-validation ensures the model’s generalizability.

### 7.2 Predicting the Binary Target (e.g., Audi vs. Non-Audi)
- **Initial Model:**  
  - A logistic regression is developed to predict the likelihood of a car being an Audi.
- **Enhancements:**  
  - Additional factors and interaction terms are incorporated.
  - **Performance Metrics:** A confusion matrix and other evaluation metrics are used to assess model accuracy.


## 8. Conclusion

- **Summary:**  
  - The report outlines a complete workflow from data preparation to advanced modeling.
  - Key findings include significant correlations (e.g., between year and mileage) and clear segmentation of car groups through clustering.
- **Implications:**  
  - The insights derived can support decision-making for pricing strategies and targeted marketing.
- **Future Work:**  
  - Further refinements may include additional predictive variables and external validation on larger datasets.
    

## References

- **Dataset:** [Kaggle Used Car Dataset](https://www.kaggle.com/adityadesai13/used-car-dataset-ford-and-mercedes)
- **Full Report PDF:** [UK Used Car Report](https://github.com/Aerosophia/Used-Cars/blob/main/Used%20Cars%20Analysis%20and%20Model%20Building/SoukainaMahboubMehboub-DelFinalRmd.pdf)
- **Additional Files:** [GitHub Repository](https://github.com/Aerosophia/Used-Cars/tree/main/Used%20Cars%20Analysis%20and%20Model%20Building)


## Author

**By:** Soukaïna Mahboub Mehboub  
**GitHub:** [@soukainacodes](https://github.com/soukainacodes)
