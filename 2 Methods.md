---
attachments: [Clipboard_2020-06-11-18-30-23.png, Clipboard_2020-06-11-18-31-10.png, Clipboard_2020-06-11-19-22-57.png, Clipboard_2020-06-11-19-25-07.png, Clipboard_2020-06-11-19-27-46.png, Clipboard_2020-06-11-19-57-21.png, Clipboard_2020-06-23-11-02-12.png, Clipboard_2020-07-27-15-41-31.png, Clipboard_2020-07-27-19-36-57.png, Clipboard_2020-08-02-16-03-43.png]
favorited: true
tags: [masterarbeit]
title: 2 Methods
created: '2020-06-09T11:25:02.276Z'
modified: '2020-08-05T10:39:42.988Z'
---

# 2 Methods

## Maschine Learning in Chemometrics


Machine Learning is the field of study that gives computers the ability to learn without being explicitly programmed. 
— Arthur Samuel, 1959

_Chemometrics is basically Machine Learning Algorithms applied to physio-chemical data._


__NIR spectra are characterized for their complexity and difficulty to be interpreted. For these reasons, multivariate methods from chemometrics are required to understand NIR spectra.__
[@Lopez2017]


<img src=@attachment/Clipboard_2020-06-11-19-25-07.png width = 600>

_Figure 3. General scheme shwoing the commonly multivariate techniques employed by NIR spectroscopy._ [@Lopez2017]

## Types of Machine Learning: Supervised and Unsupervised Learning



_Machine Learning systems can be classified according to the amount and type of supervision they get during training. [@handson8]_


### Training on labeld data - Supervised learning

Performing regression requires training data (samples) with a meassured quality to be predicted (continous response variable). In machine learning training on labeld data is called supervised learning. If the goal is to predict a discrete variable (class or type) the term classification is used.

* Linear Regression
  * A simple linear model predicting a response variable by assigning weights to (assumed to be independet) input features. Ordinary least squares regression (OLS) uses the residual sum of squares (RSS) as a loss function to estimate these weights. 

* Ridge Regression
  * Ridge introduces regularized regression by adding the L2 penalty (sum of squared coefficients)to the OLS equation, shrinking some of the coefficients close to zero.

* Lasso Regression
  * Lasso stands for least absolute shrinkage and selection operator and performs regularization by applying the L1 penalty. Minimizing the sum of absolute values from the regression coefficients, shrinking some coefficients to zero.

* Elastic Net
  * Enet combines L1 and L2 penalties, giving the algorithm more flexibility to reduce the regression coefficients. The weight of the two penaltie terms can be adjusted by crossvalidation. Elastic Net resulted from the drawback of lassos unstable variable selection depending on the amount of input data. 
  As the features in NIR spectroscopty are many and highlty correlatet, enet puts a higher wheight on the L1 penalty trying to obtain a sparse model.

* Partial Least Squares Regression
  * PLS, a cross-decomposition algorithm, performs dimensonality reduction prior to regression, by maximizing the explained variance of input and predictor matrices in a few so called latent variables. PLS-regression performs highly efficiently in analyzing data with more features than samples, and when those features are multicolinear. [@cross2020]

* Aritificial Neural Networks (ANN)
  * A Deep Neural Networks (ANN with many layers) can perfrom regression tasks by condensing the neurons in the conected layers to a single output neuron. A linear activation function is used in the final output neuron to predict the response variables value. 
   A cost function like RSS or huber loss is minimized by an optimizer like gradient descent to adjust the weights of up to millions of neurons during training. Sending all training and testing data through the network is called an epoch. After a certain amount of epoches the loss function reaches a minima or a plateau and no further improvement can be archieved by training the network.
   
   One advantage of ANN for regression is that nonlinear relationships can be learned by the the model. Nonlinear activation functions determine the activity of each neuronm, leading to different phats through the network depending on the input features. The complexity of the model (number of trainable parameters) allows the network to learn  subtle patterns in the data, enabeling neural networks to make the most accurate predictions.



[@handson8]

### Training on data without external information -  Unsupervised learning

Without labeld data to learn relationships from, unsupervised learning can be used to understand the structer of the unlabeld data by grouping the samples in a number of clusters using a distance metric (k-means), or to find independent features with the most variance by projecting the data onto principal component space. (PCA dimensionality reduction).

