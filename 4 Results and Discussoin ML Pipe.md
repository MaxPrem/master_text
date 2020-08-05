---
attachments: [Clipboard_2020-07-22-12-44-35.png, Clipboard_2020-07-22-12-46-11.png, Clipboard_2020-07-22-12-46-17.png, Clipboard_2020-07-22-12-47-21.png, Clipboard_2020-07-22-12-48-27.png, Clipboard_2020-07-22-12-48-33.png, Clipboard_2020-07-22-12-48-39.png, Clipboard_2020-07-22-12-48-45.png, Clipboard_2020-07-22-19-53-26.png, Clipboard_2020-07-22-19-53-43.png, Clipboard_2020-07-22-19-53-57.png, Clipboard_2020-07-22-19-59-34.png, Clipboard_2020-07-22-19-59-42.png, Clipboard_2020-07-22-19-59-54.png, Clipboard_2020-07-22-21-19-17.png, Clipboard_2020-07-22-21-19-25.png, Clipboard_2020-07-22-21-19-34.png, Clipboard_2020-07-22-21-19-41.png, Clipboard_2020-07-22-21-19-48.png, Clipboard_2020-07-22-21-19-53.png, Clipboard_2020-07-22-21-28-17.png, Clipboard_2020-07-22-21-28-21.png, Clipboard_2020-07-22-21-28-33.png, Clipboard_2020-07-22-21-28-56.png, Clipboard_2020-07-22-21-29-43.png, Clipboard_2020-07-22-21-29-51.png, Clipboard_2020-07-22-21-30-32.png, Clipboard_2020-07-22-21-31-47.png, Clipboard_2020-07-22-21-45-47.png, Clipboard_2020-07-22-21-45-51.png, Clipboard_2020-07-22-21-45-56.png, Clipboard_2020-07-22-21-46-00.png, Clipboard_2020-07-22-21-46-08.png, Clipboard_2020-07-22-21-46-12.png, Clipboard_2020-07-23-15-05-04.png, Clipboard_2020-07-23-15-05-11.png, Clipboard_2020-07-23-15-05-20.png, Clipboard_2020-07-23-15-07-51.png, Clipboard_2020-07-23-15-08-10.png, Clipboard_2020-07-23-15-08-21.png, Clipboard_2020-07-23-15-11-18.png, Clipboard_2020-07-23-20-52-17.png, Clipboard_2020-07-23-20-52-24.png, Clipboard_2020-07-23-20-52-30.png, Clipboard_2020-07-23-20-55-57.png, Clipboard_2020-07-23-20-56-05.png, Clipboard_2020-07-23-20-56-11.png, Clipboard_2020-07-23-20-56-30.png, Clipboard_2020-07-23-20-56-34.png, Clipboard_2020-07-23-20-56-39.png, Clipboard_2020-07-24-00-48-21.png, Clipboard_2020-07-24-00-48-34.png, Clipboard_2020-07-24-00-48-41.png, Clipboard_2020-07-24-00-48-48.png, Clipboard_2020-07-24-00-48-58.png, Clipboard_2020-07-24-00-49-04.png, Clipboard_2020-07-24-00-58-06.png, Clipboard_2020-07-24-00-58-14.png, Clipboard_2020-07-24-00-58-24.png, Clipboard_2020-07-24-00-58-32.png, Clipboard_2020-07-24-01-02-50.png, Clipboard_2020-07-24-01-02-54.png, Clipboard_2020-07-24-01-09-52.png, Clipboard_2020-07-24-01-10-01.png, Clipboard_2020-07-24-01-10-14.png, Clipboard_2020-07-24-01-10-19.png, Clipboard_2020-07-24-20-45-29.png, Clipboard_2020-07-24-20-45-57.png, Clipboard_2020-07-24-23-38-18.png, Clipboard_2020-07-24-23-39-02.png, Clipboard_2020-08-02-21-20-01.png, Clipboard_2020-08-02-21-20-12.png, Clipboard_2020-08-02-21-25-02.png, Clipboard_2020-08-02-21-27-23.png, Clipboard_2020-08-02-21-29-56.png, Clipboard_2020-08-02-22-06-27.png, Clipboard_2020-08-02-22-06-34.png, Clipboard_2020-08-02-22-39-08.png, Clipboard_2020-08-02-22-39-24.png, Clipboard_2020-08-03-23-26-41.png, Clipboard_2020-08-03-23-26-50.png, Clipboard_2020-08-03-23-28-11.png, Clipboard_2020-08-03-23-29-34.png, Clipboard_2020-08-03-23-30-33.png, Clipboard_2020-08-03-23-32-33.png, Clipboard_2020-08-03-23-33-45.png, Clipboard_2020-08-05-01-27-18.png, Clipboard_2020-08-05-01-30-03.png]
favorited: true
pinned: true
tags: [masterarbeit]
title: 4 Results and Discussoin ML Pipe
created: '2020-06-14T14:13:25.756Z'
modified: '2020-08-05T11:31:21.628Z'
---

