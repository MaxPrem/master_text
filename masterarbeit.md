---
tags: [masterarbeit]
title: masterarbeit
created: '2020-06-01T11:26:57.304Z'
modified: '2020-06-10T09:53:32.416Z'
---

# masterarbeit

# Masterarbeit:
Aim of the thesis? predicting NIR spectra, algorithm, gui,

# 1 Abstract

NIR Prepro .... Robust Reg vs Overfitting..... Classical Chemometrics -> Machine Learning ... Deep Nets

state of the art: pls ... interpretable model...
svm & deep nets with higher ~~accuracy~~

## 2 Introduction and Background:

### 2.1 History

## 2.2 NIR Spectroscopyv Theory

### 2.2.1 Messprinzip
_ Diffuse reflectance, Fourier Transformation,

# 3. Methods
## 2.3 Chemometrie

# Maschine Learning
# Preprocessing
# DimensionReduction
# Preprocessing
_ Preprocessing: MSC, MC, SavatzkyGolay polynomial function [nirpy]


# DeepLearning

## _asdfasdf_


## History of NIRs:
	_ FTNIR
	_ Diffuse reflectance, Fourier Transformation,


## Comparing Multivariate models:

pls / mulitiblock pls
randomforest / lda pca / deepnet

F - test to compare regression models =)






# 3 Methods

## Deep Neural networkds
### Architecutre
cp-mlbook: 
TensorFlow also offers a few other kinds of convolutional layers:
• keras.layers.Conv1D creates a convolutional layer for 1D inputs, such as time series or text (sequences of letters or words), as we will see in ??

using keras.Sequential API
	- Adding Gausion (Noise also works as regularization)
	- Conv1D 8 Kernel 32 widht
	- Conv1D 16 Kernel 32 wihth
	- Flatten to 1D vector
	- Dense 128
	- Dense()

## Preprocessing

### preprocessing deep Learning
to prevent the model from shortcut learning (like using the postion as feature) dataaugmentation helps greatly to introduce some ,,noise''
### PREPROCESSING Classical

using standard scaler or

robust scaler 

https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.RobustScaler.html

effects of different sclaer on the data 

#### en-pls paper: scaeling resulting in better variable selection than mean centering

https://nirpyresearch.com/two-scatter-correction-techniques-nir-spectroscopy-python/

Data pre-processing is an essential step to build most (ahem, all) types of calibration models in NIR and most spectroscopy analysis. With a well-designed pre-processing step, the performance of the model can be greatly improved.

Pre-processing techniques can be generally divided into
1) Scatter Corrections techniques and
2) Derivative techniques.
Both MSC and SNV belong to the first category.
###



Preprocessing NIRs spectra leads subsquently to smaller models with higher predictive power
by improving the signal to noise ratio.

Many algorithms rely on meanspectra like Savitzky-Golay Filtering as a reference.

Order of steps.

Importance of scaling and centering the right way. Removing Calibration data from Test set....


- FTNIR
	- Diffuse reflectance, Fourier Transformation,
	- Preprocessing: MSC, MC, SavatzkyGolay polynomial function [nirpy]

## Dimension Reduction 

PLS is at heart a dimensionality reduction technique. Just like PCA, it realises a coordinate transform. Spectra, initially function of wavelength (or wave number), are transformed to become function of generalised coordinates called principal components (or, more correctly, latent variables in PLS).

This is a key concept: there is no way around some sort of decomposition when dealing with spectral data. All spectra, from the point of view of a machine learning model, suffers from multicollinearity problems. Multicollinearity in a spectrum means that the signal at one wavelength is (somewhat or highly) correlated with the signal at neighbouring wavelengths. This correlation makes the mathematical problem of solving a least square regression ill-posed. In practice this means you can’t simply run a linear least square regression on the raw spectra, as the algorithm will fail (Note you can however modify the linear regression to introduce a regularisation of the least square problem. An example is the Ridge regression, but there’s more).

A dimensionality reduction transformation takes away the multicollinearity. The principal components are independent from one another and can be used together to run a regression. There are a number of techniques to achieve dimensionality reduction (take a look here for an overview). PLS and PCA are two of them.

