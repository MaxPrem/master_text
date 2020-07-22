---
attachments: [Clipboard_2020-06-23-14-14-50.png]
tags: [masterarbeit]
title: 3 Materials - Algorithms
created: '2020-06-11T16:53:48.871Z'
modified: '2020-07-21T16:51:26.298Z'
---

# 3 Materials - Algorithms
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


### pls variable selection



Optimise the PLS regression using the full spectrum, for instance using cross-validation or prediction data to quantify its quality.
Extract the regression coefficients form the best model.

 Each regression coefficient uniquely associates each wavelength with the response. 
 
 A low absolute value of the regression coefficient means that specific wavelength has a low correlation with the quantity of interest.

Discard the lowest correlation wavelengths according to some rule. These wavelengths are the ones that typically worsen the quality of the calibration model, therefore by discarding them effectively we expect to improve the metrics associated with our prediction or cross-validation.
@ nirpy





@nirpy


### Elastic Net
Elastic Net is a middle ground between Ridge Regression and Lasso Regression. The regularization term is a simple mix of both Ridge and Lasso’s regularization terms, and you can control the mix ratio r. When r = 0, Elastic Net is equivalent to Ridge Regression, and when r = 1, it is equivalent to Lasso Regression (see Equation 4-12).
@handsonscikit

![](@attachment/Clipboard_2020-06-11-18-31-10.png)



https://nirpyresearch.com/pls-discriminant-analysis-binary-classification-python/ PLS-LDA


### Variable Selection with Elastic net


_One possible approch for variable selection is using PLS regression and selecting wavelengths with high regression coefficients. Though this method suffers from PLS overfitting problem._

An alternative selection method based on an elastic net (EN) regression has been reported by Friedman et al.
EN regression incorporates a penalty term to enforce variable selection and another penalty term to encourage grouping of coefficients for correlated variables.


This paper reports a method for variable selection by using an EN regression prior to a second regression by using PLS, a 2‐step method termed EN‐PLS. [Using elastic net regression to perform spectrally relevant variable selection]

Unlike variable selection using the lasso, the sparsity of an EN regression is not constrained by the number of samples for a matrix that lacks full column rank, and a set of correlated variables can be selected as a group. 21




[Using elastic net regression to perform spectrally relevant variable selection]


(4) Although the accuracy of MLR is greatly increased by feature selection, MLR accuracy is still not better than the accuracy of full-spectrum PLS regression.

(5) No combination of PLS regression and feature selection has led to a prediction accuracy close to that of non-linear methods, e.g., artificial neural network (ANN).

_formular_



### Outlier Detection with PLS

_The aim is to improve the models predictive power by removing datapoints which do not fit the models underlying distribution. This can be caused by meassurement erros, __or is an effect of a to small sample size__. Removing Outlier should be done with great care, with the idea in mind to keep as many datapoints as possible._

Since we are working with labeld data for regression, 
__pls cross decomposition__
we can use the PLS algorithms ability to correlate X and y data to identify outliers and monitor MSE to observe their influence.



### Leverage

In chemometrics the leverage is a concept related to the Mahalanobis distance and is used to measure the influence of a sample in a model based on its similarity to the rest of the population. The Mahalanobis distance takes into account the correlations of the data set and is scale-invariant, i.e. not dependent on the scale of measurements.
The leverage of a sample is the distance to the centre of all samples relative to the variability in its particular direction
[@EMEA2012]

#### Metrics to define outliers with PLS regression


__Q-residuals__ are derived from the error matrix. Q-residuals account for the variations in the data that are not explained by the model as built.

An outlier is a point that does not follow the general trend of most (or all) other points. That means that for any given model, an outlier will have large Q-residual when compared to the corresponding residuals of the other points.

Q-residuals are calculated in practice by taking the sum of squares of each row of the error matrix. Python code to calculate error matrices and Q-residuals is below.
@nirpy - pls out


__Hotelling’s T-squared__ is the second important metric to detect outliers. While Q-residuals look at the variations that are not explained by the model, T-squared look at the variations within the model itself. A measure of how good is a sample within the model is given by the scores. Low scores mean very good fit. Hotelling’s T-squared can be intuitively thought as a distance of each sample from the ‘ideal’ zero-score situation of perfect fit.


## Regression

### Regression enet-PLS

### Regression CV PLS

### Regression enet

### Regression ConvNet


## Validation

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

In statistics, the Huber loss is a loss function used in robust regression, that is less sensitive to outliers in data than the squared error loss.

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
