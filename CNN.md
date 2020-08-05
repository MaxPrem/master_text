---
attachments: [Clipboard_2020-08-03-11-40-51.png, Clipboard_2020-08-03-11-42-29.png, Clipboard_2020-08-03-11-43-14.png, Clipboard_2020-08-03-11-44-27.png, Clipboard_2020-08-03-11-45-24.png, Clipboard_2020-08-03-11-45-45.png, Clipboard_2020-08-03-17-50-34.png, Clipboard_2020-08-03-17-50-42.png, Clipboard_2020-08-03-17-50-52.png, Clipboard_2020-08-03-18-49-56.png, Clipboard_2020-08-03-18-50-02.png, Clipboard_2020-08-03-18-50-10.png, Clipboard_2020-08-03-18-50-22.png]
pinned: true
tags: [masterarbeit]
title: 4.3 Results Comparison EN-PLS/CNN
created: '2020-08-03T09:29:06.380Z'
modified: '2020-08-03T21:20:43.665Z'
---

## 4.3 Results Comparison EN-PLS/CNN

We are compareing the best EN-PLS model from the previous results section, with a Deep Learning model from a convolutional neural network.

### Results Protein XP

When compareing the score and the loss plots, it can be seen that the model with selected variables generalises better on training and test data, especially by using just 2 components, which is the recomended minimal amount to perform multivariate regression. In many cases 2 latent variables is the desired number, the more components are used, the model tends to overfitt the data. This can also be observed by compareing loss or explained variance from train and test data. While the results on the training data improve with more latent variables (more noise gets explained leading to higher scores), the test data suffers from overfitting the training data. 

<table>
<tr>
<th>
EN-PLS
</th>
<th>
CNN
</th>
</tr>

<tr>
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
MSE      	0.0575		0.0277
RMSE     	0.24		0.166
Huber    	0.0275		0.0136
   CV Scores   train                    test    
Variance expl.:0.961 ± 0.026     0.942 ± 0.136
R2:            0.954 ± 0.03       0.84 ± 0.27
MSE:           0.039 ± 0.024     0.037 ± 0.058
RMSE:          0.194 ± 0.064     0.174 ± 0.166
Huber Loss:    0.019 ± 0.012     0.018 ± 0.028
Mean ± 95`%` confidence interval 10-fold CV.
</pre>
</td>
<td>
<pre>
*** Summary Reference Method: XP [gXP/kgTM] ***
Number of wavelengths: 1951
Number of training sampels: 47
Number of test sampels: 16
Number of validation sampels: 16
*** NIR Metrics ***
Standard Error Prediction (SEP): 	4.84
___Benchmarks___
Scores   	train		test 		 val 
Var.expl.	0.96		0.965		0.95
R2       	0.953		0.965		0.943
MSE     	0.0465	0.0239	0.044
RMSE     	0.216		0.154		0.21
Huber    	0.0225	0.0117	0.0208
___MC dropout benchmarks___
Scores   	train		test 		 val 
Var.expl. 0.961	  0.966		0.951
R2       	0.954		0.966		0.944
MSE      	0.0462	0.0235	0.0431
RMSE     	0.215	  0.153		0.208
Huber    	0.0224	0.0115	0.0204
Mean form 100 MC- Dropout predictions.
</pre>
</td>
</tr>

<tr>
<td>
<pre>

<img src=@attachment/Clipboard_2020-08-03-11-40-51.png width = 450>
</pre>
</td>
<td>
<pre>

<img src=@attachment/Clipboard_2020-07-30-11-01-33.png width = 480>




<tr>
<td>
<pre>

<img src=@attachment/Clipboard_2020-08-03-11-45-24.png width = 450>
</pre>
</td>
<td>
<pre>

<img src=@attachment/Clipboard_2020-08-03-11-45-45.png width = 480>



</pre>
</td>
</tr>
</table>

Not all metrics can be compared one by one as cross validation is too computational expensive for deep learning.
To estimate uncertainty 100 MC-Dropout predictions were averaged for the score and loss functions. Also for  deep learning, we splitted the test data in half to create a validation datast not seen by the model during training/back_propagation. 


It is satisfying to see that the EN-PLS model and the CNN are of compareable accuracy. They perform almost equally well on explaining the variance found in the training data. As expected is the DNN generalising better on test and validation data.
Furthermore it is even more difficult to obtain high scores on variance explained and R2-score for smaller datasets, as outliers have a stronger influence. The data used for modeling contains no outlier and can almost be becompletely explained by booth models.

