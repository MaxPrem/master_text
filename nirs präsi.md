---
attachments: [Clipboard_2020-05-10-22-36-35.png, Clipboard_2020-05-10-22-36-50.png]
title: nirs präsi
created: '2020-05-10T20:02:50.811Z'
modified: '2020-05-12T15:54:00.144Z'
---

# nirs präsi

# summary nir whitepaper

# introduction nir in carboanalysis

In a vibrational spectroscopy, near-infrared spectroscopy (NIRS) covers the transition from the visible spectral range to the mid-infrared region. The NIR spectral region ranges from 800 to 2500 nm (12,500–4000 cm−1) with absorptions representing overtones and combina- tions mainly associated with –CH, –OH, –NH, and –SH functional groups [1].


Summary
NIR analysis as an analytical technique has a long and credible history. NIR is a secondary method that never can be more accurate than the reference method upon which it is based. Statistically robust prediction models allow for a rapid and repeatable assay procedure for nutritional values that help the livestock industry detect and manage variability in com- position among and within feedstuffs. The cost-effectiveness of NIR analysis allows the total analytical error (sampling and laboratory) to be reduced because a larger number of sub-samples or sequential samples can be assayed with a limited analytical budget than is possible using the more expensive wet chemistry approaches. To enhance trust, nutrition- ists, producers and laboratories are encouraged to communicate more fully and openly so that NIR prediction model and wet chemistry statistics are understood more clearly.

# 2. NIR spectra: characteristic bands of oligosaccharide and polysaccharide


The term “near” in NIR relies on the position of the electromagnetic energy lying next to or **near the visible energy range**. Molecular vibrations in the middle infrared (MIR) range cover absorptions bands between 2500 and 25,000 nm (4000 and 400 cm−1) representing the most intense and simplest bands in the whole infrared range, whereas 

NIR bands arise in the inter- val between 800 and 2500 nm (12,500 and 4000 cm−1) covering absorptions corresponding to overtones and combinations of fundamental vibrations [14]. NIR spectroscopy is concerned with both electronic and vibrational transitions [1]. Bands due to electronic transitions are observed in the NIR region and in general are presented as weak bands. Moreover, bands arising from overtones and combination modes are so-called forbidden transitions. Starting from the diatomic molecule as the simplest vibrating system, described by the harmonic and anharmonic oscillator, the study of more complex substances is referred to as polyatomic molecules [14].


**NIR REGIONS**
The NIR region can be divided into three regions. Region I spans from 800 to 1200 nm (12,500– 8500 cm−1), also known as the “the short-wave NIR region (SWNIR),” “near-NIR region (NNIR),” or “the Herschel region,” represents bands resulting from electronic transitions, overtones, and combinations modes. Region II ranges from 1200 to 1800 nm (8500–5500 cm−1) and covers first overtones of XH (X = C, O, N), stretching vibrations and various types of com- bination modes. Finally, Region III (1800–2500 nm or 5500–4000 cm−1) is a combination mode region. Many applications utilize Regions II and III [1].


Absorptions due to different functional groups, especially –CH, –OH, and –NH, are displayed as molecular overtones and combination vibrations at specific wavebands [15, 16]. NIR spectral data are influenced by a particle size (e.g., ground or powder) and need to be properly cali- brated [17]. In Table 1, the characteristic bands of oligosaccharide and polysaccharide are listed.
NIRS has been used as a fingerprint technique for all kinds of samples (liquids, solids, and semisolids), independently of their nature, relatively simple substances or pure compounds, most times they show broad and overlapping bands, it is impossible to correctly assign the specifically vibrations, and cannot be used for structural determination of a sample [18].


# 4. Applications of carbohydrates analysis by NIRS



# EMSC

The extended multiplicative signal correction (EMSC) preprocessing method allows a separation of physical light-scattering effects from chemical (vibrational) light absorbance effects in spectra from, for example, powders or turbid solutions. It is here applied to diffuse near infrared transmission (NIT) spectra of mixtures of wheat gluten (protein) and starch (carbohydrate) powders, linearized by conventional log(1/T). Without any correction for uncontrolled light scattering variation between the powder samples, these absorbance spectra could give reasonable predictions of the analyte (gluten), but only when using multivariate calibration with a much more complex model than expected. Standard MSC preprocessing did not work for these data at all; it removed too much analyte information. However, the EMSC preprocessing yielded powder spectra that obeyed Beer's Law more or less as if they had been obtained from transparent liquid solutions, apparently by isolating the chemical light absorption from additive, multiplicative, and wavelength-dependent effects of uncontrolled light-scattering variations. The model-based EMSC and its converse, the extended inverted signal correction (EISC), gave rather complete descriptions of the diffuse absorbance spectra and virtually indistinguishable performance in the calibration set and the test set of samples.



```python
#Hyperparameters for the network
DENSE = 128
DROPOUT = 0.5
C1_K  = 8   #Number of kernels/feature extractors for first layer
C1_S  = 32  #Width of the convolutional mini networks
C2_K  = 16
C2_S  = 32
leaky_relu = keras.layers.LeakyReLU(alpha=0.2)
activation=leaky_relu


model = keras.models.Sequential([
    GaussianNoise(0.05, input_shape=(input_dim,)),
    Reshape((input_dim, 1)),
    keras.layers.BatchNormalization(),
    SeparableConv1D(C1_K, (C1_S), padding="same", activation=activation,
     kernel_initializer="he_normal"),
    keras.layers.BatchNormalization(),
    SeparableConv1D(C2_K, (C2_S), padding="same", activation=activation, 
    kernel_initializer="he_normal"),
    keras.layers.BatchNormalization(),
    Flatten(),
    Dropout(DROPOUT),
    keras.layers.BatchNormalization(),
    Dense(DENSE, activation=activation, kernel_initializer="he_normal"),
    keras.layers.BatchNormalization(),
    Dense(1, activation='linear')
])

```


````python
# define loss as class to save treshold when loading model
class HuberLoss(keras.losses.Loss):
    def __init__(self, threshold=2.0, **kwargs):
        self.threshold = threshold
        super().__init__(**kwargs)
    def call(self, y_true, y_pred):
        error = y_true - y_pred
        is_small_error = tf.abs(error) < self.threshold
        squared_loss = tf.square(error) / 2
        linear_loss = self.threshold * tf.abs(error) - self.threshold**2 / 2
        return tf.where(is_small_error, squared_loss, linear_loss)
    def get_config(self):
        base_config = super().get_config()
        return {**base_config, "threshold": self.threshold}

# train model
  history = model.fit(X_train_aug, y_train_aug, epochs = 70, batch_size=16,
            validation_data=(X_test, y_test) , callbacks=[rdlr, custom_stopper,
            tensorboard_cb, checkpoint_cb])

```


```python
#Conv Net:

XP: Nadam 70 epochs
RMSE  Train/Test	0.04	0.30
Huber Train/Test	0.0009	0.0418

XP: 33 epochs
RMSE  Train/Test	0.21	0.36
Huber Train/Test	0.0214	0.0576

# pls with Variable selection

pls_variable_selection(X_sg, y, 21)

100% completed
Optimised number of PLS components:  9
Wavelengths to be discarded 870
Optimised MSEP 0.02001732889692647

R2 calib: 0.995
R2 CV: 0.985
MSE calib: 0.005
MSE CV: 0.015

```


