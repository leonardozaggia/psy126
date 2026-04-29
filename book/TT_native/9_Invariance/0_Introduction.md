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

# <i class="fa-solid fa-scale-balanced"></i> DIF


## Differential item functioning – Measurement invariance across groups and time

Differential item functioning (DIF) arises when an item behaves differently for distinct respondent groups who possess the same latent ability. Consequently, the probability of endorsing an item varies by group membership, signalling potential bias. Detecting DIF safeguards fairness and validity by identifying items that disadvantage particular groups.

We will need two more R packages for today session: '`semTools`', '`lordif`'.
After activating your environment on Anaconda Prompt (`conda activate psy126`) you can copy paste one of the following lines based on your machine OS.

````{tab-set}
```{tab-item} Windows
~~~bash
R.exe -e "install.packages(c('semTools','lordif'), repos='https://cran.uni-muenster.de')"
~~~
```

```{tab-item} Linux/MacOS
~~~bash
R -e "install.packages(c('semTools','lordif'), repos='https://cran.uni-muenster.de')"
~~~
```
````