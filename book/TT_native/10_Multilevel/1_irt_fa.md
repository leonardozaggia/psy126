---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.11.5
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

# 8.1 IRT and Factor Analysis

<div style="display: flex; justify-content: space-between;">
  <img src="https://www.researchgate.net/profile/R-Chalmers/publication/275441302/figure/fig1/AS:613924500164609@1523382415156/The-probability-surface-plots-on-the-top-represent-two-dimensional-compensatory-left.png" alt="Multidimensional IRT" style="width: 49%;">
</div>

EFA and CFA are designed for metric input variables
(unless we use specific correlation coefficients suited for categorical data, like tetrachoric correlation). The
main outcomes are factor loadings and factor scores. IRT models are designed for
categorical data with item-category parameters (location, discrimination) and person
parameters as main outcomes. However, it has been found that there is a strong
parametric relationship between FA and IRT (Takane and De Leeuw, 1986).  

Let us consider a simple unidimensional 2-PL, rewritten in logit form:  

(1) $logit(P(X_{vi})) = \alpha_i(\theta_v - \beta_i))$

We can re-parameterize this model as  

(2) $logit(P(X_{vi})) = \alpha_i\theta_v - d_i$

with $d_i = -\beta_i\alpha_i$

The second equation reflects a factor analytic intercept-slope representation of the
2-PL. The discrimination parameter $\alpha_i$ can be interpreted as loading (i.e., slope as
reflected in the ICC plot). The parameter $d_i$ is the intercept. From the first equation,
it follows that $d_i$ = $-\beta_i\alpha_i$ . Note that both equations fit the same model, they are just
parameterized differently. Consequently, the parameters $\theta_i$ are the same, regardless
which expression we use. Within an IRT context (first equation), we call them “person
parameters,” whereas within a FA context (second equation), we call them “factor scores".  

## Fit the models

To illustrate, we conduct a 2-PL analysis which involved
dichotomous items on knowledge characteristics from the WDQ dataset.
We use the `ltm` package for R and request the two different parameterizations.

First, import all the necessary packages for R and Python.

```{code-cell}  
# General imports
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Rpy2 imports
from rpy2 import robjects as ro
from rpy2.robjects import pandas2ri, numpy2ri
from rpy2.robjects.packages import importr

# Automatic conversion of arrays and dataframes
pandas2ri.activate()
numpy2ri.activate()

# Set random seed for reproducibility
ro.r('set.seed(123)')

# Ipython extension for magic plotting
%load_ext rpy2.ipython

# R imports
importr('base')
importr('mirt')
importr('Gifi')
importr('MPsychoR')
importr('ltm')
```

Load and inspect the dataset `RWDQ` and remove the first item (first column). Name your subset `RWDQ1`.

```{code-cell} 
ro.r("data(RWDQ)")

# Convert to Python
RWDQ = pandas2ri.rpy2py(ro.globalenv['RWDQ'])

# Eliminate first item (misfit)
RWDQ1 = RWDQ.drop(RWDQ.columns[0], axis=1)

# Put data into R
ro.globalenv['RWDQ1'] = RWDQ1
```

Now we fit the two models mentioned above.

```{code-cell}  
# Fit the IRT model using lavaan's ltm
ro.r('irtpar <- ltm(RWDQ1 ~ z1)')
ro.r('fapar <- ltm(RWDQ1 ~ z1, IRT.param = FALSE)')

# Combine and compare parameter estimates
compare_params = ro.r('head(cbind(coef(irtpar), coef(fapar)))')

# Print comparison with 3 decimal precision
ro.r('print(round(head(cbind(coef(irtpar), coef(fapar))), 3))')
```

The first two columns are based on the parameterization in Eq. (1), involving
$\alpha_i$ and $\beta_i$ . The last two columns correspond to $d_i$ and $\alpha_i$ from Eq. (2).   
Let us compute the person parameters and confirm that they are the same for both models.

In theory, both set of person parameters should be the same. To investigate if this is true, use the `identical` function.

```{code-cell}  
ro.r("irtppar <- factor.scores(irtpar)$score.dat$z1")
ro.r("fappar <- factor.scores(fapar)$score.dat$z1")

print(ro.r("identical(irtppar, fappar)"))
```

```
[1] TRUE
```

As indicated by the `identical` function, the two scores are in fact the same.  

Besides IRT and Factor Analysis there is also Item Factor Analysis (IFA).
IFA marries IRT and FA so that we get the best of both worlds: On the one hand,
we have all the possibilities exploratory/confirmatory model specification, good
opportunities for goodness-of-fit assessment, and options for rotation from the FA
world. On the other hand, we can make use of the wide range of developed IRT
models and get a deep probabilistic insight into the behavior of items and persons.
Note that the terms “MIRT” and “IFA” are often used synonymously. Here, from now on, we use “MIRT.”
