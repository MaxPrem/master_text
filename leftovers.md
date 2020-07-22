---
tags: [masterarbeit]
title: leftovers
created: '2020-06-14T15:46:36.403Z'
modified: '2020-06-14T15:47:02.749Z'
---

# leftovers



 ### DataAugmentation


Instead of correction of the baseline variations we use a special implementation of data augmentation. The idea is to simulate the expected form of irrelevant noise (here baseline offset and slope and overall spectrum intensity), and expect the neural network to either extract features robust to the variations, or figure out the best corrections during training. This way we can make more efficient use of the labelled dataset. The idea is similar to the image rotations and croppings done in image recognition training.




The fat blue line is the original spectrum and the others are the modified ones. Lets apply this to all the spectrums and expand the dataset with a factor of 100. I've found that the offset and multiplication works OK around 10% of the standard deviation for the whole dataset. The slopeshift is set to half of this. This could vary depending on the dataset and may be worth experimenting with.

gen...

As an alternative to a fixed size augmented dataset, Keras can also use generator objects, which generates batches "on the fly", solving memory problems and giving even larger augmented datasets. Checkout the code at https://github.com/EBjerrum/SMILES-enumeration to see an example from another data domain I have been experimenting with.

