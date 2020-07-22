---
title: convnet
created: '2020-05-07T08:05:37.410Z'
modified: '2020-06-02T08:05:36.175Z'
---

# convnet

What if I told you that there’s a layer you can use as a drop-in replacement for Conv2D that will make your model lighter (fewer trainable weight parameters) and faster (fewer floating-point operations) and cause it to perform a few percentage points bet- ter on its task? 

 This layer performs a spatial convolution on each channel of its input,independently, before mixing output channels via a pointwise convolution (a 1 × 1 convolution), as shown in figure 7.16.
  **This is equivalent to separating the learn- ing of spatial features and the learning of channel-wise features, which makes a lot of sense if you assume that spatial locations in the input are highly correlated, but differ- ent channels are fairly independent**.
  
   It requires significantly fewer parameters and involves fewer computations, thus resulting in smaller, speedier models. And because it’s a more representationally efficient way to perform convolution, it tends to learn better representations using less data, resulting in better-performing models.

   **These advantages become especially important when you’re training small models from scratch on limited data. For instance, here’s how you can build a lightweight, depthwise separable convnet for an image-classification task (softmax categorical clas- sification) on a small dataset:**

# skicitlearn
# depthwise separable convolution (SeparableConv2D layer)

Note that it’s highly likely that regular convolutions will soon be mostly (or com- pletely) replaced by an equivalent but faster and representationally efficient alterna- tive: the depthwise separable convolution (SeparableConv2D layer). This is true for 3D, 2D, and 1D inputs. When you’re building a new network from scratch, using depth- wise separable convolutions is definitely the way to go. The SeparableConv2D layer can be used as a drop-in replacement for Conv2D, resulting in a smaller, faster network that also performs better on its task.
Here’s a typical image-classification network (categorical classification, in this case):

```python
model = models.Sequential() 
model.add(layers.SeparableConv2D(32, 3, activation='relu',
                                input_shape=(height, width, channels))) 

model.add(layers.SeparableConv2D(64, 3, activation='relu'))
model.add(layers.MaxPooling2D(2))

model.add(layers.SeparableConv2D(64, 3, activation='relu')) 
model.add(layers.SeparableConv2D(128, 3, activation='relu'))
model.add(layers.MaxPooling2D(2))

model.add(layers.SeparableConv2D(64, 3, activation='relu')) 
model.add(layers.SeparableConv2D(128, 3, activation='relu')) 
model.add(layers.GlobalAveragePooling2D())

model.add(layers.Dense(32, activation='relu')) 
model.add(layers.Dense(num_classes, activation='softmax'))

model.compile(optimizer='rmsprop', loss='categorical_crossentropy')
``` --
