---
attachments: [Clipboard_2020-06-11-18-30-23.png, Clipboard_2020-06-11-18-31-10.png, Clipboard_2020-06-11-19-22-57.png, Clipboard_2020-06-11-19-25-07.png, Clipboard_2020-06-11-19-27-46.png, Clipboard_2020-06-11-19-57-21.png, Clipboard_2020-06-23-11-02-12.png]
favorited: true
tags: [masterarbeit]
title: 2 Methods
created: '2020-06-09T11:25:02.276Z'
modified: '2020-07-21T17:16:20.898Z'
---

# 2 Methods

## Maschine Learning in Chemometrics


Machine Learning is the field of study that gives computers the ability to learn without being explicitly programmed. 
— Arthur Samuel, 1959

_Chemometrics is basically Machine Learning Algorithms applied to physio-chemical data._


__NIR spectra are characterized for their complexity and difficulty to be interpreted. For these reasons, multivariate methods from chemometrics are required to understand NIR spectra.__
[@Lopez2017]


<img src=@attachment/Clipboard_2020-06-11-19-25-07.png width = 600>

_Figure 3. General scheme shwoing the commonly multivariate techniques employed by NIR spectroscopy._


#### summary

If your linear model contains many predictor variables or if these variables are correlated, the standard OLS parameter estimates have large variance, thus making the model unreliable.

To counter this, you can use regularization - a technique allowing to decrease this variance at the cost of introducing some bias. Finding a good bias-variance trade-off allows to minimize the model's total error.

There are three popular regularization techniques, each of them aiming at decreasing the size of the coefficients:
* Ridge Regression, which penalizes sum of squared coefficients (L2 penalty).
* Lasso Regression, which penalizes the sum of absolute values of the coefficients (L1 penalty).
* Elastic Net, a convex combination of Ridge and Lasso.

The size of the respective penalty terms can be tuned via cross-validation to find the model's best fit.

@nirpy
## Types of Machine Learning: Supervised and Unsupervised Learning



_Machine Learning systems can be classified according to the amount and type of supervision they get during training. [@handson8]_


### Training on labeld data - Supervised learning

Performing regression requires training data (samples) with a meassured quality to be predicted (response variable). In machine learning training on labeld data is called supervised learning. If the goal is to predict a discrete variable (class or type), instead of a continous varaible the term classification is used.

* Linear Regression
  * A simple linear model predicting a response variable by assigning weights to (assumed to be independet) input features. Ordinary least squares regression (OLS) uses the mean squared error (MSE) as a loss function to estimate these weights. 

* Ridge Regression
  * Ridge introduces regularized regression by adding the L2 penalty to the OLS equation (minimizing ther sum of squared coefficients by shrinking some coefficients close to zero)

* Lasso Regression
  * Lasso performs regularization with the L1 penalty (minimizing the sum of absolute values of coefficients, by shrinking some coefficients to zero.)

* Elastic Net
  * Enet combines L1 and L2 penalties, giving the algorithm more flexibility to reduce the regression coefficients. The weight of the two penaltie terms can be adjusted by crossvalidation. Elastic Net resulted from the drawback of lassos unstable variable selection depending on the input data. 
  As the features in NIR spectroscopty are many and highlty correlated, enet puts a higher wheight on the L1 penalty trying to obtain a sparse model.

* Partial Least Squares Regression
  * PLS a cross-decoposition algorithm, performs dimensonality reduction prior to regression, by maximizizing the explained variance of input and predictor matrices in a few so called latent variables. PLS-regression is highly efficient when the number of features extends the number of samples, and when those features are multicollinear. [@cross2020]

* Aritificial Neural Networks (ANN)
  * A Deep Neural Networks (ANN with many layers) can perfrom regression tasks by condensing the neurons in the conected layers to a single output neuron, predicting the response variables value. A residual loss function like mean squared error or huber loss is used to adjust the wheights of up to millions of neurons in each iteration. The training iterations consisting of forward and backward passes are called an epoch. After a certain amount of epoches the loss function reaches a minima or a plateau and no further improvement can be archieved by adjusting the weights. This is also called the vanishing gradient problem [@Hochreiter1998], the weights can get stuck on a plateau, as it is not  simple to find a minimum in multidemensional feature space. Changeing the weights initialization and activation functions as well as using a robust loss function like huber loss to estimate the training erros can result in a more accurate model. Nonlinear relationships can be learned by the use of nonlinear activation functions, leading to different phats through the network depending on the input features. With so many adjustable wheights to extract information about the underlying relationship, nerual networks can make the most accurate prediction on the data at hand.



[@handson8]

### Training on data without external information -  Unsupervised learning

Without labeld data to learn relationships from, information can be extracted by observing  the underlying structure of the data. 
Much can be gained by grouping the samples in a number of clusters using a distance metric (k-means), or by projecting the data on principal component space (PCA dimensionality reduction).