# 4 Results and Discussoin ML Pipe


<img src=@attachment/Clipboard_2020-06-11-19-27-46.png width = 500>

## Preprocessing-Pipeline Results

Signal preprocessing is an essential part and one oft the most important steps in NIR spectra analysis. It can lead to robust models with high accuracy, but can also result in overfitting by incorporating more noise into the model.

The effect of different derivatives in the preprocessing-pipeline are shown below on the full spectra, the other standard parameters lead to good results.

First the NIR spectra are scaled using the GlobalStandardScaler(), next scattering artefacts from meassureing in diffuse-reflectance mode are corrected using the ExtendedMultiplicativeScattercorrectionScaler().
In the last step using the Savitzky-Golay filter, high frequency noise is smoothed using a polynomial fit function (OLS), and low frequenzy noise in the from of varrying baselines and slopes can be reduced by using differentiation, on a adjustable windowsize. The size of the window influences the smoothing degree, as more points are generalised together. The combination of this two transformations in one step make Savitzky-Golay a highly popular algorithm in signal processing. 


```python

# sklearn Pipline containing preprocessing steps
  pipe = Pipeline([
      ("scaleing_X", GlobalStandardScaler()),
      ("scatter_correction", EmscScaler()),
      ("smmothing", SavgolFilter(window_size = 12, polyorder=2, deriv=0)),
  ])

# train and test spectra are pre-processed with the fit_transform and transform method
  pipe.fit_transform(X_train)
  pipe.transform(X_test)
```


#### Untreated Spectra
The varrying baseline is one of the first things noticed when observing the untreated spectra. The regions only containing random fluctuations form 10000  $cm^{-1}$ to  8000 $cm^{-1}$ are also clearly visible.
<img src=@attachment/Clipboard_2020-07-22-12-46-11.png width = 450><img src=@attachment/Clipboard_2020-07-22-12-46-17.png width = 450>

#### Pipeline transormed Spectra: Dev = 0
The effects of the multiplicative scatter correction algorithm, correcting baselineshift and varrying slopes to some extend, and the polynomial smoothing of the SavGol filter in the next step result in more interpretable spectra. Note that no derivatisation is performed, as the parameter is set to 0. The aligned spectra now show regions with high variance, making random noise and fluctuations at the edges clearly distinguishable from chemically related variations.

<img src=@attachment/Clipboard_2020-07-22-12-44-35.png width = 450><img src=@attachment/Clipboard_2020-07-22-12-47-21.png width = 450>
By compareing the two achses of the spectra the effects of mean centering and standardizing the data becomes visible. The cut out spectra is centered at a different region, as it is containing less wavelenghts with lower absorbance.

#### Pipeline transormed Spectra: Dev = 1
The first derivative spectra from savgol filtering, show stronger features with high variance and varrying slope. The spectra were baseline adjusted by derivatisation and almost set to the same center for full and cut-out spectra. The high noise region in the full spectra should be removed prior to regression, as the amplification of random fluctuations would reduce overall predictability of the model. 

<img src=@attachment/Clipboard_2020-07-22-12-48-27.png width = 450><img src=@attachment/Clipboard_2020-07-22-12-48-33.png width = 450>

#### Pipeline transormed Spectra: Dev = 2
The strong amplification of random fluctuations in the noise is first noticed when looking at the full spectra. The drawback of derivatisation becomes obvious as noise now dominates the spectra. On the other hand, the region containing structured variance is now easily distinguishable, making high derivatives useful for deciding where to cut off the edges of the specra.
The feature rich region containing peaks now looks overamplified, as smaler peaks apear in the flanks of the taler ones.

