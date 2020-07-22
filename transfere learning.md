---
title: transfere learning
created: '2020-05-18T22:06:15.474Z'
modified: '2020-05-18T22:10:31.015Z'
---

# transfere learning

First, you need to load model A, and create a new model based on the model A’s lay‐ ers. Let’s reuse all layers except for the output layer:
```python


model_A = keras.models.load_model("my_model_A.h5")
model_B_on_A = keras.models.Sequential(model_A.layers[:-1])
model_B_on_A.add(keras.layers.Dense(1, activation="sigmoid"))
```
Note that model_A and model_B_on_A now share some layers. When you train model_B_on_A, it will also affect model_A. If you want to avoid that, you need to clone model_A before you reuse its layers. To do this, you must clone model A’s architecture, then copy its weights (since clone_model() does not clone the weights):
```python
model_A_clone = keras.models.clone_model(model_A)
model_A_clone.set_weights(model_A.get_weights())
```
Now we could just train model_B_on_A for task B, but since the new output layer was initialized randomly, it will make large errors, at least during the first few epochs, so there will be large error gradients that may wreck the reused weights. To avoid this, one approach is to freeze the reused layers during the first few epochs, giving the new layer some time to learn reasonable weights. To do this, simply set every layer’s train able attribute to False and compile the model:

```python 
for layer in model_B_on_A.layers[:-1]: 
  layer.trainable = False

model_B_on_A.compile(loss="binary_crossentropy", optimizer="sgd", metrics=["accuracy"])
```
#You must always compile your model after you freeze or unfreeze layers.

Next, we can train the model for a few epochs, then unfreeze the reused layers (which requires compiling the model again) and continue training to fine-tune the reused layers for task B. After unfreezing the reused layers, it is usually a good idea to reduce the learning rate, once again to avoid damaging the reused weights:

```python

history = model_B_on_A.fit(X_train_B, y_train_B, epochs=4, validation_data=(X_valid_B, y_valid_B))

for layer in model_B_on_A.layers[:-1]: 
  layer.trainable = True
optimizer = keras.optimizers.SGD(lr=1e-4) # the default lr is 1e-3 model_B_on_A.compile(loss="binary_crossentropy", optimizer=optimizer,
metrics=["accuracy"])

history = model_B_on_A.fit(X_train_B, y_train_B, epochs=16,
validation_data=(X_valid_B, y_valid_B))
```

So, what’s the final verdict? Well this model’s test accuracy is 99.25%, which means that transfer learning reduced the error rate from 2.8% down to almost 0.7%! That’s a factor of 4!


