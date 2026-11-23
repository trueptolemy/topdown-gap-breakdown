# topdown-gap-breakdown

A short write-up of a method that breaks the throughput score gap between two
configurations, typically a virtual machine (VM) and bare metal (BM), down into
Top-down Microarchitecture Analysis (TMA) categories.

Comparing TMA percentages side by side does not show where a gap comes from.
Each case normalizes by its own cycle count, so a category whose cost grew in
the VM can still show a smaller share there. The method uses the score ratio
to put both cases on the same cycle base:

$$
1 - r = \sum_{i \in \text{TMA}} \left( \text{Ratio}_{i,\text{VM}} - \frac{r}{\beta}\,\text{Ratio}_{i,\text{BM}} \right) + r\left(\frac{1}{\beta} - 1\right),
\qquad r = \frac{\text{Score}_\text{VM}}{\text{Score}_\text{BM}},\quad
\beta = \frac{\text{Freq}_\text{VM}\,\text{Util}_\text{VM}}{\text{Freq}_\text{BM}\,\text{Util}_\text{BM}}
$$

Each term is the share of the score gap that one TMA category costs on top of
bare metal. The document also covers:
- sub-node breakdowns with per-environment weight factors;
- a consistency check that compares the score-based view with the sampled PMU
  windows;
- a case study on SPEC CPU 2017 520.omnetpp_r with 4K and 2M EPT pages.

## Files

| file | content |
|---|---|
| [breakdown_topdown_metric.pdf](breakdown_topdown_metric.pdf) | the document |
| [breakdown_topdown_metric.tex](breakdown_topdown_metric.tex) | its LaTeX source |

## Build

```bash
xelatex breakdown_topdown_metric.tex
xelatex breakdown_topdown_metric.tex
```

XeLaTeX or LuaLaTeX is required. The source prefers Aptos, Calibri and Cambria
Math. Without them it falls back to Carlito, Latin Modern Sans and Latin Modern
Math or STIX Two Math.

