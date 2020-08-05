---
tags: [masterarbeit]
title: 5 Discussion
created: '2020-06-17T14:40:00.427Z'
modified: '2020-07-31T14:33:36.096Z'
---

# 5 Discussion



### Robust Models

A robust model will predict unseen data more accurately because it is less likely to be affected by noise(to model the noise). This is why an PLS model with the lowest RMSE and the highest R2 is not always the best model.


#### Methods to obtain robust models in NIR spectroscopy:
* Spectral preprocessing: remove random Noise by smoothing, baseline by derivatisation

* Variable Selection: selecting a few bands from the spectra, can greatlty reduce the models complexity, bands containing noise from the atmospheric CO2 ... should always be removed.

* Outlier Removal: removing faulty spectra as well as meassurement erros,

* Regularization:
 PLS regression with more than 2-3 components starts overfitting,

* Elasticnet regression: self regularization 

DeepNets: DropOut makes the neighboured weights more likely to have relevant information, test & val set help to prevent overfiting,
backprogration ...

### Spectral preprocessing



__Preprocessing__ is essential to reduce the variance caused by messurement effects as particle size and surface light scattering effects.

Piplene shows high variance regions in the spectra, cutting away...

picutures
* full spec
* full spec 2nd deriv
* cut spc 0 deriv prp
* cut spc 2nd



### Elastic Net Variable Selection
The effectiveness of variable selection greatly depends
* on the correlation of the response variable with the spectra,
* the undertaken signal processing steps,
* and the region of the spectra selected.

If all the requirements are met, ElasticNet can reduce the number of wavelenghts used for calibration by 97-98%.



Varaible selection performs better on spectra without 2nd order Dev.
as noise is ofen amplifeid


 it tends to select one variable form a correlated group. 




### Variable selection

Variable selection when performed right will result in a smaller, robuster model focusing on information rich regions of the spectra.

As variable selection is a computationally expensive procedure, runtime can be greatly improved by removing atmospheric peaks and noise edges in advance.

2nd order deriv pic
discussion????
A model for protein prediction in wheat with selected wavelengths can explain over 95% of the variance with just 2 components opposed to 5-6 components needed without variable selection.

Models with variable selection do not always perform in higher R2 or lower RMSE when performing crossvalidation,

(4) Although the accuracy of MLR is greatly increased by feature selection, MLR accuracy is still not better than the accuracy of full-spectrum PLS regression.
(5) No combination of PLS regression and feature selection has led to a prediction accuracy close to that of non-linear methods, e.g., artificial neural network (ANN).

[Variable selection in near-infrared spectroscopy: Benchmarking of feature selection methods on biodiesel data]

When the EN regression is mean‐centered only, variables with large variance are more likely to be selected, irrespective of the information content. Scaling causes the EN selection to be based upon a measure of the correlation with y. If high‐variance noisy variables are present in a data set, the EN‐PLSS/C method is likely to avoid selecting such variables, while other PLS‐based methods will often fail at this basic yet essen- tial task.
[Using elastic net regression to perform spectrally relevant variable selection]



##########################

