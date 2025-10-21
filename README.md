# Accuracy Is Not Enough  
## Confusion Matrix Metrics That Actually Work in CVE Impact Prediction
*by Keerthana Purushotham • 6 min read*

    Copyright (C) 2025  Keerthana Purushotham <keep.consult@proton.me>.
    Licensed under the GNU AGPL v3. See LICENSE for details.

### Cite this article -
>     1. APA (7th Edition):
>        '''
>        Purushotham, K. (2024, [Month Day]). Accuracy is not enough: Confusion matrix metrics that actually work in CVE impact prediction. [Substack.
>        keerthanapurushotham.substack.com/p/accuracy-is-not-enough-confusion](https://keerthanapurushotham.substack.com/p/accuracy-is-not-enough-confusion)
>        Also available at:
>        [Medium](https://medium.com/@keerthanapurushotham/accuracy-is-not-enough-confusion-matrix-metrics-that-actually-work-in-cve-impact-prediction-d4bafd9cec1b)
>        [GitHub](https://github.com/keerthanap8898/Accuracy-is-Not-Enough-in-Cybersecurity/tree/main)
>        '''   
>     2. IEEE Style:
>        '''
>        K. Purushotham, “Accuracy Is Not Enough: Confusion Matrix Metrics That Actually Work in CVE Impact Prediction,” Substack, Oct. 2024. [Open-source on Substack: 
>        keerthanapurushotham.substack.com/p/accuracy-is-not-enough-confusion](https://keerthanapurushotham.substack.com/p/accuracy-is-not-enough-confusion)
>        Also available at:
>        [Medium](https://medium.com/@keerthanapurushotham/accuracy-is-not-enough-confusion-matrix-metrics-that-actually-work-in-cve-impact-prediction-d4bafd9cec1b)
>        [GitHub](https://github.com/keerthanap8898/Accuracy-is-Not-Enough-in-Cybersecurity/tree/main)
>        '''
>     3. BibTeX Entry:
>       ```bibtex
>         @misc{purushotham2024accuracy,
>         author       = {Keerthana Purushotham},
>         title        = {Accuracy Is Not Enough: Confusion Matrix Metrics That Actually Work in CVE Impact Prediction},
>         howpublished = {Substack},
>         year         = {2024},
>         month        = {October},
>         url          = {https://keerthanapurushotham.substack.com/p/accuracy-is-not-enough-confusion},
>         note         = {Also available on Medium and GitHub: 
>                         \url{https://medium.com/@keerthanapurushotham/accuracy-is-not-enough-confusion-matrix-metrics-that-actually-work-in-cve-impact-prediction-d4bafd9cec1b}, 
>                         \url{https://github.com/keerthanap8898/Accuracy-is-Not-Enough-in-Cybersecurity}}
>                        }
>        ```