<img src=@attachment/Clipboard_2020-07-22-12-48-39.png width = 450><img src=@attachment/Clipboard_2020-07-22-12-48-45.png width = 450>

## Variable Selection

Multivartiate data as chemometrics spectra contain thousands of variables, most of which are uninformative, redundant and highly correlated. The spectra shown are always the same and crude protein (XP) is used as a response variable for regularized regression, except for one example using acid detergent fiber (ADForg). 
ElasticNets mixing parameter $\alpha$ is evaluated using crossvalidation prior to variable selection.

## ElasticNet Variable Selection Results

The effects of different crossvalidated values for $\alpha$ are shown here. $\alpha$ is not only affected by the shape of the spectra but also by the number of samples used for regression. Most of the time the variable selection is reproducable but, results varry if a larg test set is generated and the regularized regression performs worse on a smaller trainings dataset. The variable selection also takes longer to perform or even fails, if the correlation with the response variable is not verry high.

```python

# sklearn Pipline containing preprocessing steps
  pipe = Pipeline([
      ("scaleing_X", GlobalStandardScaler()),
      ("scatter_correction", EmscScaler()),
      ("smmothing", SavgolFilter(window_size = 12, polyorder=2, deriv=0)),
      ("variable_selection", EnetSelect())
  ])

# train and test spectra are pre-processed with the fit_transform and transform method
  pipe.fit_transform(X_train, y_train)
  pipe.transform(X_test)
```


### 0 Derivative Spectra - $\alpha$ = 1.0
Elastic nets cross validated tuning parameter $\alpha$, mixing L1 and L2 ratio results in a conventional lasso regression. The variable selection seems to be effective as the atmospheric peak mostly containing noise around 5200 $cm^{-1}$ is ignored and a sparse selection of 18 wavelenghts is obtained. 

The feature importance bar plot shows the effect of pure lasso regression. Only single variables are selected from highly correlated groups (see wavenumbers in plot). Most wavelengths are selected arount 4400 $cm^{-1}$ and the wavelength with the highest correlation to the reference method is selected at 4872 $cm{-1}$.

<img src=@attachment/Clipboard_2020-07-23-15-07-51.png width = 450><img src=@attachment/Clipboard_2020-07-22-21-45-51.png width = 450>

Optimal l1_ratio: 1.0
Number of iterations 6143
R2: 0.982
18 features selected, reduction of 97.43%

### 0 Derivative Spectra  - $\alpha$ = 0.995

These variable selection plots are obtained from regularized regression on the same spectra using ADForg as response variable. It is interesting to see that the small amount of L2 regularization leads to more variables selected in groups, although the number of selected wavelengths stays the same. 
The variable importance bar plot indicates that the right hand side of the spectra contains more relevant information to predict the fiber content. This is due to different locations in the spectra for N-H overtones and O-H overtones.  

<img src=@attachment/Clipboard_2020-08-03-23-33-45.png width = 450><img src=@attachment/Clipboard_2020-08-03-23-26-50.png width = 450>


Optimal l1_ratio: 0.995
Number of iterations 3292
R2: 0.9409686056672426
18 features selected, reduction of 97.43%



### 1. Derivative Spectra - $\alpha$ = 1.0

Elastic Net variable selection of the 1 derivative spectra seems to be focused on regions with steep and varrying slopes mostly in the flanks of the transformed peaks. 

The feature importance barplot shows a sparse collection of 16 wavelengths, with single wavelengths selected left and right of the center of the amplified peaks.


<img src=@attachment/Clipboard_2020-07-23-15-11-18.png width = 450><img src=@attachment/Clipboard_2020-07-22-21-46-00.png width = 450>


__Optimal l1_ratio: 1.0__
Number of iterations 8173
R2: 0.9787823305171468
14 features selected, reduction of 98.00%

### 1. Derivative Spectra - $\alpha$ = 0.5

