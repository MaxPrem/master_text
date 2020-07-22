---
attachments: [Clipboard_2020-06-09-12-17-28.png, Clipboard_2020-06-09-12-28-31.png, Clipboard_2020-06-14-19-48-44.png]
pinned: true
tags: [masterarbeit]
title: Multivariate Analysis in NIR Spectroscopy
created: '2020-06-09T09:39:07.203Z'
modified: '2020-07-20T16:53:31.892Z'
---

# Multivariate Analysis in NIR Spectroscopy 

# 1 Abstract

### Summary NIR Chemometrics

Near-infrared spectroscopy (NIRS) is a high-throughput, low-cost, solvent-free, and nondestructive analytical tool. 


In Chemoetrics machinelearning and singal transformation methods are applied to process and correlate spectra (or other instrumental data) with measureable phisical properties and sample qualities, to gain insights and relevant information. 


## 1 Introduction

The aim of my thesis is to develop state of the art workflows and tools for the analysis of NIR spectra at _ the institute of animal nutrtion_ - TTE Boku. The goal is to obtain robust regression models on __lab-meassurements vs. NIR spectra__,  to predict spectra of unknown samples confidently.

* Rashmon: the multiplicitoy of good models;
* Occam: the conflict between simplicity and accuracy;
* Bellman: dimensionality curse or blessing;
[@Breiman2001]

Unfortonately, in prediction, accuracy and simplicity (interpretability are in conflict. 

*the Occam Dilemma)accuray genreally requires more complex predictoin kethods. Simple and inerpretable fucntions do note make the most accuraet predictors.

If the goad is interpretability, gaining information about the model , or accuracy on the relation between predictors and response variables.

For this task two workflows were developed, 
* a classical linear model approach using Partial Least Squares Regression!!! with preceding variable selection(regularized reg.) and spectral preprocessing,
* as well a nonlinear-regression model using Convolutional-Neural-Networks, a deep neural network architecture highly effective for analyzing visual data.

* a data model approch combining regularized linear regression for variable selection and partial least square regression for dimension reduction on the selected wavelenghts to create a sparse model.


The deep learning approach will (always) result in a model with higher precision and more robustness to outliers, at the cost of a more complex model. 
That is harder to interprete.


PLS regression, a much simpler algorithm prone to overfitting, can yield highly accurate models as well, though an effektive combination of spectral-preprocessing steps has to be found. The disadvantag of finding the optimal pre-treatments, can be outweighted by having a smaller and easier to interprete model, according to Occams's Razor.

_“All else being equal, simpler models should be favored over more complex ones.”_
__"interpretation vs prediction"__

Still, if no satisftying model can be obtained by PLS regressioun, due to bad data or other difficulties like finding an informative set of wavelenghts, one can try to make a prediction by using the self-optimizing Convolutional Neural Network.


## History & Background

Initially described in the literature in 1939, NIRS was first applied to agricultural products in 1968 by Karl Norris and co-workers. They discoverd absorption bands from wheat kernels in the near infrared regions of spectra and concluded that specific regions can be used to predict protein content, moisture and other properties.

[@whitepaper]

### Fourier TF NIR ft-NIR

Fourier Transformation was already known in the beginning of the 18th century. Technical Innovation and progress in computer hardware, lead to the development of FT-NIR devices. Makeing it possible to simultaneously meassures a wide spectral range, resulting in faster meassurements with higher signal-noise ratio. Making NIR spectroscopy a feasible solution to a wide range of practical applications.


### Applications of NIR spectroscopty

NIR spectroscopy found many applications in different fields



* in biotechnology the use of  NIR spectra is investigated to montior media , metabolit content and biomass in fermentation processes.
 [Spectroscopy in Biotechnology Research and Development]

* in the medical field NIR is used to monitor....