Unlike PCA, PLS is a cross-decomposition technique. It derives the principal components by maximising the covariance between the spectra and the response variable (PCA on the contrary is based on minimising the covariance between the different spectra, without looking at the response variable). Therefore PLS will ensure that the first few principal components have a good degree of correlation with the response variable. This fact alone is arguably the reason why PLS is generally very successful in building calibration models in spectroscopy: in one swift operation, PLS can accomplish both dimensionality reduction and good correlation with the response.

Now, PLS has been originally developed for (and mostly lends itself to) regression problems. Other dimensionality reduction techniques – such as PCA or LDA – are often/always used for classification. While being a dimensionality reduction technique itself, PLS is not generally applied to classification problems in the same way. Here’s a few reasons for that.

PCA decomposition doesn’t require the knowledge of the response variable. It therefore lends itself to both regression and classification problems, the latter in supervised or unsupervised fashion alike.
LDA decomposition is specified only for categorical response variables. It is therefore naturally applied to (supervised) classification.
PLS decomposition is inextricably linked to the response variable which is usually a continuous variable. PLS predictions therefore belongs to a continuum, which is another way of saying that PLS is naturally applicable to regressions.

https://nirpyresearch.com/pls-discriminant-analysis-binary-classification-python/ PLS-LDA

## Variable Selection
lalala not so well....

Variable selection in chemometrics
The idea behind variable selection in chemometrics is that when it comes to spectral measurements not all wavelengths are created equals. In visible and NIR spectroscopy especially, it is often hard to predict in advance which wavelength bands will contain most of the signal related to the analyte we want to measure. So, as a first shot, we measure the whole range allowed by our instrument, and then figure out later which bands are more relevant for our calibration.

#### Feature selection by filtering - PLS
Feature selection by filtering is one of the simplest ways of performing wavelength selection. For an overview of the methods that are currently used, check out this excellent review paper by T. Mehmood et al.: A review of variable selection methods in Partial Least Squares Regression.

The idea behind this method is very simple, and can be summarised in the following:

	1. Optimise the PLS regression using the full spectrum, for instance  using cross-validation or prediction data to quantify its quality.

  2. Extract the regression coefficients form the best model. Each regression coefficient uniquely associates each wavelength with the response. A low absolute value of the regression coefficient means that specific wavelength has a low correlation with the quantity of interest.

	3. Discard the lowest correlation wavelengths according to some rule. These wavelengths are the ones that typically worsen the quality of the calibration model, therefore by discarding them effectively we expect to improve the metrics associated with our prediction or cross-validation.



#### Feature selection by ElasticNet - PLS

Multivariate  Statistics:

Modelselection? Feature Engineering, Variable Selection, singular Matrix problem -> sparce matrix?

	Classification:
		Standardisation PCA, Randomforest

	Regression:
		PCR, PLS

	Validation:
		Loss function (vs. Simlated annealing)

N-Fold Cross-Validation train test split..


### MVR vs Deeplearning

### Classification / Dim reduction:
### Feature scaling / standaridisation:

https://scikit-learn.org/stable/auto_examples/preprocessing/plot_scaling_importance.html#sphx-glr-auto-examples-preprocessing-plot-scaling-importance-py

## PCA/RobPCA

## Regression:
https://scikit-learn.org/stable/auto_examples/plot_kernel_ridge_regression.html#sphx-glr-auto-examples-plot-kernel-ridge-regression-py


# 4 Materials:

# 5 Results:

# 6 Discussion

Table 5: Model performance on train and test set for partial least squares (PLS) and neural network models (NN). Train set includes the validation set used for tuning of hyperparameters and consists of spectrum obtained with instrument one. Test set consists of tablet samples that was never included in train and validation sets and consists of spectrums obtained with instrument two. The best performance on each test set is marked in bold.

Figure 5: Scatter plot of true and predicted reference values using the extrapolation dataset with data augmentation followed by extended multiplicative scatter correction (EMSC). The training of the CNN model included the validation set used in the tuning of the hyperparameters. The small insert on each graph shows a zoom of the external test set.