The mix ratio of elastic net results in an equal L1 and L2 ratio, leading to groups of selected variables from highly variable regions. The value for $\alpha$ was obtained from crossvalidation on a smaller trainigset for regularized regression. Compared to the set of variables selected from conventional lasso regression now whole regions between previously single peaks are selected. The barplot shows only 30 wavelenghts but 153 got selected, showing more wavelengths of equal importance than previously.


<img src=@attachment/Clipboard_2020-07-24-20-45-57.png width = 450><img src=@attachment/Clipboard_2020-07-24-20-45-29.png width = 450>

Optimal l1_ratio: 0.5
Number of iterations 3185
R2: 0.973934034975289
153 features selected, reduction of 78.17%

### 2. Derivative Sepctra: $\alpha$ = 0.01

The strong feature transformation of the 2nd derivative results in more randomly selected wavelenghts, as variance over the whole spectra gets amplified. The previosly ignored noisy region around 5300 $cm^{-1}$ contains now selected wavelenghts and the region around 4850 $cm^{-1}$ with most variables selcted in the previous variable selction contains now no selected wavelengths at all.
Regions around 4900 $cm{^-1}$ ignored by 0 dev, and relatively low ranked in  the 1 dev spectra, now dominated the influence of the 2 dev spectra.

<img src=@attachment/Clipboard_2020-07-23-15-08-21.png width = 450><img src=@attachment/Clipboard_2020-07-22-21-46-12.png width = 450>

__Optimal l1_ratio: 0.01__
Number of iterations 2427
R2: 0.9868291336609326
583 features selected, reduction of 16.83%

Interesting is the effect of the 2nd order derivative on the variable selection method.

 Elasticnet crossvalidation of the mixing parameter, performing conventional lasso regression on 0 dev. spectra before, now favors ridge regression on the strongly deformed spectra. 
 The reason for this is that before most information could be extracted from a few wavelenghts. Now with the effect of derivatisation, variation all over the spectra got amplified leading no more to a sparse optimal solution from regularized regression.

The amplification of higly correlated regions led to a higher l2 penalty ratio for regularized regression, as lasso is not able to select a high number of variables from intercorrelated groups.

## Validating Regression models

Estimating a models accuracy and predictive power is an essential step when deciding between similar models or the optimal number of latent variables. It is not recomended to validate the model on the data used for training. Methods like cross-validation or leave-one-out crossvalidation are popular methods for doing so, but they are blind to overfitting. The most relyable and recomended approach is to use test data not seen by the model during training. Cross-validation can be used on the training and test data to get a better estimation. In some cases the crossvalidated results perform much worse. This can be due to unfavorable splits from small datasets, giving samples not perfektly fitting the population a high leverage. To adjust this, one can increase test set size, risking a worse trained model, or by reducing the number of splits for cross-validation. Not all metrics are affected by crossvalidation with smaller sample sizes the same way, so no need to reduce the traingset too much.

### PLS vs EN-PLS

The following results compare PLS and EN-PLS regression on the same preprocessed spectra, focusing on the cut out region from 5500 to 4100 cm$^{-1}$. The number of training samples used for variable selection is reduced as a bigger test set for effective cross-validation is needed. 
Prior to regression an optimised number of latent variables for dimension reduction needs to be choosen.

The score plot ,the higher the better, showing variance-explained and the loss plot, lower is better, showing MSECV on train and test data can help in doing so. One should always consider the amount of additonal information gained from each component. A minima on the loss plot is not the best choice for choosing the optimal number of components.

Models can be best compared by takeing a closer look at the benchmark table, especially the cross-validated part. The challenge is to find a number of latent variables that generalises well on traing and test data. 
Using variable selction prior to dimension reduction should result in a model needing fewer latent variables to explain the same amount of variance, as less noise is incorporated into the first few components.

With an overall small sample size, crossvalidation results can vary strongly on the amount of train/test data used (see the 95% confidence intervall), especially scores like variance explained suffer from to litte test data. In addition 10-fold crossvalidation fails when the number of samples is to small for the number of splits. If the number of samples is to small to calculate the  cross-validation score or metric the value "nan ± nan" is printed instead. In this case one can either increase the number of samples or reduce the number of cross-validation splits.

Function used to create regression summary:

