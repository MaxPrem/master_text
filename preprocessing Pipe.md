---
title: preprocessing Pipe
created: '2020-05-07T15:50:07.477Z'
modified: '2020-05-07T15:58:21.356Z'
---

# preprocessing Pipe

```python

from ChemUtils import EmscScaler, GlobalStandardScaler, SavgolFilter


# scale y
yscaler = GlobalStandardScaler()
y_scaled = yscaler.fit_transform(y)

# Extensive Multiplicative Scattercorrection

pipeline = Pipeline([
    ("scaleing_X", GlobalStandardScaler()),
    ("scatter_correction", EmscScaler()),
    ("smmothing", SavgolFilter())
])

X_pipe = pipeline.fit_transform(X)


with plt.style.context(('ggplot')):
    plt.plot(wl, X_pipe.T)
    plt.xlabel('Wavelength (nm)')
    plt.ylabel('D2 Absorbance')
    plt.show()
```