This is also a problem when performing cross validation. The splits of the already too small dataset can result in negative values or Nan (not a number). This can be adjusted by reducing the number of splits, or if possible by increasing the test set size.


The PLS hyperparameter were calculated by crossvalidation to find the lowest mse for test and trainings data.
The trainings data wasn't seen by the PLS model during training, but was added to the score plot to see if the model generalises well or starts to overfitt strongly.

After compareing validation tables for a different number of components, the 2 component model was selected as it had overall the beter scores and regression metrics.

This is due to the fact, that PLS starts to overfitt with more than two components selected. This becomes visible when calculating the training data scores and losses with crossvalidation or by compareing the NIR metric functions (SEP, SEC, SECV, RPD)


The training dataset is big enough for the splits to return valid results and always favors the 2 component model. The not crossvalidated scores and losses may look better with more components, but they are to optimistic, because they were calculated from the training data.

If the 2 component model is of compareable accuracy, it should always be preferred as it generalises better on unseen data.

The CNN neural network was trained for about 50 epoches on the training and test data, used to finetune the weights. The validation samples were set aside to give a better comparision with the PLS test data. Overall accuracy is high for all datasets. 


## Results ADForg
Lets Compare a dataset with higher variance, containg meassurements for acid detergent fiber describing the indigestible fraction of dietary fibre in anaimal feedstock.
Also here the results for booth models are explaining the data verr well. The model could not cv predict R2 score and Variance explained due to inhomogenity in the test sets splits from crossvalidation. One could either increase test set size or decrease the number of splits. With the overall small samplesize we do not want to reduce the samples for training the network any further, indicating that more labeld samples are needed when the variance in the data is high.

<table>
<tr>
<th>
EN-PLS
</th>
<th>
CNN
</th>
</tr>

<tr>
<td>
<pre>
*** Summary Reference Method: ADForg [gADF/kgTM]]  ***
Number of latent variables: 2
Number of wavelengths: 18
Number of training sampels: 55
Number of test sampels: 24
*** NIR Metrics ***
Standard Error Calibration (SEC): 	10.6
Standard Error Prediction (SEP): 	6.69
Standard Error CV (SECV): 	6.595 ± 0.692
Relative prediction deviation (RPD): 	10.8
Scores   	train		test 
R2       	0.905		0.953
MSE      	0.0953		0.0475
RMSE     	0.309		0.218
Huber    	0.0442		0.023
CV Scores      train                test        
Variance expl.:0.923 ± 0.054    -0.378 ± 4.41
R2:            0.919 ± 0.054    -0.443 ± 4.494
MSE:           0.075 ± 0.064     0.063 ± 0.092
RMSE:          0.267 ± 0.126     0.237 ± 0.166
Huber Loss:    0.035 ± 0.028      0.03 ± 0.042
Mean ± 95`%` confidence interval 10-fold CV.
</pre>
</td>
<td>
<pre>
*** Summary Reference Method: ADForg [gADF/kgTM]]  ***
Number of wavelengths: 1951
Number of training sampels: 56
Number of test sampels: 19
Number of validation sampels: 4
*** NIR Metrics ***
Standard Error Prediction (SEP): 	4.49
___Benchmarks___
Scores   	train		test 		 val 
Var.expl. 0.953		0.874		0.817
R2       	0.951		0.827		0.801
MSE      	0.0491	0.083		0.225
RMSE     	0.222		0.288		0.474
Huber    	0.0238	0.0392	0.0981
___MC dropout benchmarks___
Scores   	train		test 		 val 
Var.expl. 0.954	  0.872		0.816
R2       	0.951		0.828		0.8
MSE      	0.0486	0.0825	0.226
RMSE     	0.221		0.287		0.475
Huber    	0.0236	0.039		0.0984
Mean form 100 MC- Dropout predictions.

</pre>
</td>
</tr>

<tr>
<td>
<pre>

<img src=@attachment/Clipboard_2020-08-03-11-40-51.png width = 450>
</pre>
</td>
<td>
<pre>

<img src=@attachment/Clipboard_2020-07-30-11-01-33.png width = 480>




<tr>
<td>
<pre>