```python
# function definition
def cv_benchmark_model(X, y, X_test, y_test, model, y_unscaled, ref, **kwargs):
	"""Final Output Function for pls regression"""
	# get name of reference method for outputtable
	print_nir_metrics(X, y, X_test, y_test, model, y_unscaled, ref)
	print_regression_benchmark(X, y, X_test, y_test, model)
	# print cross-validation table
	print_cv_table(X, y, X_test, y_test, model)

# dictionary containg train and test data
data_en0 = {"X": X_train_0, "y": y_train, "X_test": X_test_0, "y_test": y_test}
# function call
cv_benchmark_model(**data_en0, y_unscaled=y, ref=ref, model=model_0)

```

### 0 Derivative Spectra: 

When compareing the score and the loss plots, it can be seen that the model with selected variables generalises better on training and test data, especially by just using 2 components. In many cases 2 latent variables is the desired number, with more components selected, the model tends to overfitt the data. This can also be observed by compareing loss or explained variance from train and test data. While the results on the training data improve with more latent variables (more noise gets explained leading to higher scores), the test data suffers from the model overfitting the training data. 

It can also be seen that the full spectra PLS model is better at explaining the training data, this is due to the strength of PLS explaining the variance at hand. PLS strength is also its weakness, as some portion of the variance is derived from noise. This makes EN-PLS so effektive combinig the strenghts of the two algorithms. Elasticnet is great at selecting sources of informative variance, but does not come close at to PLS's ability to find a hyperdimensional plane finding the direction of maximum variance.

<table>
<tr>
<th>
PLS
</th>
<th>
EN-PLS
</th>
</tr>

<tr>
<td>
<pre>
*** Summary Reference Method: XP [gXP/kgTM] ***
Number of latent variables: 4
Number of wavelengths: 701
Number of training sampels: 55
Number of test sampels: 24
*** NIR Metrics ***
Standard Error Calibration (SEC): 	10.9
Standard Error Prediction (SEP): 	7.25
Standard Error CV (SECV): 	6.774 ± 0.374
Relative prediction deviation (RPD): 	7.33
Scores   	train		test 
R2       	0.943		0.982
MSE      	0.0567	0.0188
RMSE     	0.238		0.137
Huber    	0.0272	0.0093
   CV Scores   train                    test    
Variance expl.:0.964 ± 0.058     0.921 ± 0.132
R2:            0.957 ± 0.062      0.88 ± 0.16
Huber Loss:    0.017 ± 0.018     0.017 ± 0.022
MSE:           0.034 ± 0.036     0.034 ± 0.046
RMSE:          0.175 ± 0.112     0.173 ± 0.132
Mean ± 95`%` confidence interval 10-fold CV.
</pre>
</td>
<td>
<pre>
*** Summary Reference Method: XP [gXP/kgTM] ***
Number of latent variables: 2
Number of wavelengths: 24
Number of training sampels: 55
Number of test sampels: 24
*** NIR Metrics ***
Standard Error Calibration (SEC): 	10.4
Standard Error Prediction (SEP): 	7.21
Standard Error CV (SECV): 	6.76 ± 0.375
Relative prediction deviation (RPD): 	7.57
Scores   	train		test 
R2       	0.942		0.974
MSE      	0.0575	0.0277
RMSE     	0.24		0.166
Huber    	0.0275	0.0136
   CV Scores   train              test    
Variance expl.:0.961 ± 0.026     0.942 ± 0.136
R2:            0.954 ± 0.03       0.84 ± 0.27
Huber Loss:    0.019 ± 0.012     0.018 ± 0.028
MSE:           0.039 ± 0.024     0.037 ± 0.058
RMSE:          0.194 ± 0.064     0.174 ± 0.166
Mean ± 95`%` confidence interval 10-fold CV.
</pre>
</td>
</tr>

<tr>
<td>
<pre>


</pre>
</td>
<td>
<pre>



</pre>
</td>
</tr>
</table>


<img src=@attachment/Clipboard_2020-07-24-00-48-21.png width = 450><img src=@attachment/Clipboard_2020-07-24-00-48-41.png width = 450>

<img src=@attachment/Clipboard_2020-07-24-00-48-34.png width = 450><img src=@attachment/Clipboard_2020-07-24-00-48-48.png width = 450>
<img src=@attachment/Clipboard_2020-07-24-00-48-58.png width = 450><img src=@attachment/Clipboard_2020-07-24-00-49-04.png width = 450>