* Principal Component Analysis (PCA)
  * Visualization and Dimensionality reduction by projecting samples onto Principal Component space
* K-means-clustering
  * Grouping samples into a k number of clusters, with max mean center distance. Different strategies and distance meassurers can be used to calculate the space between samples and clusters, trying to find meaningful relationships in multidimensional feature space.


### Modeling the Data
The fewer degrees of freedom a model has, the harder it will be for it to overfit the data. This can be achieved by reducing the number of input-variables by variable selection or perfroming dimensionality reduction.
[@handson8]

![](@attachment/Clipboard_2020-06-11-18-30-23.png)

__Noise__: __Physico-chemical data always contains noise, where the term “noise” is usually reserved for small, fast, random fluctuations of the response.__ The first aim of any scientific experiment is to generate data of the highest quality, and much effort is usually put into decreasing noise levels. Noise can simply be reduced by performing $n$ repeated measurements of a sample, averaging out the variance from unwanted physical properties and random fluctuationsby a factor of $\sqrt{n}$.

[@chemoR]

### Variance Bias
______________
#### Overfitting the Training Data

__Complex models such as deep neural networks can detect subtle patterns in the data, but if the training set is noisy, or if it is too small (which introduces sampling noise), then the model is likely to detect patterns in the noise itself.__
[@handson8]

A model containing more parameters than necessary to learn the fundamental relationships in the data, is prone to suffer from overfitting by learning patterns in the noise. Using out of bag samples, not seen by the model during traing, an estimate on the accuracy of the model can be made. Overfitting can be prevented by reducing the number of features and/or by increasing the sample size.


#### Underfitting the Training Data
Underfitting occures when the model is to simple to learn the underlying relation from the training data to make acurate predictions.
[@handson8]


#### Dealing with Spectral Data

## Multivariate Analysis

_All spectra, from the point of view of a machine learning model, suffers from multicollinearity problems. Multicollinearity in a spectrum means that the signal at one wavelength is highly correlated with the signal at neighbouring wavelengths._

There is no way around some sort of decomposition (removing multicollinearity) when dealing with spectral data. 


_The high correlation makes the mathematical problem of solving a least square regression ill-posed. Simply running a linear least square regression on the raw spectra will fail._

__The trick is to modify the linear regression by introducing regularisation to the least square problem (Lasso regression), or performing dimensionreduction first (PCA) and run linear regression on a few independent variabels.__

## Linear Models and the multicolinearity problem
**
Linear regression is used to estimate a target value from linear combinations of input features. In OrdinaryLeastSquares regression (OLS) the target variable is approximated by minimizing the mean squard error (MSE) loss function on the training data. The coefficients used in the linear model need to be independent, otherwise their variance is too high and predictions are not accurate.
In NIR chemometrics we deal with data containing mostly highly correlated features, and more variables than samples.
This prequisites make OLS regression regression fail, when trying to predict from NIR spectra containg a number of correlated features highly exceeding the number of samples.

One solution is to the select a set of wavelenghts (indepented varaiables) and perform OLS regression on those features. 



## Regularized Linear Models

#### re_summary

Linear models, as well ordinary least squared (OLS) 



__Regularization__ is a form of regression, that constrains/ regularizes or shrinks the coefficient estimates towards zero. In other words, this technique discourages learning a more complex or flexible model, so as to avoid the risk of overfftting.

If there is noise in the training data, then the estimated coefficients won’t generalize well to the future data. This is where regularization comes in and shrinks or regularizes these learned estimates towards zero.

[@Regularization in Machine Learning]

#### Loss Function

The fitting procedure involves a loss function, known as residual sum of squares or RSS. The coefficients are chosen, such that they minimize this loss function.

$$
\mathrm{RSS}=\sum_{i=1}^{n}\left(y_{i}-\beta_{0}-\sum_{j=1}^{p} \beta_{j} x_{i j}\right)^{2}
$$

#### Ridge

$$
\sum_{i=1}^{n}\left(y_{i}-\beta_{0}-\sum_{j=1}^{p} \beta_{j} x_{i j}\right)^{2}+\lambda \sum_{j=1}^{p} \beta_{j}^{2}=\operatorname{RSS}+\lambda \sum_{j=1}^{p} \beta_{j}^{2}
$$

 will shrink the coefficients for least important predictors, very close to zero. But it will never make them exactly zero. In other words, the finnal model will include all predictors.


#### Lasso
$$
\sum_{i=1}^{n}\left(y_{i}-\beta_{0}-\sum_{j=1}^{p} \beta_{j} x_{i j}\right)^{2}+\lambda \sum_{j=1}^{p}\left|\beta_{j}\right|=\operatorname{RSS}+\lambda \sum_{j=1}^{p}\left|\beta_{j}\right|
$$

