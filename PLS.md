---
deleted: true
tags: [masterarbeit]
title: PLS
created: '2020-06-23T09:27:17.175Z'
modified: '2020-06-23T10:04:42.326Z'
---

# PLS

\
The general underlying model of multivariate PLS is

$$X = T P^\mathrm{T} + E$$

 balkjjdkfal;skdjflaks;dfj $X = T P^\mathrm{T} + E$ a;dlsjflaksjdf 

```latex
Y = U Q^\mathrm{T} + F
```
where {{mvar|X}} is an <math>n \times m</math> matrix of predictors, {{mvar|Y}} is an <math>n \times p</math> matrix of responses; {{mvar|T}} and {{mvar|U}} are <math>n \times l</math> matrices that are, respectively, projections of {{mvar|X}} (the ''X score'', ''component'' or ''factor'' matrix) and projections of {{mvar|Y}} (the ''Y scores''); {{mvar|P}} and {{mvar|Q}} are, respectively, <math>m \times l</math> and <math>p \times l</math> orthogonal ''loading'' matrices; and matrices {{mvar|E}} and {{mvar|F}} are the error terms, assumed to be independent and identically distributed random normal variables. The decompositions of {{mvar|X}} and {{mvar|Y}} are made so as to maximise the [[covariance]] between {{mvar|T}} and {{mvar|U}}.



# enet

lasso penalty function
```latex
<math>\|\beta\|_1 = \textstyle \sum_{j=1}^p |\beta_j|

```
The estimates from the elastic net method are defined by
```latex 
\hat{\beta} \equiv \underset{\beta}{\operatorname{argmin}} (\| y-X \beta \|^2 + \lambda_2 \|\beta\|^2 + \lambda_1 \|\beta\|_1)

```


# latex
<style TYPE="text/css">
code.has-jax {font: inherit; font-size: 100%; background: inherit; border: inherit;}
</style>
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
    tex2jax: {
        inlineMath: [['$','$'], ['\\(','\\)']],
        skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'] // removed 'code' entry
    }
});
MathJax.Hub.Queue(function() {
    var all = MathJax.Hub.getAllJax(), i;
    for(i = 0; i < all.length; i += 1) {
        all[i].SourceElement().parentNode.className += ' has-jax';
    }
});
</script>
<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.4/MathJax.js?config=TeX-AMS_HTML-full"></script>


 *E*~0~=*mc*^2^


```latex
`x^2`
`f(x) = x^2`
```


```latex
x_{1,2} = {-b\pm\sqrt{b^2 - 4ac} \over 2a}.
```

```latex
\begin{align*}
  f(x) &= x^2\\
  g(x) &= \frac{1}{x}\\
  F(x) &= \int^a_b \frac{1}{3}x^3
\end{align*}
```



# rMarkdonw

---
title: "Sample Equations used in Statistics"
output: html_document
---
###  Summations
### Without Indices
$\sum x_{i}$
$\sum x_{i}^2$
$\sum x_{i}y_{i}$
#### With Indices - Inline Form
$\sum_{i=1}^n x_{i}$
$\sum_{i=1}^n x_{i}^2$
$\sum_{i=1}^n x_{i}y_{i}$
#### With Indices - Display Form
$$\sum_{i=1}^n x_{i}y_{i}$$
### Independent Samples
$$\mu_{\bar{x_{1}} - \bar{x_{2}}} = \mu_{1} - \mu_{2}$$
$$\sigma_{\bar{x_{1}} - \bar{x_{2}}}^2 = \frac {\sigma_{1}^2}{n_{1}} + \frac{\sigma_{2}^2}{n_{2}}$$
$$\mu_{\hat{p}_{1} - \hat{p}_{2}} = p_{1} - p_{2}$$
$$\sigma_{\hat{p}_{1} - \hat{p}_{2}}^2 = \frac {p_{1}(1 - p_{1})}{n_{1}} + \frac {p_{2}(1 - p_{2})}{n_{2}}$$
### Pooled Sample Variance
$$s_{p}^2 = \frac {(n_{1} - 1)s_{1}^2 + (n_{2} - 1)s_{2}^2}{n_{1} + n_{2} - 2}$$
### Pooled Sample Proportion
$$\hat{p} = \frac {n_{1}\hat{p}_1 + n_{2}\hat{p}_{2}}{n_{1} + n_{2}}$$
### Chi-Square Test
$$\chi^2 = \sum \frac {(O - E)^2}{E}$$
### Correlations
$${SS}_{xx} = \sum (x - \bar{x})^2 = \sum x^2 - \frac {(\sum x)^2}{n}$$
$${SS}_{xy} = \sum (x - \bar{x})(y - \bar{y}) = \sum xy - \frac {(\sum x)(\sum y)}{n}$$
$$r = \frac {{SS}_{xy}}{\sqrt {{SS}_{xx}{SS}_{yy}}}$$
### Regression
#### Population Regression Line
$$E(y) = \alpha + \beta{x}$$
$$var(y) = \sigma^2$$
#### Least Squares Line
$$\hat{y} = a + bx$$
where 
$$b = \frac {{SS}_{xy}}{{SS}_{xx}}$$
and 
$$\bar{y} = a + b\bar{x}$$
#### Residual Sum of Squares
$$SSResid = \sum (y - \hat{y})^2 = \sum y^2 - a\sum y - b \sum xy$$
#### Standard Errors
$$s_{e} = \sqrt \frac {SSResid}{n - 2}$$
$$s_{b} = \frac {s_{e}}{\sqrt {{SS}_{xx}}}$$
$$s_{a + bx} = s_{e} \sqrt {1 + \frac {1}{n} + \frac {(x - \bar{x})^2}{{SS}_{xx}}}$$
for prediction:
$$se(y - \hat{y}) = s_{e} \sqrt {1 + \frac {1}{n} + \frac {(x - \bar{x})^2}{{SS}_{xx}}}$$
### Variance
$$SSTr = \frac {T_{1}^2}{n_{1}} + \frac {T_{2}^2}{n_{2}} + ... + \frac {T_{k}^2}{n_{k}} - \frac {T^2}{n}$$
$$SSTo = x_{1}^2 + x_{2}^2 + ... + x_{k}^2 - \frac {T^2}{n}$$
$$SSE = SSTo - SSTr$$