* Principal Component Analysis (PCA)
  * Visualization and Dimensionality reduction by projecting samples onto Principal Component space
* K-means-clustering
  * Grouping samples into a k number of clusters, while maximizing cluster center distance. Different strategies and distance meassurs can be used to calculate the space between samples and clusters, to visualizing the underlying relationships in multidimensional feature space.

## Modeling the Data
Fewer degrees of freedom make it less likely for a model to overfit the data. 
This can be achieved by using a simpler model (fewer components) and by reducing the complexity of the data by decreasing the number of input-variables (variable selection) or perfroming dimensionality reduction (PCA, PLS) prior to training the model.
[@handson8]

![](@attachment/Clipboard_2020-06-11-18-30-23.png)

### Noise 

Random fluctuations always occure when using physio-chemical methods to meassure effects and states.The first aim of any scientific experiment is to generate data of the highest quality, and much effort is usually put into decreasing noise levels. Noise can simply be reduced by performing $n$ repeated measurements of a sample, averaging out the variance from unwanted physical properties and random fluctuationsby a factor of $\sqrt{n}$.
[@Wehrens2011]

### Overfitting the Training Data

A model containing more parameters than necessary to learn the fundamental relationships in the data will overfitt, as it is prone to model random patterns present in the noise.

Using out of bag samples (test data) not seen by the model during traing, an estimate about the models accuracy can be done. Overfitting can be prevented by reducing the number of parameters used by the model, the number of input features and/or by increasing the sample size. [@handson8]

### Underfitting the Training Data
Underfitting occures when the model is to simple to learn the underlying mechanisms from the training data to make accurate predictions.
[@handson8]

## Multivariate Analysis 

### Dealing with Spectral Data

Modeling multivariate data, containing more highly correlated variables than samples, is the main difficulty in analyzing NIR spectra. Standard ordinary least squares (OLS) predictions will fail, as the inverse of a matrix with more features than samples has no unique solution. Indicating a high to infinite amount of inverse matrices and too many possible coefficient vectors. [@Wehrens2011]

One way to tackle these problems is to use regularized regression to reduce the variance of the coefficient estimates by introducing some bias.

Another way is to  perform dimensionalty reduction prior to regression. This is done by explaining most of the variance in the data by projecting it onto a lower dimensional space created from linear combination of the input variables. These are called principal components for PCA and latent variable for PLS regression.

These two techniques can also be combined with great succes in a method called EN-PLS [@Giglio2018]. A set of informative variables is selected by elastic net regression prior to dimension reduction. The reduction of noise by removing uninformative variables, results in a model needing fewer latent variables to explain the structure of the data, makeing it less likely to overfit.


## Linear Models and the multicolinearity problem

Linear regression is used to model the relationship of a target value from input features (explanatory variables). In OrdinaryLeastSquares regression (OLS) the response variable is predicted by minimizing the mean squard error (MSE) on the training data (input features). The coefficients used in the linear model need to be independent, otherwise their variance is too high and predictions are not accurate.
NIR chemometrics spectra contain mostly highly correlated features, and more variables than samples, makeing it diffcult to perform regression on the spectra without multivariate techniques.
These prequisites make OLS regression regression fail, when trying to predict NIR spectra. One solution is to the select a set of not highly correlated wavelenghts and perform OLS regression on those features. 

### Regularized Linear Models

Regularization in linear regression can be done by reduceing the number of features by setting some of the coefficients to zero (lasso) creating a sparse model with single variables selected from groups of highly correlated ones, or by reducing some of the coefficients close to zero (ridge) creating a model containing all variables with adjusted feature weights. 
Booth regularization approches solve the multicolinearity problem by introducing bias to estimate the coefficients, creating a model that can be used to predict from NIR spectra.

The two regularization methods can also be combined leading to a reduction of noise and unimportant variables, makeing regularized regressiuon a suitable variable selection method for NIR spectroscopy.

[@Regularization in Machine Learning]

#### Loss Function for Ordinary Least Squares regression

Residual sum of squares (RSS), the loss function to be minimized in ordinary least squares (OLS) regressions is used to estimate the optimal weights to predict the response variables. It meassurs the sum of errors from predicted $\hat{y}$ minus actual response value $y$ from the model, and is squared to return only positive values.

