---
attachments: [Clipboard_2020-08-10-21-59-11.png, Clipboard_2020-08-10-21-59-28.png, Clipboard_2020-08-10-22-00-14.png, Clipboard_2020-08-10-22-00-23.png]
tags: [masterarbeit]
title: Summary edited
created: '2020-08-02T17:22:28.223Z'
modified: '2020-08-11T08:33:19.250Z'
---

# Summary edited


In this thesis we present and demonstrate methods to overcome the difficulties associated with analyzing NIR spectra. A combination of regularized regression and dimension reduction referred to as (ElasticNet-PartialLeastSquares) EN-PLS can overcome the multicollinearity problem from neighbouring wavelengths. PLS creats a sparse model robust to overfitting from the non zero coefficietns of the preceding variable selection step. Another more modern approach utilizes deep convolutional neural networks (CNN), known for their outstanding ability to analyze and predict from spatial data such as pictures and spectra. Booth approaches can result in models with high predictive power, but each comes with a drawback.

The CNN creates a model with higher accuracy but is less interpretable. Millions of adjustable weights simulate the process that generate the data in a black box model. The backpropagation algorithm estimates errors from the labeld data to tune these parameters in a direction that minimize the prediction error. The training continues till the loss function converges, i.e. a minimum is reached.

The EN-PLS model on the other hand is more interpretable, unraveling the uninformative spectra, selecting chemically relevant regions and displaying wavelengths of importance. The approach can also result in highly accurate predictions, but needs more prerequisites to effectively perform variable selection and dimension reduction without incorporating too much noise in the model.

One of these prerequisites is to preprocess the NIR spectra in order to remove unwanted physical artefacts from diffuse reflectance messurements.
Additive and multiplicative effects from reflections on surfaces of solids and powders, appears in the form of varying baselines, slopes, intensities and other random fluctuations.
Scatter correction algorithms, smoothing filters and other mathematical transformations as mean-centering and derivatization improve the general signal to noise ratio. The order in which these functions are applied can greatly influence the outcome of a regression analysis. Although, heavy preprocessing can amplify noise and leads to overfitting. 

The CNN performs best on slightly preprocessed spectra, but the aim is to generate more data to train on. Dataaugmentation is used to simulate expected noise from diffuse reflectance meassurements and scatter correciton is applied in the next step to remove these again. The result is 100 slightly different spectra from one meassurement. During training Backpropagation tunes the weights of all the layers in a direction that reduces the total loss. The resulting trained visual layers perform effektive preprocessing to remove noise and to extract features for the following fully connected layers.

Elatic Net's regularized regression uses the traditionally preprocessed spectra to select a sparse set of wavelengths. The algorithm benefits from its ability to seamlessly combine lassos and ridges L1 and L2 penalties. The mostly dominant L1 penalty shrinks the coefficients of uninformative wavelengths to 0. This minimizes the sum of absolute values from the regression coefficients and results in a sparse selection. The L2 penalty, on the other hand minimizes the sum of squared coefficients. This causes shrinkage in some of the coefficients close to zero but performs no variable selection.

Elastic nets optimal mixing parameter is calculated with cross-validation.
Conventional lasso regression (CV enets $\alpha = 1$) removes up to 98% of the wavelenghts, if some wavelengths are equally importat they are selected randomly.  The combination of L1 and L2 penalty in elastic net can overcome this difficulty and leads to a sparse selection of groups of equally important variables. The selected set of variables becomes more reproduceable. 


In the second step of EN-PLS, dimension reduction is performed by cross decomposition on the set of informative wavelengths and the response variable used for regression. The algorithm creats so called latent varaibles that explain most of the variance found in the X and Y data matrices. These are orthogonal linear combinations that form a lower dimensional space in attempts to conserve the structure of the multidimensional data. These latent variables are formed in a way, that explain most of the variance the first component. If more than two components are used for regression, overfitting is more likely as PLS incorporates more noise in the model.

The comparison of EN-PLS and CNN shows that both methods can make highly accurate predictions. The CNN results in a model with higher accuracy, but the EN-PLS can make comparatively good predictions if the labelled data is of high quality. One should use the two methods according to the task. 
EN-PLS delivers a better interpretation about the underlying relationship in the data, however, if the goal is the make accurate predictions from unknown samples from NIR-spectroscopy then the CNN should be used.