Lasso is another variation, in which the above function is minimized. Its clear that this variation differs from ridge regression only in penalizing the high coefficients


It uses |βj| (modulus)instead of squares of β, as its penalty. In statistics, this is known as the L1 norm.

in the case of the lasso, the L1 penalty has the effect of forcing some of the coefficient estimates to be exactly equal to zero when the tuning parameter λ is sufficiently large. Therefore, the lasso method also performs variable selection and is said to yield sparse models.


#### Elastic Net
Elastic Net first emerged as a result of critique on lasso, whose variable selection can be too dependent on data and thus unstable. The solution is to combine the penalties of ridge regression and lasso to get the best of both worlds. Elastic Net aims at minimizing the following loss function:

$$
L_{\text {enet }}(\hat{\beta})=\frac{\sum_{i=1}^{n}\left(y_{i}-x_{i}^{\prime} \hat{\beta}\right)^{2}}{2 n}+\lambda\left(\frac{1-\alpha}{2} \sum_{j=1}^{m} \hat{\beta}_{j}^{2}+\alpha \sum_{j=1}^{m}\left|\hat{\beta}_{j}\right|\right)
$$
where α is the mixing parameter between ridge (α = 0) and lasso (α = 1).

#### Penalities


Consider their are 2 parameters in a given problem. Then according to above formulation, the ridge regression is expressed by β12 + β22 ≤ s. This implies that ridge regression coefficients have the smallest RSS(loss function) for all points that lie within the circle given by β12 + β22 ≤ s.
Similarly, for lasso, the equation becomes,|β1|+|β2|≤ s. This implies that lasso coe=cients have the smallest RSS(loss function) for all points that lie within the diamond given by |β1|+|β2|≤ s.

![](@attachment/Clipboard_2020-06-23-11-02-12.png)
_Fig.: The above image shows the constraint functions(green areas), for lasso(left) and ridge regression(right), along with contours for RSS(red ellipse)._

https://tex.stackexchange.com/questions/431483/how-to-draw-lasso-and-ridge

[@Regularization in Machine Learning]




### Dimension Reduction 

Principal components represent a decomposition of the original data into orthogonal directions. In this way the collinearity problem is removed while most of the information present in the original data is preserved.

NIRPY: pca revisited


 The retrieved principal components are independent from one another and can be used to run a  regression.
@nirpy

### Cross-decomposition

Unlike PCA, PLS is a cross-decomposition technique. It derives the latent variables by maximising the covariance between the spectra and the response variable. 
Therefore PLS will ensure that the first latent variables have a good degree of correlation with the response variable. 



### PLS regression

_Cross decomposition algorithms finds the fundamental relations between two matrices ($X$ and $Y$). The so called latent variables approaches to model the covariance structures in these two spaces. They will try to find the multidimensional direction in the $X$ space that explains the maximum multidimensional variance direction in the $Y$ space._

PLS-regression is particularly suited when the matrix of predictors has more variables than observations (as in NIR spectra), and when there is multicollinearity among $X$ values. By contrast, standard regression will fail in these cases.
@scikitlearn - crossdecomposion

In general multivariate PLS, the model for the spectra is written as:

![](@attachment/Clipboard_2020-06-11-19-57-21.png)



$$X = T \times P^T + E$$


* $X$ are initial (or preprocessed) spectra. In total we’ve got m spectra (or samples) and $n$ wavelengths.  If we stack them all up we have a $m×n$ matrix.

* $P$ is the loading matrix, which says how much every wavelength band weighs in in the final model. The number $k$ is the number of components we chose for our PLS regression. Finally note that $P$ has a superscript: $P^t$ just means that we have to transpose the matrix P to make the multiplication work.

* The matrix $T$ is called the scores. Loosely speaking the scores can be interpreted as a measure of how well each sample is described by the model.

* Finally there is an error matrix $E$ , which contains all spectral variations in $X$ that cannot be described by the model.

* A similar model is also built for the response variables, that are the labels used to train the algorithm



The PLS cross decomposition algorithm finds the fundamental relation between the response varible (labels), for instance protein content, and spectra of animal feed.

$Y = U \times Q^T + F$ 

 The PLS model is built in such a way to maximise the covariance between  $T$ and $U$.

the other matrices are analogous to what we described above



### pls wikipedia
-------------------

The general underlying model of multivariate PLS is

$X = T \times P^\mathrm{T} + E$
$Y = U \times Q^\mathrm{T} + F$

X is an n×mn\times m matrix of predictors, Y is an n×pn\times p matrix of responses

T and U: respectively, projections of X (the X score, component or factor matrix) and projections of Y (the Y scores)

P and Q are  orthogonal loading matrices

E and F are the error terms
----------------------

# Variable Selection


