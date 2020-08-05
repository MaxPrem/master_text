---
title: Mathematical pretreatments
created: '2020-06-24T10:00:15.079Z'
modified: '2020-07-27T21:11:44.735Z'
---

# Mathematical pretreatments


## Preprocessing

Scattering effects can be both additive and multiplicative. Additive effects (such as path length differences) produce a baseline displacement of the spectrum along the vertical axis, while multiplicative effects (particle size for instance)  modify the local slope of the spectrum.

The idea behind scattering corrections is to get rid of all effects that are unrelated to the chemical nature of the sample, but just depend on the sample morphology and the measurement geometry.  So, the idea goes, if we are able to remove these undesirable effects beforehand, we should get a better model for the quantity of interest.

nirpy





• Preprocessing 6.5
– Main goal of the preprocessing stage is to remove variation within the data that does not pertain to the analytical information.

• Typical preprocessing methods
* Baseline Correction
* Mean Centering
* Normalization
* Orthogonal Signal Correction 
* Savitsky-Golay Derivatisation
* Multiplicative Scatter Correction
@presi


## Pipeline

```python
pipeline = Pipeline([
    ("scaleing_X", GlobalStandardScaler()),
    ("scatter_correction", EmscScaler()),
    ("smmothing", SavgolFilter(polyorder=2,deriv=1))
])
```

#### Scaleing:

When variables have been measured in di↵erent units or have widely different scales, we should take this into account. Obviously, one does not want the scale in which a variable is measured to have a large influence on the model: just switching to other units would lead to di↵erent results. One popular way of removing this dependence on units is called autoscaling, where every column xi is replaced by
( xi - yi ) / ^sigmai
In statistics, this is often termed standardization of data; the effect is that all variables are considered equally important.
[chemometricswithr]


The employed scaling methods greatly influence the result of an analysis. One should therefore carefully consider scaling methods ( and  order) to aquire desired results.

 

### Standardization

#### MSC:

Another way to remove scatter effects in infrared spectroscopy is Multiplicative Scatter Correction (MSC, [13,14]). One effectively models the signal of a query spectrum as a linear function of the reference spectrum: 

An obvious reference spectrum may not be available, and then often a mean spectrum is used. This is also the approach in the msc function of the pls package: [Chemometrics with R]

{add picture of 1fst dev spectra}


Scattering artifacts adversely affect infrared reflectance measurements of powders and soils, and extended multiplicative and extended inverse scatter correction (EMSC[1] and EISC[2]) are flexible methods useful for correcting for these artifacts

Conclusions: EMSC and EISC can be used to remove variability in reflectance spectra. The methods can be viewed as filters that parse the information into e.g., chemically related and scattering related variance. The result can be good models[3,5] with corrected spectra that are easily interpretable. However, some work is required by practitioners to optimize the filter parameters.
[@Gallagher2000]


### Baseline Removal:
In some forms of spectroscopy one can encounter a baseline, or “background signal” that is far away from the zero level. 



Infrared spectroscopy, for instance, can lead to scatter effects – the surface of the sample influences the measurement. As a result, one often observes spectral offsets: two spectra of the same material may show a constant difference over the whole wavelength range. This may be easily removed by taking first derivatives (i.e., looking at the differences between intensities at sequential wavelengths, rather than the intensities themselves). Take a look at the gasoline data: [Chemometrics with R]

__we use savgolfiltering__

#### Savgolfiltering
One of the most commonly used and frequently cited filters in chemometrics is the Savitzky- Golay smoothing and differentiation filter.[1] The “savgol” filter is often used as a preprocessing in spectroscopy and signal processing. The filter can be used to reduce high frequency noise in a signal due to its smoothing properties and reduce low frequency signal (e.g., due to offsets and slopes) using differentiation.

[@savgol]

 