$$
\mathrm{RSS}=\sum_{i=1}^{n}\left(y_{i}-\beta_{0}-\sum_{j=1}^{p} \beta_{j} x_{i j}\right)^{2} =\sum_{i=1}^{n}\left(y_{i}-\hat{y}_{i}\right)^{2}
$$


* $\beta_{j}$ are unknown coefficients
* $x$ are the quantitative inputs
* $\beta$ are the estimated inputs 
* $p$ is the number of dimensions (p = 1 -> univariate regression; p > 1 -> multivariate regression i.e. more than one feature  per input variable)

 In OLS regression we estimate the coefficients $\beta_{i}=\left(\beta_{i 1}, \beta_{i 2}, \ldots, \beta_{i p}\right)^{T}$ for each input variable $x_{i}=\left(x_{i 1}, x_{i 2}, \ldots, x_{i p}\right)^{T}$ for the $i$th case, to find optimal weights resulting in a minimal loss. 

(T = transpose; indicates columvector)

[@Ziegel2003]

#### Ridge

$$
\sum_{i=1}^{n}\left(y_{i}-\beta_{0}-\sum_{j=1}^{p} \beta_{j} x_{i j}\right)^{2}+\lambda \sum_{j=1}^{p} \beta_{j}^{2}$$

$$=\operatorname{RSS}+\lambda \sum_{j=1}^{p} \beta_{j}^{2}$$

Ridge regression minimizes the RSS loss function by adding a penalty term that is equal to size of the square of the coefficients (L2 - penalty), shrinking some coefficients almost to zero. The estimated model includes all predictor variables with assigned weights. [@Ziegel2003]


#### Lasso
$$
\sum_{i=1}^{n}\left(y_{i}-\beta_{0}-\sum_{j=1}^{p} \beta_{j} x_{i j}\right)^{2}+\lambda \sum_{j=1}^{p}\left|\beta_{j}\right|
$$

$$=\operatorname{RSS}+\lambda \sum_{j=1}^{p}\left|\beta_{j}\right|$$

Lasso is another variation, in which the above function is minimized by the absolute sum of the coefficients (L1 - penalty), setting some of the coefficients exactly to 0, if the tuning coefficients $\lambda$ controling the penalty reaches a certain limit.

Lasso creates sparse models by selecting the non-zero coefficients, opposed to rige regression using all variables setting some coefficients almost to 0. [@Ziegel2003]

#### Elastic Net
Elastic net combines L1 and L2 penalty terms to minimze the RSS loss function, with the advantage of beeing able to select more than one variable out of a group of highly intercorrelated variables. Lasso fails at selecting variables deterministically if the number of features surpasses the number of samples resulting in single variables selected randomly if two were equally important in a intercorrelated group. [@Ziegel2003]


$$
\frac{\sum_{i=1}^{n}\left(y_{i}-\beta_{0}-\sum_{j=1}^{p} \beta_{j} x_{i j}\right)^{2}}{2 n}+\lambda\left(\frac{1-\alpha}{2} \sum_{j=1}^{p} {\beta}_{j}^{2}+\alpha \sum_{j=1}^{p}\left|\hat{\beta}_{j}\right|\right)
$$

$$=\frac{RSS}{2n} +\lambda\left(\frac{1-\alpha}{2} \sum_{j=1}^{p} {\beta}_{j}^{2}+\alpha \sum_{j=1}^{p}\left|\hat{\beta}_{j}\right|\right)$$ 

$\alpha$ is elasticnet's mixing parameter, performing conventional ridge regression with $\alpha = 0$ and conventional lasso regressen with $\alpha = 1$.

#### Penalities

![](@attachment/Clipboard_2020-07-27-15-41-31.png)

The outline of the penalties is shown in the contour plot. The round contour is the ridge penalty, the box shaped contour the lasso penalty and the red one is the penalty of elastic net for $\alpha = 0.5$. The shape of the elastic net countour results from the value of $\alpha$.
[@Zou2005]

### Dimension Reduction 



PCA performs dimension reduction by creating linear combination of the input variables. These so called principal components, point in the direction explaining most of the variance in the data and are orthogonal to each other. Plotting the data using the first two principal components visualizes the higher dimensional data in 2d space. The more components are used, the higher dimensional is the principal component space used to explain the variance of the data.

[@revpca20]

### Cross-decomposition

The difference between PCA and PLS is that PLS is a cross-decompostion technique. The first obtained latent varaibles tries to explain most of the variance of X and y, opposed to PCA's principal components explaining most of X variance in the first component.



