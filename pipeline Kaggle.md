---
title: pipeline Kaggle
created: '2020-05-08T08:16:38.595Z'
modified: '2020-06-03T20:10:54.519Z'
---

# pipeline Kaggle

<https://www.kaggle.com/baghern/a-deep-dive-into-sklearn-pipelines>

## old outcommented code before update

```python
'''pipl;ine'''


import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import scipy.io as sio
import numpy as np

specs = pd.read_csv('./luzrawSpectra/nirMatrix.csv')
lab = pd.read_excel('./luzrawSpectra/labdata.xlsx')

from import_luz import importLuz
X, y_Xp, y_Xl, wl = importLuz(specs, lab)
y = y_Xp

from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.25, random_state=42)
X_train_pipe = X_train

import matplotlib.pyplot as plt
%matplotlib inline

#_ = plt.plot(wl,X_train.T)


from ChemUtils import GlobalStandardScaler


xscaler = GlobalStandardScaler()
"""test could be used on different dataset (diff insturemnt or out of cal....)"""

X_train = xscaler.fit_transform(X_train)
X_test = xscaler.transform(X_test)
X_val = xscaler.transform(X_val)

X_train.mean()

#_ = plt.plot(wl,X_train.T)

# %% markdown
# The differences between spectrums are not changed, but the range is adjusted and the mean moved to zero. Below, we also scale the measured API concentration with another GlobalScaler (Here scikit learns standard scaler would also have worked)
# %% codecell

# scale y
yscaler = GlobalStandardScaler()
y_train = yscaler.fit_transform(y_train)
y_test = yscaler.transform(y_test)
y_val = yscaler.transform(y_val)


from sklearn.preprocessing import RobustScaler
ysacaler = RobustScaler()

y_train = yscaler.fit_transform(y_train)
y_test = yscaler.transform(y_test)
y_val = yscaler.transform(y_val)



def dataaugment(x, betashift = 0.05, slopeshift = 0.05,multishift = 0.05):
    #Shift of baseline
    #calculate arrays
    beta = np.random.random(size=(x.shape[0],1))*2*betashift-betashift
    slope = np.random.random(size=(x.shape[0],1))*2*slopeshift-slopeshift + 1
    #Calculate relative position
    axis = np.array(range(x.shape[1]))/float(x.shape[1])
    #Calculate offset to be added
    offset = slope*(axis) + beta - axis - slope/2. + 0.5

    #Multiplicative
    multi = np.random.random(size=(x.shape[0],1))*2*multishift-multishift + 1

    x = multi*x + offset

    return x

shift = np.std(X_train)*0.1
shift

X_train_aug = np.repeat(X_train, repeats=100, axis=0)
X_train_aug = dataaugment(X_train_aug, betashift = shift, slopeshift = 0.05, multishift = shift)

X_test_aug = np.repeat(X_test, repeats=100, axis=0)
X_test_aug = dataaugment(X_test_aug, betashift = shift, slopeshift = 0.05, multishift = shift) #not needed

y_train_aug = np.repeat(y_train, repeats=100, axis=0) #y_train is simply repeated
y_test_aug = np.repeat(y_test, repeats=100, axis=0) #y_train is simply repeated
#_ = plt.plot(wl,X_train_aug.T)

X_train_aug
X_train_aug.mean()
X_train_aug.std()

X_train_aug
X_train_aug.mean()
X_train_aug.std()

from ChemUtils import Dataaugument, EmscScaler
from sklearn.pipeline import Pipeline




aug_pipline = Pipeline([
    ("scaleing_X", GlobalStandardScaler()),
    ("dataaugmentation", Dataaugument()),
    ("scatter_correction", EmscScaler())
    ])

X_aug = aug_pipline.fit_transform(X_train_aug)
X_pipe_test = aug_pipline.transform(X_train_aug)

#_ = plt.plot(wl, X_train_aug.T)
#_ = plt.plot(wl, X_train_aug.T)

X_aug.mean()
X_aug.std()
X_aug.mean()
X_aug.std()

X_pipe_test.mean()
X_pipe_test.std()
X_pipe_test.mean()
X_pipe_test.std()


from sklearn.preprocessing import RobustScaler



rob_aug_pipline = Pipeline([
    ("rob_scaleing_X", GlobalStandardScaler()),
    ("dataaugmentation", Dataaugument()),
    #("scatter_correction", EmscScaler())
    ])

X_aug = aug_pipline.fit_transform(X_train_aug)
X_pipe_test = aug_pipline.transform(X_train_aug)

#_ = plt.plot(wl, X_train_aug.T)
#_ = plt.plot(wl, X_train_aug.T)

X_aug.mean()
X_aug.std()
X_aug.mean()
X_aug.std()

X_pipe_test.mean()
X_pipe_test.std()
X_pipe_test.mean()
X_pipe_test.std()




y_rob_aug_pipline = Pipeline([
    ("rob_scaleing_X", GlobalStandardScaler()),
    ("dataaugmentation", Dataaugument()),
    #("scatter_correction", EmscScaler())
    ])

y_test_pipe = y_rob_aug_pipline.fit_transform(y_test)

```