### 1 Derivative Spectra:

With a smaller training sample size, due to more test samples needed for crossvalidation, the performence of the variable selection method suffered from more variables with equal importance to choose from, resulting in a higher L1 penalty favoring ridge regression. Not only did it fail to generate a sparse model as ridge regression started to take over, it also performes worse compared to the model using the whole selected spectral range. Suggesting that selecting variables from 1 Derivative spectra is more difficult compared to only smoothed spectra. The reason is that the noise also gets amplified, and overfitting occures due to a too small sample size.

The score plot on the test data is also more unstable, suggesting that more noise got incorporated into the first latent variables, compared to the 0 Derivative spectra.

<table>
<tr>
<th>
PLS
</th>
<th>
EN-PLS
</th>
</tr>

<tr>
<td>
<pre>
*** Summary Reference Method: XP [gXP/kgTM] ***
Number of latent variables: 5
Number of wavelengths: 701
Number of training sampels: 55
Number of test sampels: 24
*** NIR Metrics ***
Standard Error Calibration (SEC): 	11.1
Standard Error Prediction (SEP): 	7.25
Standard Error CV (SECV): 	6.79 ± 0.373
Relative prediction deviation (RPD): 	7.17
Scores   	train		test 
R2       	0.926		0.989
MSE      	0.0739		0.0121
RMSE     	0.272		0.11
Huber    	0.0351		0.00596
   CV Scores   train                    test    
Variance expl.:0.959 ± 0.066      0.94 ± 0.098
R2:            0.951 ± 0.088     0.894 ± 0.13
Huber Loss:    0.018 ± 0.012     0.014 ± 0.018
MSE:           0.036 ± 0.024     0.028 ± 0.036
RMSE:          0.187 ± 0.064     0.157 ± 0.116
Mean ± 95`%` confidence interval 10-fold CV.

</pre>
</td>
<td>
<pre>
*** Summary Reference Method: XP [gXP/kgTM] ***
Number of latent variables: 4
Number of wavelengths: 576
Number of training sampels: 55
Number of test sampels: 24
*** NIR Metrics ***
Standard Error Calibration (SEC): 	10.9
Standard Error Prediction (SEP): 	7.22
Standard Error CV (SECV): 	6.786 ± 0.373
Relative prediction deviation (RPD): 	7.29
Scores   	train		test 
R2       	0.941		0.986
MSE      	0.0586		0.0143
RMSE     	0.242		0.12
Huber    	0.0281		0.00707
CV Scores      train                test        
Variance expl.:0.961 ± 0.05      0.926 ± 0.138
R2:            0.953 ± 0.062     0.881 ± 0.16
MSE:           0.037 ± 0.024     0.031 ± 0.04
RMSE:          0.189 ± 0.06      0.165 ± 0.122
Huber Loss:    0.018 ± 0.012     0.015 ± 0.02
Mean ± 95`%` confidence interval 10-fold CV.
</pre>
</td>
</tr>
</table>

<img src=@attachment/Clipboard_2020-07-24-00-58-06.png width = 450><img src=@attachment/Clipboard_2020-07-24-00-58-14.png width = 450>


<img src=@attachment/Clipboard_2020-07-24-00-58-24.png width = 450><img src=@attachment/Clipboard_2020-07-24-00-58-32.png width = 450>



### 2 Derivative Spectra:

Regression on 2nd order derivatized spectra results in overfitted models, that fail to generalise well on test data. The EN-PLS algorithm performs worse than the full spectra PLS regression, due to elastic nets difficulties to select significant wavelenghts from the amplified features.
<table>
<tr>
<th>
PLS
</th>
<th>
EN-PLS
</th>
</tr>

<tr>
<td>
<pre>
*** Summary Reference Method: XP [gXP/kgTM] ***
Number of latent variables: 2
Number of wavelengths: 701
Number of training sampels: 55
Number of test sampels: 24
*** NIR Metrics ***
Standard Error Calibration (SEC): 	10.7
Standard Error Prediction (SEP): 	6.98
Standard Error CV (SECV): 	6.775 ± 0.374
Relative prediction deviation (RPD): 	7.27
Scores   	train		test 
R2       	0.964		0.981
MSE      	0.0356		0.0195
RMSE     	0.189		0.14
Huber    	0.0174		0.00962
   CV Scores   train                    test    
