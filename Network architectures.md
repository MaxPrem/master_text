---
title: Network architectures
created: '2020-05-05T06:27:16.895Z'
modified: '2020-05-05T07:54:18.928Z'
---

# Network architectures

Vector data —Densely connected network (Dense layers).
􏰄 Image data—2D convnets.
􏰄 Sound data (for example, waveform)—Either 1D convnets (preferred) or RNNs.
􏰄 Text data—Either 1D convnets (preferred) or RNNs.
􏰄 Timeseries data—Either RNNs (preferred) or 1D convnets.
􏰄 Other types of sequence data—Either RNNs or 1D convnets. Prefer RNNs if data
ordering is strongly meaningful (for example, for timeseries, but not for text).
􏰄 Video data—Either 3D convnets (if you need to capture motion effects) or a combination of a frame-level 2D convnet for feature extraction followed by
either an RNN or a 1D convnet to process the resulting sequences.
􏰄 Volumetric data—3D convnets.

# DENSELY CONNECTED NETWORKS

called densely connected because the units of a Dense layer are connected to every other unit. The layer attempts to map relationships between any two input features; this is unlike a 2D convolution layer, for instance, which only looks at local relationships.
Densely connected networks are most commonly used for categorical data.

**They’re also used as the final classification or regression stage of most networks** . For instance, the convnets covered in chapter 5 typically end with one or two Dense layers, and so do the recurrent networks in chapter 6.They’re also used as the final classification or regres- sion stage of most networks. For instance, the convnets covered in chapter 5 typically end with one or two Dense layers, and so do the recurrent networks in chapter 6.


Remember: **to perform binary classification**, end your stack of layers with a Dense layer with a single unit and a sigmoid activation, and use binary_crossentropy as the loss. Your targets should be either 0 or 1:


```python
from keras import models from keras import layers
model = models.Sequential()
model.add(layers.Dense(32, activation='relu', input_shape=(num_input_features,))) model.add(layers.Dense(32, activation='relu'))
model.add(layers.Dense(1, activation='sigmoid'))
model.compile(optimizer='rmsprop', loss='binary_crossentropy')
```

**To perform single-label categorical classification** (where each sample has exactly one class, no more), end your stack of layers with a Dense layer with a number of units equal to the number of classes, and a softmax activation. If your targets are one-hot encoded, use categorical_crossentropy as the loss; if they’re integers, use sparse_categorical_ crossentropy:

```python
model = models.Sequential()
model.add(layers.Dense(32, activation='relu', input_shape=(num_input_features,))) model.add(layers.Dense(32, activation='relu')) model.add(layers.Dense(num_classes, activation='softmax'))
model.compile(optimizer='rmsprop', loss='categorical_crossentropy')
```

**To perform multilabel categorical classification** (where each sample can have several classes), end your stack of layers with a Dense layer with a number of units equal to the number of classes and a sigmoid activation, and use binary_crossentropy as the loss. Your targets should be k-hot encoded:

```python
model = models.Sequential()
model.add(layers.Dense(32, activation='relu', input_shape=(num_input_features,))) model.add(layers.Dense(32, activation='relu')) model.add(layers.Dense(num_classes, activation='sigmoid'))
model.compile(optimizer='rmsprop', loss='binary_crossentropy')
```

**To perform regression toward a vector of continuous values**, end your stack of layers with a Dense layer with a number of units equal to the number of values you’re trying to predict (often a single one, such as the price of a house), and no activation. Several losses can be used for regression, most commonly mean_squared_error (MSE) and mean_absolute_error (MAE):

```python
model = models.Sequential()
model.add(layers.Dense(32, activation='relu', input_shape=(num_input_features,))) model.add(layers.Dense(32, activation='relu')) model.add(layers.Dense(num_values))
```


