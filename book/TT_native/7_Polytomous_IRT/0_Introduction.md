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

# <i class="fa-solid fa-cubes"></i> Polytomous

## Measurement models for Polytomous scores


In the previous session, we focused on dichotomous data, where responses were scored as either correct or incorrect. In this chapter, we extend the framework to **polytomous items**—those allowing for multiple ordered response categories (e.g., Likert scales, partial credit tasks).

We introduce a series of models for analyzing such data, each differing in how they parameterize response structure:

- **Rating Scale Model (RSM)** — assumes equal threshold distances across items.
- **Partial Credit Model (PCM)** — allows item-specific thresholds.
- **Generalized PCM (GPCM)** — adds item-specific discrimination parameters.
- **Graded Response Model (GRM)** — estimates cumulative probabilities for ordered categories.

Each model reflects different assumptions about how response categories function, and selecting the appropriate model depends on both theoretical and empirical considerations.

*Reminder:* All models assume unidimensionality, which should be verified using the methods introduced earlier.