Variance expl.:0.962 ± 0.058     0.811 ± 0.636
R2:            0.956 ± 0.068      0.71 ± 0.656
Huber Loss:    0.017 ± 0.02      0.025 ± 0.032
MSE:           0.035 ± 0.044     0.052 ± 0.068
RMSE:          0.176 ± 0.118     0.213 ± 0.164
Mean ± 95`%` confidence interval 10-fold CV.

</pre>
</td>
<td>
<pre>
*** Summary Reference Method: XP [gXP/kgTM] ***
Number of latent variables: 4
Number of wavelengths: 327
Number of training sampels: 55
Number of test sampels: 24
*** NIR Metrics ***
Standard Error Calibration (SEC): 	11.0
Standard Error Prediction (SEP): 	6.92
Standard Error CV (SECV): 	6.8 ± 0.371
Relative prediction deviation (RPD): 	7.07
Scores   	train		test 
R2       	0.943		0.996
MSE      	0.0575		0.00369
RMSE     	0.24		0.0607
Huber    	0.0276		0.00184
CV Scores      train                test        
Variance expl.:0.967 ± 0.042     0.784 ± 0.772
R2:            0.961 ± 0.038     0.709 ± 0.938
MSE:           0.033 ± 0.032     0.039 ± 0.056
RMSE:          0.176 ± 0.086     0.183 ± 0.146
Huber Loss:    0.016 ± 0.016     0.019 ± 0.026
Mean ± 95`%` confidence interval 10-fold CV.
</pre>
</td>
</tr>
</table>

<img src=@attachment/Clipboard_2020-07-24-01-09-52.png width = 450><img src=@attachment/Clipboard_2020-07-24-01-10-01.png width = 450>

<img src=@attachment/Clipboard_2020-07-24-01-10-14.png width = 450><img src=@attachment/Clipboard_2020-07-24-01-10-19.png width = 450>


## PLS Variable selection
Another method implemented is PLS variable selection. Opposed to elastic net, their is no regularization parameter shrinking coefficients during regression.
The function performs pls regression up to the given number of components. For each model, the coefficients are sorted and deleted one at a time, until the loss function reaches a minimum. This procedure is repeated for different numbers of selected latent variables.

This algorithm performes poorly compared to elastic net variable selection,

* it is prone to select variables form noise,
* the runtime scales verry poorly with the size of the input spectra, as wavelengths are deleted in a nested loop for each component after sorting, making the process computational expensive
* it can not create sparse models by selecting single variables from groups of correlated variables as elasticnet does.


<table>
<tr>
<th>
PLS 2 components
</th>
<th>
PLS 20 components
</th>
</tr>

<tr>
<td>
<pre>
*** Summary Reference Method: XP [gXP/kgTM] ***
Number of latent variables: 2
Number of wavelengths: 215
Number of training sampels: 55
Number of test sampels: 24
*** NIR Metrics ***
Standard Error Calibration (SEC): 10.7
Standard Error Prediction (SEP): 7.35
Standard Error CV (SECV): 6.748 ± 0.369
Relative prediction deviation (RPD): 7.56
Scores    train   test
R2        0.964   0.967
MSE       0.0364  0.0344
RMSE      0.191   0.185
Huber     0.0175  0.0169
CV Scores   train           test
Var.expl.:  0.967 ± 0.046   0.85 ± 0.356
R2:         0.961 ± 0.046   0.794 ± 0.39
MSE:        0.032 ± 0.038   0.044 ± 0.044
RMSE:       0.17  ± 0.12    0.201 ± 0.116
Huber Loss: 0.016 ± 0.018   0.021 ± 0.022
Mean ± 95% confidence interval 10-fold CV.
</pre>
</td>
<td>
<pre>
*** Summary Reference Method: XP [gXP/kgTM] ***
Number of latent variables: 3
Number of wavelengths: 147
Number of training sampels: 55
Number of test sampels: 24
*** NIR Metrics ***
Standard Error Calibration (SEC): 10.8
Standard Error Prediction (SEP): 7.35
Standard Error CV (SECV): 6.769 ± 0.374
Relative prediction deviation (RPD): 7.34
Scores      train   test
R2          0.951   0.979
MSE         0.0488  0.0223
RMSE        0.221   0.149
Huber       0.0237  0.011
CV Scores   train            test
Var.expl.:  0.962 ± 0.04     0.861 ± 0.432
R2:         0.955 ± 0.048    0.674 ± 1.332
MSE:        0.036 ± 0.022    0.039 ± 0.046
RMSE:       0.187 ± 0.058    0.187 ± 0.13
Huber Loss: 0.018 ± 0.01     0.019 ± 0.022
Mean ± 95% confidence interval 10-fold CV.
</pre>
</td>
</tr>

