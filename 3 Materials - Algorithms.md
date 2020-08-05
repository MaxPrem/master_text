---
attachments: [Clipboard_2020-06-23-14-14-50.png]
tags: [masterarbeit]
title: 3 Materials - Algorithms
created: '2020-06-11T16:53:48.871Z'
modified: '2020-08-04T21:51:10.135Z'
---




# 3 Materials - Algorithms

scikit learn
keras
computer
code for dataaug
code for emsc
code for sav gol
python versoin....
spectra + perkeinelmeyer...




Workflow - Pipeline
* Preprocessing
  * Scaleing
  * EMSC scatter correction
  * Savgol Smoothing
  * Enet Variable Selection
    * cross-validated regulraization optimization

* PLS Variable Selection
  * greedy variable selection
* Outlier Detection
  * pls outlier Detectin
* Regression
  * PLS regression

## Variable Selection



_Nir spectra meassured over the instruments full range contain mostly uninformative and highly correlated variables. Performing variable selection before PLS regression, results in a more robust models with fewer PLS components required. 
PLS regression starts to overfitt the data quickly, as it finds highly correlated variables __by chance__ in the noisy regions of the spectra. To explain most of the variance  more latent variables are needed to account for the noise, thus overfitting occures.


@nirpy




### Variable Selection with Elastic net


_One possible approch for variable selection is using PLS regression and selecting wavelengths with high regression coefficients. Though this method suffers from PLS overfitting problem._

An alternative selection method based on an elastic net (EN) regression has been reported by Friedman et al.
EN regression incorporates a penalty term to enforce variable selection and another penalty term to encourage grouping of coefficients for correlated variables.


__This paper reports a method for variable selection by using an EN regression prior to a second regression by using PLS, a 2‐step method termed EN‐PLS. [Using elastic net regression to perform spectrally relevant variable selection]__

Unlike variable selection using the lasso, the sparsity of an EN regression is not constrained by the number of samples for a matrix that lacks full column rank (more variables than samples), and a set of correlated variables can be selected as a group.



(4) Although the accuracy of MLR is greatly increased by feature selection, MLR accuracy is still not better than the accuracy of full-spectrum PLS regression.

(5) No combination of PLS regression and feature selection has led to a prediction accuracy close to that of non-linear methods, e.g., artificial neural network (ANN).

+++ en pls



## Regression

### PLS regression

verry effective, on highly correlated data with more features than samples.

### Regression enet-PLS

has the advantage of varaibles selected with l1 and l2 norm. creating a sparse set of variables prior to dimension reduction with pls. The advantage is that less noise gets incoperated in the latent variables.

### Regression enet
Elastic net can also be used to predict samples, though it comes not close to the predictability of PLS regression achived by maximizing the explained variance $Y$ in $X$ multidimensional space.

### Regression ConvNet
Deep Neural Networks with convolutional layers, used for extracting features from visual data, feed the fully connected layers with their many weights, trying to minimize the training errors, each iteration.

 As the network gets optimised the weights in the convolutional layers get updated as well performing preprocessing steps, with similar results to known techniques as MSC and SavGol.


# Validation

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
