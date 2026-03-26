# RCT Verdict Classifier

A single-page browser tool for interpreting randomized clinical trial results with a **CI + MCID-first workflow**, plus a secondary **prior-sensitivity table** for posterior probability support.

![status](https://img.shields.io/badge/status-stable-green) ![license](https://img.shields.io/badge/license-MIT-blue)

<h2 align="center"><a href="https://ihtanboga.github.io/rct-verdict-classifier/">Open Live Demo</a></h2>

---

## What it does

When a trial reports something like `HR 0.89 (95% CI 0.77 to 1.04; p = 0.14)`, the lazy summary is often "no significant difference." This tool is built to answer the better question:

**What does the confidence interval actually exclude relative to clinically important thresholds?**

The live app now emphasizes:

1. **Frequentist core**: null + MCID-based classification
2. **Scientific reporting language**: output phrasing suited to methods/results sections
3. **Prior sensitivity support**: flat, skeptical, optimistic, and pessimistic posterior checks shown as a separate layer, not as the primary verdict engine

## Core verdicts

| Class | Frequentist definition |
|---|---|
| **Positive** | Entire CI beyond the benefit MCID |
| **Imprecise (+)** | Benefit is statistically significant, but CI still crosses the benefit MCID |
| **Neutral** | Clinically important benefit and clinically important harm are both excluded |
| **Negative** | Clinically important benefit is excluded, but clinically important harm is not fully excluded |
| **Inconclusive / Underpowered** | CI still includes clinically important benefit and/or clinically important harm |
| **Harmful** | Entire CI beyond the harm MCID |

## Prior sensitivity layer

The page no longer uses an "Expected Effect (Optimistic Prior)" input. Instead, the posterior support section applies a fixed prior set:

- **Flat**
- **Weak skeptical**
- **Moderate skeptical**
- **Strong skeptical**
- **Moderate optimistic**
- **Moderate pessimistic**

For each prior, the app reports:

- Posterior median and 95% CrI
- `Pr(benefit)`
- `Pr(MCID benefit)`
- `Pr(indifference)`
- `Pr(MCID harm)`

This table is intended as a **sensitivity check**, not as the primary classification rule.

## Features

- **Clean single-page UI** with dark navy / orange hero treatment
- **No preset chip bar** in the live input form
- **Multiple input modes**: ratio estimate + 95% CI, or 2x2 event counts
- **CI + MCID forest visualization**
- **Step-by-step decision trace**
- **Scientific reporting sentence**
- **Framework figure cards** pulled from the repo's SVG assets
- **Downloadable HTML summary**
- **Zero build step** - runs entirely in the browser

## Method summary

### Frequentist decision path

1. Does the 95% CI exclude the null?
2. If benefit-signaling: does the upper CI bound remain beyond the benefit MCID?
3. If not significant: is clinically important benefit excluded?
4. Is clinically important harm also excluded?
5. Use those exclusions to separate **neutral**, **negative**, and **inconclusive**.

### Posterior support

Posterior calculations use conjugate normal-normal updating on the log-ratio scale and are displayed only as a supporting sensitivity layer across the six fixed priors listed above.

## Figures included in the repo

- `figures/ci_mcid_decision_algorithm.svg`
- `figures/ci_mcid_classification_scenarios.svg`
- `figures/p_nonsig_three_scenarios_english.svg`
- `figures/negative_vs_neutral_comparison.svg`
- `figures/underpowered_visual_explanation.svg`

## Conceptual sources

The current revision is aligned to the accompanying interpretation note and emphasizes the same distinction between:

- **negative** vs **neutral**
- **non-significant** vs **inconclusive**
- **statistical** vs **clinical** significance

Key cited influences remain:

- Pocock SJ, Stone GW. *NEJM*. 2016;375:861-870.
- Hawkins AT, Samuels JD. *JAMA*. 2021;326:1875-1876.
- Altman DG, Bland JM. *BMJ*. 1995;311:485.
- Gelman A, Carlin J. *Perspect Psychol Sci*. 2014;9:641-651.

## Author

Prof. Ibrahim Halil Tanboga, MD, PhD - Nisantasi University Medical School

## License

MIT
