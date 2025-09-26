# Accuracy Is Not Enough  
## Confusion Matrix Metrics That Actually Work in CVE Impact Prediction

*by Keerthana Purushotham • 6 min read*

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

* Follow me on [LinkedIn](https://www.linkedin.com/in/keerthanapurushotham/) for more work.  
* Email: keep.consult@proton.me*