#### PLS 
Partial least squares (PLS) analysis can be used to build predictive models, even if the features are very little correlated. 

The aim of PLS is to establish a relationship between the two matrices X and Y by crossdecomposition. The process is as follows: First, the main components for X and Y are calculated separately. The matrix X scores are then used to predict the Y scores in a regression model, which in turn can then be used to predict Y.

Partial Least Squares (PLS) models are based on the main components of both the independent variable X and the dependent variable Y. The central idea is to calculate the main components separately for the matrices X and Y and a regression model between the scores of the main components (and not the original data).

For this purpose, the matrix X is broken down into a matrix T (the "score" matrix) and a matrix P '(the "loadings" matrix) plus an error matrix E. The matrix Y is divided into the matrices U and Q and the error term F disassembled. These two equations are called the "external relationships". The aim of PLS ​​is to minimize the norm of F while maintaining a correlation between X and Y by relating the matrices U and T: U = BT. This equation is also called the "inner relationship".


#### PLS


The aim of PLS is to establish a relationship between the two matrices X and Y by crossdecomposition. The so called latent variables approaches to model the covariance structures in these two spaces and tries to find the multidimensional direction in the $X$ space that explains the maximum multidimensional variance direction in the $Y$ space.

According to sklearn's documentation PLS-regression is particularly suited when the matrix of predictors has more variables than observations (as in NIR spectra), and when there is multicollinearity among $X$ values. By contrast, standard regression will fail in these cases.__
[@cross2020]

![](@attachment/Clipboard_2020-08-02-16-03-43.png)
[@pls2020]

$X = T \times P^T + E$


* $X$ is the matrix consisting of $m$ spectra (samples) and $n$ wavelengths, a $m×n$ matrix.

* $P$ is the loading matrix, the containing loading vectors show the variable importance for each component (latent variable) in the model. 

* The matrix $T$ is called the scoreing matrix. The scores describe how well each sample pair (spectra + reference value) is described by the underlying model.

* The error matrix $E$ , adds error terms for the variance in the data $X$, that can not be explained by the model, also called bias.


Analogous a model is created for the response variable.


$Y = U \times Q^T + F$ 

The PLS model has the objective to maximize covariance between the loading matrices $T$ and $U$, by finding a multidimensional direction in $X$ space explaining the variance in $Y$.
[@pls2020]



### Outlier Detection with PLS

PLS can also be used to perfrom outlier removal, by determining the samples fit with the model and the whole sample population. Since we are working with labeld data, we are going to use all information available, spectra and reference method values, to identify outliers.

The two metrics estimating each samples fit to the model's underlying distribution are Q-residuals and Hotteling's T-squared distance.

The Q-residualsmatrix describes the variation not explained by the obtained model and also depends on the number of components selected. We are using a 95% confidence intervall to decide if a value qualifies as an outlier.

Hotteling's T-squared distance
The Hotteling's T-squared distance is a metric meassureing a sample's fit described by the model, with a score of 0 defining a perfect fit.

### Variable Selection with PLS

PLS can also be used for variable selectoin, by sorting the wavelenghts according to their score correlating with the response variable.
One wavelength after another is deleted until a minimum mean squared error is reached. This procedure is repeated up to a defined number of principal components. Unfortunately this method has a few drawbacks. First PLS strength of explaining a maximum of variance leads to the selection of noisy variables correlating by chance, another drawback is the increase of the runtime with the input size. Makeing it perform worse on the task than regularized regression.




# Validating Regression using Loss and Score Functions

https://scikit-learn.org/stable/modules/learning_curve.html

# Error
[from _regression sklearn]
"""Metrics to assess performance on regression task

__Functions named as ``*_score`` return a scalar value to maximize: the higher the better__

__Function named as ``*_error`` or ``*_loss`` return a scalar value to minimize: the lower the better__
"""

## Bias (means of errors)


A statistic measuring the mean of the errors between the NIRS and reference quantitative analyte values


$$
\text { Bias }=\frac{\sum_{i=1}^{n}\left(y_{i}-Y_{i}\right)}{n}
$$

Y = NIRS predicted value
y = reference method value 
n = number of samples

@[]

## SEC 
Standard error of estimate (SEE), also termed standard error of calibration (SEC).