<tr>
<td>
<pre>

![](@attachment/Clipboard_2020-08-05-01-27-18.png)
Optimised number of PLS components:  2
Wavelengths to be discarded 486
Optimised MSEP 0.0354
</pre>
</td>
<td>
<pre>

![](@attachment/Clipboard_2020-08-05-01-30-03.png)
Optimised number of PLS components:  14
Wavelengths to be discarded 531
Optimised MSEP 0.0208
</pre>
</td>
</tr>
</table>


￼
## Outlier Removal

### Summary Outlier Metrics
An example workflow to remove outliers is presented as follows.

Since we are working with labeld data, we are going to use all information available, spectra and reference method values to identify outliers. The two metrics estimating each samples fit to the model's underlying distribution are Q-residuals and Hotteling's T-squared distance.

#### Q-residuals
The Q-residuals are obtained by PLS regression from the response variable equation $Y = U \times Q^T + F$. The matrix describes the variation not explained by the obtained model and also depends on the number of components selected. We are using a 95% confidence intervall to decide if a value qualifies as an outlier.

#### Hotteling's T-squared distance
The Hotteling's T-squared distance is a metric meassureing a sample's fit described by the model, with a score of 0 defining a perfect fit.

### Results Outlier removal

We are analyzing a data set containing a few outlier using the same spectra as before. The reference method containing outlier is  crude ash (XA), a gravimetically meassured value describing a samples anorganic fraction.

First we calculate the optimal number of components with crossvalidation from the already preprocessed data.
```
mse_minimum(X_train, y_train)
```

![](@attachment/Clipboard_2020-08-02-21-20-12.png)

Next we performe PLS regression with the determined number of components.

```
pls_regression(X_train_0, y_train, 6)
```


![](@attachment/Clipboard_2020-08-02-21-25-02.png)

Now we initalise our Outlier class. Select the number of components to fit the pls model, and plot the resulting distribution.
``` python
rem_outlier = Outlier()
rem_outlier.fit(X = X_train_0, y = y_train, n_comp = 6)
rem_outlier.plot(X_train_0, y_train)
```


The plot shows two samples defined as outliers by the two metrics in the right corner. Some more samples could be outliers according to the q-residuals. The function will measure the MSE in a new model for each Outlier removed and stores the optimal numbert.

![](@attachment/Clipboard_2020-08-02-22-39-08.png)

By calling the fit_transform or transform method the MSE error is calculated iteratively for each samples removed, and the model with lowest MSE defines the number of samples removed. Sometimes no samples are removed, since the overall result is not improving.

We save the results in variables named X_rem, y_rem and plot the new distribution. 
Another set of samples classifies as Outliers according to the Q-residuals, but the algorithm keeps the samples as there is no improvemnet in the models accuracy by removing more samples. This indicates that Q-residuals alone is not a good meassurer to identifiy outliers, but in combination with Hotteling's T square Outliers not fitting the underlying data can be removed.

This method fails, if the variance in the data is to high from unpreciese reference methods. Data

```
X_rem, y_rem = rem_outlier.fit_transform(X_train_0, y_train, max_outlier = 25)
rem_outlier.plot(X_rem, y_rem)
```

![](@attachment/Clipboard_2020-08-02-21-29-56.png)
5 outlier were removed, as removing more samples did not lead to a lower MSE.

![](@attachment/Clipboard_2020-08-02-22-06-27.png)
Plotting the curve for MSE per component, we can see on the y-scale that our MSE is sligtly lower, over the whole range of components.

![](@attachment/Clipboard_2020-08-02-22-39-24.png)




