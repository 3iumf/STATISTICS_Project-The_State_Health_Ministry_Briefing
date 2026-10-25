# Haemoglobin Robust Statistics — State Health Ministry Briefing

Hand-worked and Python-verified analysis of haemoglobin (Hb) levels from a random sample of pregnant women at a clinic, prepared as a briefing for a State Health Ministry.

## The problem

The State Health Ministry drew a random sample of **10 pregnant women** from a clinic register of **1,000** and measured haemoglobin (g/dL):

```
10.2, 11.5, 9.8, 12.0, 10.6, 11.1, 10.4, 11.8, 9.5, 5.1
```

The Ministry wants to know:
- What is the typical Hb at this clinic?
- How reliable is that figure?
- What should be done about the 5.1 reading?
- How many women should be tested next time?

## Results

| Step | Task | Result |
|------|------|--------|
| 1 | Centre | Mean = **10.20 g/dL**, Median = **10.50 g/dL** |
| 2 | Spread | Variance = **3.907**, SD = **1.977 g/dL** (divisor n − 1) |
| 3 | Quartiles (linear interpolation) | Q1 = **9.90**, Q2 = **10.50**, Q3 = **11.40**, IQR = **1.50** |
| 4 | 1.5 × IQR fences | [**7.65**, **13.65**], so **5.1 is an outlier** |
| 5 | Without 5.1 | Mean 10.77, Median 10.60, SD 0.885, IQR 1.30 |
| 6 | Sample size for SE ≤ 0.25 | n = (1.5 / 0.25)² = **36 women** |

## Decision (Step 5)

Report the **median and IQR (10.5 g/dL, IQR 1.5)**. When 5.1 is removed they barely change (the median goes from 10.5 to 10.6 and the IQR from 1.5 to 1.3), whereas the SD falls by more than half. The reading of 5.1 g/dL should be treated as a **real extreme, not an error**. It is clinically possible (severe anaemia), so it should stay in the data once confirmed. This woman most likely belongs to a **different, high-risk group** and should be referred urgently and tracked separately.

## Repository contents

| File | Description |
|------|-------------|
| `Hb_Ministry_Manual_Solution.pdf` | Step-by-step manual (hand) working with explanations |
| `Hb_Ministry_Python_Check.ipynb` | Jupyter notebook that reproduces and checks every answer, with a boxplot of the outlier fences |

## Methods used

- **Mean and median** as measures of centre
- **Sample variance and SD** with Bessel's correction (n − 1)
- **Quartiles by linear interpolation**, using position L = (n − 1)p + 1 (NumPy's default and Excel's `QUARTILE.INC`)
- **Tukey's 1.5 × IQR fences** for detecting outliers
- **Robust vs non-robust statistics**: how the mean and SD compare with the median and IQR
- **Standard error and sample size**: SE = σ / √n, so n = (σ / SE)²

## How to run

```bash
pip install numpy matplotlib jupyter
jupyter notebook Hb_Ministry_Python_Check.ipynb
```

## Tools

Python · NumPy · Matplotlib · Jupyter Notebook

---
*Part of my AI Engineer training: Day 3 Project (Sampling + Robust Statistics).*