### 🔗 Read the full post here:
- Medium: [medium.com/post/d4bafd9cec1b](https://medium.com/post/d4bafd9cec1b)
- Substack: [substack.com/home/post/p-174062640](https://substack.com/home/post/p-174062640)
- LinkedIn: [linkedin.com/posts/keerthanapurushotham_vulnerabilitymanagement-cve-security-activity-7374937046538436608-quKj](https://www.linkedin.com/posts/keerthanapurushotham_vulnerabilitymanagement-cve-security-activity-7374937046538436608-quKj/)
---

In cybersecurity, mapping vulnerabilities (CVEs) across Linux distributions is not just classification — it’s risk control. Whether `python-requests` in Debian matches `python3-requests` in Red Hat can mean the difference between a patched system and an exploitable one.

## Why does this matter?

> False negatives (missed vulnerabilities) leave blind spots.  
> False positives (over-flagged safe packages) burn developer time and erode trust.  
> Accuracy hides both problems.

### The solution: 
***treat the confusion matrix as a toolbox, and climb through its metrics step by step.***

#### Leveled Confusion Matrix Metrics Framework (L0–L6)
![confusion_matrix_levels_pyramid.png](https://github.com/keerthanap8898/Accuracy-is-Not-Enough-in-Cybersecurity/blob/main/confusion_matrix_levels_pyramid.png)

---

## Trade-Offs:

### False Negatives  
The cost of not only missing the goal but causing a loss that can end in catastrophe (e.g. a 0-day CVE miss, undetected sepsis, or a satellite collision that wipes out a multi-billion-dollar asset). That’s why systems lean heavily on redundancy, richer signals, and continuous error-analysis to “catch what matters most.”

### False Positives  
Less risky, but they erode trust and waste resources. Too many false alarms = alert fatigue, extra labor, wasted cycles (e.g. trade entries falsely flagged as fraud, AV systems braking on empty roads, false debris alarms in space). Even justice systems suffer: mis-applied risk scores can harm real lives.

#### Domain Specific Examples  
![Domain_examples.png](https://github.com/keerthanap8898/Accuracy-is-Not-Enough-in-Cybersecurity/blob/main/Domain_examples.png)

#### Visualization of FN vs FP tradeoffs across industries.
![FNvsFP_Trade-offs_across_Domains.png](https://github.com/keerthanap8898/Accuracy-is-Not-Enough-in-Cybersecurity/blob/main/FNvsFP_Trade-offs_across_Domains.png)

---

### Level 0: Core Counts (Primitives)
The foundation of all metrics:
- **TP (True Positive):** Vulnerable package correctly flagged  
- **TN (True Negative):** Safe package correctly ignored  
- **FP (False Positive):** Safe package wrongly flagged  
- **FN (False Negative):** Vulnerable package missed  

---

### Level 1: Class Rates (per positive/negative)
- **Recall (TPR / Sensitivity):** Prioritizes catching vulnerabilities  
  - ![Recall.png](https://github.com/keerthanap8898/Accuracy-is-Not-Enough-in-Cybersecurity/blob/main/formulae_images/Recall.png)
- **Specificity (TNR):** Ensures safe packages aren’t over-flagged  
  - ![Specificity.png](https://github.com/keerthanap8898/Accuracy-is-Not-Enough-in-Cybersecurity/blob/main/formulae_images/Specificity.png)

- Complementary rates:  
  - FNR = 1 – Recall  
  - FPR = 1 – Specificity  

**Security takeaway:** FNR is the costliest mistake; FPR is the loudest one.

---

### Level 2: Predictive Values (per outcome)
- **Precision (PPV):** Of the flagged packages, how many are truly vulnerable?  
  - ![Precision.png](https://github.com/keerthanap8898/Accuracy-is-Not-Enough-in-Cybersecurity/blob/main/formulae_images/Precision.png)

- **Negative Predictive Value (NPV):** Of the safe-labeled packages, how many actually are safe?  
  - ![Negative_Predictive_Value.png](https://github.com/keerthanap8898/Accuracy-is-Not-Enough-in-Cybersecurity/blob/main/formulae_images/Negative_Predictive_Value.png)

Complements:
- FDR = 1 – Precision  
- FOR = 1 – NPV  

**Security takeaway:** FOR is underused but crucial — it reveals the risk of trusting a “safe” prediction.

---

### Level 3: Likelihood Ratios (decision-level odds)
- **Positive Likelihood Ratio (PLR):** How much a positive result increases odds of vulnerability  
  - ![Positive_Likelihood_Ratio.png](https://github.com/keerthanap8898/Accuracy-is-Not-Enough-in-Cybersecurity/blob/main/formulae_images/Positive_Likelihood_Ratio.png)

- **Negative Likelihood Ratio (NLR):** How much a negative result decreases odds of vulnerability  
  - ![Negative-Likelihood-Ratio.png](https://github.com/keerthanap8898/Accuracy-is-Not-Enough-in-Cybersecurity/blob/main/formulae_images/Negative-Likelihood-Ratio.png)

> Security takeaway: PLR measures alert trustworthiness; NLR measures trust in “safe” decisions.

---

### Level 4: Balanced Metrics (threshold trade-offs)
- **F1-Positive:** Balances catching vulnerabilities vs avoiding wasted alerts  
  - ![pos_F1_Score.png](https://github.com/keerthanap8898/Accuracy-is-Not-Enough-in-Cybersecurity/blob/main/formulae_images/pos_F1_Score.png)

- **F1-Negative:** Balances suppressing false alarms vs maintaining trust  
  - ![neg_F1_Score.png](https://github.com/keerthanap8898/Accuracy-is-Not-Enough-in-Cybersecurity/blob/main/formulae_images/neg_F1_Score.png)

- **Balanced Accuracy (BA):** Mitigates bias in imbalanced datasets  
  - ![Balanced_Accuracy.png](https://github.com/keerthanap8898/Accuracy-is-Not-Enough-in-Cybersecurity/blob/main/formulae_images/Balanced_Accuracy.png)

- **Youden’s J:** Quick threshold selector maximizing separation from randomness  
  - ![Youdens_J.png](https://github.com/keerthanap8898/Accuracy-is-Not-Enough-in-Cybersecurity/blob/main/formulae_images/Youdens_J.png)

---

### Level 5: Agreement and Global Correlation
- **Cohen’s Kappa (κ):** Corrected measure of agreement beyond chance  
  - ![Cohens_Kappa.png](https://github.com/keerthanap8898/Accuracy-is-Not-Enough-in-Cybersecurity/blob/main/formulae_images/Cohens_Kappa.png)

- **Matthews Correlation Coefficient (MCC):** Robust metric stable across imbalanced datasets; applicable in security, bioinformatics, finance  
  - ![Matthews_Correlation-Coefficient.png](https://github.com/keerthanap8898/Accuracy-is-Not-Enough-in-Cybersecurity/blob/main/formulae_images/Matthews_Correlation-Coefficient.png)

---

### Level 6: Baseline Snapshot
- **Accuracy:** A quick overall number — but misleading when vulnerabilities are rare  
  - ![plain_Accuracy.png](https://github.com/keerthanap8898/Accuracy-is-Not-Enough-in-Cybersecurity/blob/main/formulae_images/plain_Accuracy.png)

> Security takeaway: Accuracy is for dashboards, not critical risk decisions.

---

## Practical Recommendations

- Lead with **Recall** and **FNR**, because misses are catastrophic  
- Track **FOR** and **NLR**, because trusting “safe” labels is risky  
- Use **Balanced Accuracy** and **Youden’s J** to choose thresholds  
- Report **MCC** and **F1** for robustness  
- Treat **Accuracy** only as a sanity check  

> Both matters: FN kills you outright; FP bleeds you slowly.

---

## Closing

> Security & threat impact prediction is not about being “mostly right.” It’s about being *“right where it counts.”*

This leveled framework transforms the confusion matrix into a decision map — one that uncovers blind spots, tames operational noise, and aligns predictions with real-world risk.

---

### Glossary of Acronyms

1. **CVE** — Common Vulnerabilities and Exposures  
2. **TP** — True Positive  
3. **TN** — True Negative  
4. **FP** — False Positive  
5. **FN** — False Negative  
6. **TPR / Recall / Sensitivity** — Proportion of vulnerabilities correctly flagged  
7. **TNR / Specificity** — Proportion of safe packages correctly ignored  
8. **FNR** — False Negative Rate  
9. **FPR** — False Positive Rate  
10. **PPV / Precision** — Of flagged items, how many truly are vulnerable  
11. **NPV** — Of safe-labeled items, how many truly are safe  
12. **FDR** — False Discovery Rate  
13. **FOR** — False Omission Rate  
14. **PLR** — Positive Likelihood Ratio  
15. **NLR** — Negative Likelihood Ratio  
16. **BA / Balanced Accuracy** — Average of Recall and Specificity  
17. **MCC** — Matthews Correlation Coefficient  
18. **κ / Cohen’s Kappa** — Chance-corrected measure of agreement  

---

### Summary Cheat Sheet:
![Confusion_matrix_Cheat-Sheet.png](https://github.com/keerthanap8898/Accuracy-is-Not-Enough-in-Cybersecurity/blob/main/Confusion_matrix_Cheat-Sheet.png)

---
They’re all metrics that are easy to map with ingestion tools too — niche statistics you’d commonly see around ML models but mathematically speaking, they apply to any statistically, predictive black box.

## For example,
**CVE-2023–48022** is an epitome of how a disputed CVE turned into a false-negative, hiding an actively exploited bug downstream. Tracking False-Negative-Rate (FNR) or Negative-Likelihood-Ratio (NLR) would’ve flagged very early on that “safe/unaffected” wasn’t safe. Even MCC would’ve exposed the imbalance of missing rare but critical vulnerabilities.

- The JSON for OSV template has attributes that can be automated,
  - CNA [disputed] → implying no urgent fix needed.
  - CISA [affected] → treat as dangerous.
- CVE-2023–48022 : github.com/CVEProject/cvelistV5/blob/main/cves/2023/48xxx/CVE-2023-48022.json
  - ![OSV for CVE 2023-48022](https://github.com/keerthanap8898/Accuracy-is-Not-Enough-in-Cybersecurity/blob/main/CVE-2023-48022.png)

#### `That’s the FN suppressed incorrectly when it was being actively exploited.`
- FNR (↑) spikes to 1 if an exploited vulnerability is missed.
- NLR (↑) the “safe/unaffected” label was untrustworthy.
- MCC (↓) correlation drops since a rare but critical positive was missed.

```
All this obviously depends on the timing of & if exploitations/bugs in your tool are identifiable.
```

To help visualize the dashboard, I plotted a sample and it would look something like this — image attached below.

  - ![Example - How to read these metrics](https://github.com/keerthanap8898/Accuracy-is-Not-Enough-in-Cybersecurity/blob/main/Matthews%20Correlation%20Coefficient%20(MCC)%20Trend.png)

The blue arrows along the MCC graph indicates decrease in overall prediction-mapping trust.
---
* Follow me on [LinkedIn](https://www.linkedin.com/in/keerthanapurushotham/) for more work.  
* Email: keep.consult@proton.me
