---
tags: [masterarbeit]
title: Summary
created: '2020-07-21T17:14:04.412Z'
modified: '2020-08-10T20:11:04.926Z'
---

# Summary


In this thesis we present and demonstrate methods to overcome the difficulties associated with analyzing NIR spectra.
A combination of regularized regression and dimension reduction referred to as (ElasticNet-PartialLeastSquares) EN-PLS can overcome the multicollinearity problem from neighbouring wavelengths. A sparse model robust to overfitting is created by PLS regression on the non-zero coefficients. Another more modern approach utilizes deep convolutional neural networks (CNN), known for their outstanding ability to analyze and predict from spatial data such as pictures and spectra. Booth approaches can result in models with high predictive power, but each comes with a drawback.

The CNN creates a model with higher accuracy but is less interpretable, as it acts as a blackbox model trying to emulate the process that generates the data by adjusting millions of weights. Being able to learn from labeled data by adjusting the parameters in a direction that minimize the prediction error in a process called backpropagation.

The EN-PLS model on the other hand is more interpretable, unraveling the uninformative spectra, selecting chemically relevant regions and displaying wavelengths of importance. The approach can also result in highly accurate predictions, but needs more prerequisites to effectively perform variable selection and dimension reduction without incorporating too much noise in the model.

One of these prerequisites is to preprocess the NIR spectra in order to remove unwanted physical artefacts obtained from measuring in diffuse reflectance. The resulting additive and multiplicative effects from reflection on surfaces of solids and powders appear in the form of varying baselines, slopes, intensities and other random fluctuations. The objective is to improve the general signal to noise ratio, by using scatter correcting algorithms, smoothing filters and mathematical transformations as mean-centering and derivatization. The order in which these functions are applied can greatly influence the outcome of a regression analysis. Preprocessing the spectra too heavily can blow up noise and leads to overfitting.
The CNN performs better on slightly preprocessed spectra, but the aim is to generate more data by creating relevant to be expected noise in a process called dataaugmentation. The convolutional layers then learn effektive preprocessing from the spectra by tuning the parameters through backpropagation. 

Using the preprocessed spectra, a sparse selection of wavelengths can be obtained by elasticnets regularized regression. The algorithm benefits from its ability to seamlessly combine lassos and ridges L1 and L2 penalties. 

While the mostly dominant L1 penalty shrinks the coefficients of uninformative wavelengths to 0, minimizing the sum of absolute values from the regression coefficients, is the L2 penalty responsible for selecting equally important variables from groups of highly correlated ones.

Depending on the crossvalidation result of elasticnets mixing parameter, variable selection can result in a removal of up to 98% of the wavelengths, by performing conventional lasso regression ($\alpha$ = 1).


Adding the L2 penalty ($\alpha < 1$) can lead to more reproducible results by selecting small groups, as equally important variables from regions are selected randomly by lasso. $alpha = 0$ 



In the second step of EN-PLS, dimension reduction is performed by cross decomposition on the set of informative wavelengths and the response variable used for regression.

The algorithm is trying to explain most of the variance found in the data matrices by creating so called latent variables. 
That are orthogonal linear combinations forming a lower dimensional space trying to conserve the structure of the multidimensional data.

PLS suffers from incorporating randomly correlating variables resulting from noise when forming these components, especially when more than two components are used to create a model. 

The reduction of uninformative variables prior to dimension reduction makes it possible to explain most of the chemical information in just two components, resulting in a model that makes accurate predictions on unseen test data.

Comparing the results of EN-PLS and CNN, both methods can make highly accurate predictions. 

The CNN results are always better in a higher accuracy, but the EN-PLS can make comparatively good predictions if the labeled data is of high quality. 
One should use the two methods according to the task. Understanding and interpreting the data can be done better by performing EN-PLS. Is the goal to make accurate predictions from unknown samples scanned with the NIR-spectroscopy analyzer, the CNN should be used.