<img src=@attachment/Clipboard_2020-08-03-11-45-24.png width = 450>
</pre>
</td>
<td>
<pre>

<img src=@attachment/Clipboard_2020-08-03-11-45-45.png width = 480>



</pre>
</td>
</tr>
</table>

## Results Protein B

Protein B is a solveable fraktion of the protein found in animal feed stock. The analysis is more error-prone and contains many outliers, overshadowing the true distribution. The small sample size makes it diffiult for the models to generalise well on unseen data, indicating that more labeld data is needed from this reference method to obtain stable predictions.


<table>
<tr>
<th>
EN-PLS
</th>
<th>
CNN
</th>
</tr>

<tr>
<td>
<pre>
*** Summary Reference Method: ProteinB ***
Number of latent variables: 2
Number of wavelengths: 61
Number of training sampels: 55
Number of test sampels: 24
*** NIR Metrics ***
Standard Error Calibration (SEC): 	9.7
Standard Error Prediction (SEP): 	6.33
Standard Error CV (SECV): 	6.687 ± 0.951
Relative prediction deviation (RPD): 	8.36
Scores   	train		test 
R2       	0.455		0.715
MSE      	0.545		0.338
RMSE     	0.738		0.581
Huber    	0.192		0.142
CV Scores      train                test        
Variance expl.:0.355 ± 1.21     -0.729 ± 3.032
R2:            0.302 ± 1.196    -0.776 ± 2.974
MSE:           0.467 ± 0.428     0.711 ± 1.078
RMSE:          0.665 ± 0.318     0.792 ± 0.58
Huber Loss:    0.183 ± 0.156     0.261 ± 0.338
Mean ± 95`%` confidence interval 10-fold CV.
</pre>
</td>
<td>
<pre>
*** Summary Reference Method: ProteinB ***
Number of wavelengths: 1951
Number of training sampels: 46
Number of test sampels: 25
Number of validation sampels: 8
*** NIR Metrics ***
Standard Error Prediction (SEP): 	5.57
___Benchmarks___
Scores   	train		test 		 val 
Var.expl.	0.781		0.578		0.657
R2       	0.777		0.488		0.102
MSE      	0.223		0.363		1.08
RMSE     	0.473		0.602		1.04
Huber    	0.0959	0.143		0.371
___MC dropout benchmarks___
Scores   	train		test 		 val 
Var.expl.	0.779		0.571		0.663
R2       	0.774		0.481		0.122
MSE      	0.226		0.368		1.06
RMSE     	0.475		0.606		1.03
Huber    	0.0969	0.145 	0.364
Mean form 100 MC- Dropout predictions.
</pre>
</td>
</tr>

<tr>
<td>
<pre>

<img src=@attachment/Clipboard_2020-08-03-18-49-56.png width = 450>
</pre>
</td>
<td>
<pre>

<img src=@attachment/Clipboard_2020-08-03-18-50-10.png width = 480>




<tr>
<td>
<pre>

<img src=@attachment/Clipboard_2020-08-03-18-50-02.png width = 450>
</pre>
</td>
<td>
<pre>

<img src=@attachment/Clipboard_2020-08-03-18-50-22.png width = 480>



</pre>
</td>
</tr>
</table>

Although none of the models can explain the data perfectly the CNN can deal better with the many outliers. One of the reasons is that the huber loss function scales down the effect of outliers, another reason is the iterative nature of the training. The best model is found by trial and error, opposed to PLS objective to find the direction explaining most of the variance in X and y.
Also important to note is that the PLS plot shows CV R2, while the CNN plot shows R2. These meassures can not be compared directly, as R2 will alwats be more optimistic than cross-validated estimate.

Also here the score plots suggest a higher number of components for the EN-PLS model, but the additional variance explained by more components also models noise and can lead to overfitting. 

As in most cases the two component system generalises better on unseen data and leads to better results in the validation table. The curve for the test data in the validation plot looks unstable. This is caused by a too small sample size, leading to unfavorable splits during cross validation. Still the tow curves show the same minima.

The reason that the 2 component system performs so well compared to more components is defenitely variable selection, enabeling PLS to focus on variance related to chemical information in the first two components. PLS regression alone without preceding variable selction can result in higher trainig scores (if more components are used) but will most likely always overfit and generalise worse on unseen test data. It will also explain more variance linked to noise in the first two components, as this is the main drawback of regular PLS regression.