* __In the agrifood sector, the potential of NIRS have been widely investigated, this is a very powerful tool that provides meaningful information about internal and external properties of fruits, such as sugar content, total acidity, pH, soluble solid content, dry matter, firmness, and bruises, to mention some [36].__

 Moreover, NIRS can be applied to a wide variety of problems such as determination of particle size [38], determination of the best harvesting time [37], and investigation of geographical origin of foods such as apples, meat, and cheese [39].
[@Lopez2017]

### Advantages

When dealing with large sample sizes for chemical analysis or online process quality control, NIR spectroscopy can save resources and time. Assesing multible parameter without losing sample in one meassurement provides a big advantage over wet lab analysis.
 This gives producers and nutritionists better capabilities to monitor variability in crude materials and end products.

### Drawbacks

__Because it is a comparative analytical method, NIRS is a secondary, or indirect method based on regression against a primary or reference method.__ Consequently, a NIR prediction can never be more accurate than the primary reference method. __Every reference method has limits to its applicability and associated error.__ These limitations and errors must be understood and quantified to decide what degree of analytical error should be attributed to the NIRS prediction model versus the reference chemistry.

[@Sapienza2008]


<img src=@attachment/Clipboard_2020-06-11-19-27-46.png width = 500>

_Figure 4. Scheme for the construction of a quantitative model._


## NIR Spectra

__In vibrational spectroscopy, near-infrared spectroscopy (NIRS) covers the transition from the visible spectral range to the mid-infrared region. The NIR spectral region ranges from 800 to 2500 nm (12,500–4000 cm−1) with absorptions representing overtones and combinations mainly associated with –CH, –OH, –NH, and –SH functional groups [1].__


_[1] Ozaki Y. Near-infrared spectroscopy—its versatility in analytical chemistry. Analytical Sciences: the International Journal of the Japan Society for Analytical Chemistry. 2012;28:545–563. DOI: 10.2116/analsci.28.545._

![](@attachment/Clipboard_2020-06-09-12-17-28.png)

### IR-Messbereiche
• Nahes Infrarot (NIR): 15.000 cm-1 – 4000 cm-1
„Obertöne“ 2. bzw. 3. Ordnung (schwach), niederenergetische d-d Übergänge
• Mittleres Infrarot (MIR): 4000 cm-1 – 600 cm-1
Streck- und Winkeldeformationsschwingungen von C-H, C-C und
• Fernes Infrarot (FIR): 600 cm-1 – 10 cm-1
Streck- und Winkeldeformationsschwingungen von Schweratomen, Gerüst-, Torsions- und Ringdeformationsschwingungen

### Measurement

By orientation, NIR instruments are of two main types: reflectance and transmittance. For a reflectance NIR instrument, the detector is located on the same side of the sample as the light source so the NIR light is reflected off of the sample. For transmission instruments, the detector is placed on the opposite side of the sample from the light source so the light is transmitted through the sample (Figure 2).


Nir spectra can be obtained by meassuring in reflectance or transmittance mode, depending on the location of the detector. Portable and labsized instruements mainly operate in diffuse reflectance mode to obtain spectra, as the sample simply needs to be placed on a surface for meassurement. The improvements of scatter correcting algorithms and computer hardware, further reduced meassured noise from physical properties as particle size, makeing diffuse reflectance a widely used method.



![](@attachment/Clipboard_2020-06-09-12-28-31.png)


Measurements by NIRS procedures are sensitive to the physical properties of the sample which affect the transmission and reflectance of light. Included among these properties are the physical shape and grind size of the sample particles, independent of whether the means of sample presentation is a ring cup, optical quartz Petri dish, or a natural product cell that uses fresh, undried, unground samples. [Nirs White Paper]


Sample preparation and presentation to the NIR instrument varies widely. Though dried, finely ground samples are often employed, whole grains or fresh, unground samples also can be scanned. Instruments can be stationary in a laboratory or mobile (e.g. on a silage chopper).
[@Sapienza2008]