## The Bias/Variance Tradeoff
An important theoretical result of statistics and Machine Learning is the fact that a model’s generalization error can be expressed as the sum of three very different errors:
Bias
Variance
This part is due to the model’s excessive sensitivity to small variations in the training data. A model with many degrees of freedom (such as a high-degree pol‐ ynomial model) is likely to have high variance, and thus to overfit the training data.
Irreducible error
This part is due to the noisiness of the data itself. The only way to reduce this part of the error is to clean up the data (e.g., fix the data sources, such as broken sensors, or detect and remove outliers).
Increasing a model’s complexity will typically increase its variance and reduce its bias. Conversely, reducing a model’s complexity increases its bias and reduces its variance. This is why it is called a tradeoff.


	Underfitting Overfitting
	- Training Loss -- / Validation loss ++
	- > stop Training model to prevent Overfitting


	# 7 Conclusion and Outlook
	# 8 References
	# 9 Figures and Tablets
	# 10 Appendix






# ChemometricswithR



### Standaridisation and Meancentering




Many other smoothing functions are available – only a few will be men- tioned here briefly. In signal processing, Savitsky-Golay filters are a popular choice [10]; every point is replaced by a smoothed estimate obtained from a local polynomial regression. An added advantage is that derivatives can si- multaneously be calculated (see below). In statistics, robust versions of locally weighted regression [11] are often used; loess and its predecessor lowess are available in R as simple-to-use implementations. The fact that the fluctuations in the noise usually are much faster than the data has led to a whole class of frequency-based smoothing methods, of which wavelets [12] are perhaps the most popular ones. The idea is to set the coefficients for the high-frequency components to zero, which should leave only the signal component.

# 3.7 Conclusion


Data preprocessing is an art, in most cases requiring substantial background knowledge. Because several steps are taken sequentially, the number of possible schemes is often huge. Should one scale first and then remove noise or the other way around? Individual steps will influence each other: noise removal may make it more easy to correct for a sloping baseline, but the presence of a baseline may also influence your estimate of what is noise. General recipes are hard to give, but some problems are more serious than others. The presence of peak shifts, for instance, will make any multivariate analysis very hard to interpret.

Finally, one should realise that bad data preprocessing can never be com- pensated for in the subsequent analysis. One should always inspect the data before and after preprocessing and assess whether the relevant information has been kept while disturbing signals have been removed. Of course, that is easier said than done – and probably one will go through a series of modelling cycles before one is completely satisfied with the result.

- FTNIR
	- Diffuse reflectance, Fourier Transformation, nirpyblog
	- Preprocessing: MSC, MC, SavatzkyGolay polynomial function [nirpy]


ALGORITHMS:

PCA:

PCA finds a new set of dimensions such that all the dimensions are orthogonal (and hence linearize independent) and ranked according to the variance of data along them.

Find a transformation such that
-	The transformed features are linearly independent
-	Dimensionality can be reduced by taking only the dimensions with the highest importance
-	Those  newly found dimensions should minimize the projection error
-	The project points should have maximum spread, i.e. maximum variance

Variance: formular

Covariance Matrix:
inidicates the level to which two varialbles vary together.

cov formularv -> eigenvectors , eigenvalues

Eigenvector, Eigenvalues:
The eigenvectors point in the direction of the maximum variance, and the corresponding eigenvalues indicates the importance of its corresponding eigen vector.
Av` = λv`

Approach:
-	Substract the mean from X
-	Calculate Cov(X,X)
-	Calculate eigenvectors and eigenvalues of covariance matrix
-	Sort the eigenvectors according to their eigenvalues in decreasing order
-	Choose first k eigenvectors and that will be the new k dimensions
-	Transfrom the original n dimensional data points into k dimension (=Projections with dot product)



	.







Classification:
votingClassifier
https://scikit-learn.org/stable/auto_examples/ensemble/plot_voting_decision_regions.html

randomforest + Roc curve:

https://scikit-learn.org/stable/auto_examples/plot_roc_curve_visualization_api.html#sphx-glr-auto-examples-plot-roc-curve-visualization-api-py

Linear Regression:

Multiple Linear Regression

Multiple Linear Regression uses two or more independent variables to predict the values of the dependent variable. It is based on the following equation that we’ll explore later on:
y=b+m1x1+m2x2+...+mnxny=b+m1x1+m2x2+...+mnxn


LossFunction:

Gradient Descent for Intercept



Results:





Classyfing unknown spectra

Classification:
votingClassifier
https://scikit-learn.org/stable/auto_examples/ensemble/plot_voting_decision_regions.html

randomforest + Roc curve:

https://scikit-learn.org/stable/auto_examples/plot_roc_curve_visualization_api.html#sphx-glr-auto-examples-plot-roc-curve-visualization-api-py

