---
title: finetune params
created: '2020-06-03T20:12:07.278Z'
modified: '2020-06-03T20:12:49.776Z'
---

# finetune params

#Fine-Tuning Neural Network Hyperparameters
The flexibility of neural networks is also one of their main drawbacks: there are many hyperparameters to tweak. Not only can you use any imaginable network architec‐ ture, but even in a simple MLP you can change the number of layers, the number of neurons per layer, the type of activation function to use in each layer, the weight 

def build_model(n_hidden=1, n_neurons=30, learning_rate=3e-3, input_shape=[8]): model = keras.models.Sequential()
options = {"input_shape": input_shape}
for layer in range(n_hidden):
model.add(keras.layers.Dense(n_neurons, activation="relu", **options))
options = {} model.add(keras.layers.Dense(1, **options)) optimizer = keras.optimizers.SGD(learning_rate) model.compile(loss="mse", optimizer=optimizer) return model