#####

<https://www.kaggle.com/hamidhaghshenas/high-quality-mathematical-equations-using-latex>


<https://www.calvin.edu/~rpruim/courses/s341/S17/from-class/MathinRmd.html>

$$x = y $$

 $$x < y $$

 $$x > y $$

 $$x \le y $$

 $$x \ge y $$

 $$x^{n}$$

 $$x_{n}$$

 $$\overline{x}$$

 $$\hat{x}$$

 $$\tilde{x}$$

 $$\frac{a}{b}$$

 $$\frac{a}{b}$$

 $$\displaystyle \frac{a}{b}$$

 $$\binom{n}{k}$$

 $$x_{1} + x_{2} + \cdots + x_{n}$$

 $$x_{1}, x_{2}, \dots, x_{n}$$

 $$x \in A$$

 $$|A|$$

 $$x \in A$$

 $$x \subset B$$

 $$x \subseteq B$$

 $$A \cup B$$

 $$A \cap B$$

 $$X \sim {\sf Binom}(n, \pi)$$ 

 $$\mathrm{P}(X \le x) = {\tt pbinom}(x, n, \pi)$$ 

 $$P(A \mid B)$$

 $$\mathrm{P}(A \mid B)$$
 $$\{1, 2, 3\}$$

 $$\sin(x)$$

 $$\log(x)$$

 $$\int_{a}^{b}$$

 $$\left(\int_{a}^{b} f(x) \; dx\right)$$

 $$\left[\int_{\-infty}^{\infty} f(x) \; dx\right]$$

 $$\left. F(x) \right|_{a}^{b}$$

 $$\sum_{x = a}^{b} f(x)$$

 $$\prod_{x = a}^{b} f(x)$$

 $$\lim_{x \to \infty} f(x)$$

 $$\displaystyle \lim_{x \to \infty} f(x)$$
When the data points are equally spaced, an analytical solution to the least-squares equations can be found. This solution forms the basis of the convolution method of numerical smoothing and differentiation. 

Suppose that the data consists of a set of ''n''  points (''x''<sub>''j''</sub>, ''y''<sub>''j''</sub>)  (''j'' = 1, ..., ''n''), where ''x'' is an independent variable and ''y''<sub>''j''</sub> is a datum value.

 A polynomial will be fitted by [[linear least squares (mathematics)|linear least squares]]  to a set of ''m'' (an odd number) adjacent data points, each separated by an interval ''h''. Firstly, a change of variable is made
$z = {{x - \bar x} \over h}$ 


where ${\bar x}$is the value of the central point. ''z'' takes the values $\tfrac{1-m}{2},\cdots,0,\cdots,\tfrac{m-1}{2}$. <ref group=note>With even values of ''m'', ''z'' will run from 1&nbsp;−&nbsp;''m'' to ''m''&nbsp;−&nbsp;1 in steps of 2</ref> The polynomial, of degree ''k'' is defined as $Y = a_0  + a_1 z + a_2 z^2  \cdots  + a_k z^k.$ <ref group=note>. 

The simple [[moving average]] is a special case with ''k'' = 0, ''Y'' = ''a''<sub>0</sub>. In this case all convolution coefficients are equal to 1/''m''.</ref>
The coefficients ''a''<sub>0</sub>, ''a''<sub>1</sub> etc. are obtained by solving the [[normal equations]] (bold '''a''' represents a [[Vector space|vector]], bold '''J''' represents a [[Matrix (mathematics)|matrix]]).

${\mathbf{a}} = \left( {{\mathbf{J}}^{\mathbf{T}} {\mathbf{J}}} \right)^{ - {\mathbf{1}}} {\mathbf{J}}^{\mathbf{T}} {\mathbf{y}}$
The $i</math>-th row of $\mathbf J$has values $1, z_i, z_i^2, \dots$.