A statistic measuring the difference between the NIRS procedure and reference method quantitative analyte values of the calibration set. [@EMEA2012]

$$
\mathrm{SEC}=\sqrt{\frac{\sum\left(X_{i}-Y_{i}\right)^{2}}{(N-p-1)}}
$$

MLR: number of wavelenghts
PLS/PCR: number of principal components
ANN: number of trainable weights or notes in final layer


The SEC will decrease with the number of wavelengths (independent variable
NIRS Calibration Basics 145
terms) used within an equation, indicating that increasing the number of terms will allow more variation within the data to be explained, or “fitted.” The SEC statistic is a useful estimate of the theoretical “best” accuracy obtainable for a specified set of wavelengths used to develop a calibration equation

@Handbook of Near-Infrared Analysis, Third Edition (Practical Spectroscopy) by Donald A. Burns, Emil W. Ciurczak (z-lib.org).pdf



$$
\mathrm{SEP}=\sqrt{\frac{\sum\left(X_{i}-Y_{i}\right)^{2}}{N}}
$$

## SECV - Standard Error of CrossValidation

A statistic measuring the difference between the NIRS procedure and reference method quantitative analyte values of the calibration set using a cross-validation method.

$$
S E C V=\sqrt{\frac{\sum_{i=1}^{n}\left(y_{c v, j}-Y_{c v, i}\right)^{2}}{n}}
$$

Ycv = NIRS predicted value
ycv = reference method value
n = number of samples 

## SEP - Standard Error of Prediction

A statistic measuring the difference between the NIRS procedure and reference method quantitative analyte values of the calibration test set and the independent validation set. The SEP derived from the independent validation set is considered a pivotal statistical parameter.
SEP

$$
S E P=\sqrt{\frac{\sum_{i=1}^{n}\left(y_{V, i}-Y_{V, j}\right)^{2}}{n}}
$$

## REP - Relative prediction deviation

$$
REP =\sqrt{\frac{\sum_{i=1}^{n}\left(SD\right)^{}}{SEC}}
$$

### Mean squared error 
<https://en.wikipedia.org/wiki/Mean_squared_error>

In statistics, the mean squared error (MSE) or mean squared deviation (MSD) of an estimator measures the average of the squares of the errors—that is, the average squared difference between the estimated values and the actual value.

$$\operatorname{MSE}=\frac{1}{n}\sum_{i=1}^n(Y_i-\hat{Y_i})^2$$

The MSE can also be computed on ''q ''data points that were not used in estimating the model, either because they were held back for this purpose or because these data have been newly obtained.  The MSE is often called the mean squared prediction (MSEP) error on test data or mean squared error of cross validataion (MSECV), when the held out data was obtained by crossvalidation.

$$\operatorname{MSEP}=\frac{1}{q}\sum_{i=n+1}^{n+q}(Y_i-\hat{Y_i})^2$$



#### Huber loss

In statistics, Huber loss is a robust estimator to determine the location parameter of a normally distributed population. It is also a frequently used loss function in machine learning and robust regression.

The robustness is achieved by scaling down large values, starting at $k$, that are seen as outliers to cut their quadratic influce.


The Huber loss function describes the penalty incurred by an estimation procedure f. Huber (1964) defines the loss function piecewise by[1]


```latex
L_\delta (a) = \begin{cases}
 \frac{1}{2}{a^2}                   & \text{for } |a| \le \delta, \\
 \delta (|a| - \frac{1}{2}\delta), & \text{otherwise.}
\end{cases}
```




<img src=@attachment/Clipboard_2020-06-23-14-14-50.png width="200">

This function is quadratic for small values of $a$, and linear for large values, with equal values and slopes of the different sections at the two points where $|a| = \delta$. The variable $a$ often refers to the residuals, that is to the difference between the observed and predicted values $a = y - f(x)$, so the former can be expanded to 
 
 [Huber, Peter J. (1964). "Robust Estimation of a Location Parameter". Annals of Statistics. 53 (1): 73–101. doi:10.1214/aoms/1177703732. JSTOR 2238020.]

```latex
L_\delta(y, f(x)) = \begin{cases}
 \frac{1}{2}(y - f(x))^2                   & \textrm{for } |y - f(x)| \le \delta, \\
 \delta\, |y - f(x)| - \frac{1}{2}\delta^2 & \textrm{otherwise.}
\end{cases}

```


















