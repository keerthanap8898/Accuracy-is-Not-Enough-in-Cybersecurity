# Research Interpretation: "Accuracy Is Not Enough"

## Core Claim
The work argues that **plain accuracy is an unsafe primary KPI** for CVE impact prediction and vulnerability mapping, especially when vulnerabilities are rare, labels are delayed/disputed, and the cost of false negatives is catastrophic.

## Proposed Contribution
A **Leveled Confusion Matrix Framework (L0-L6)**:
- L0: TP/TN/FP/FN primitives
- L1: Class rates (Recall/Specificity/FNR/FPR)
- L2: Predictive values (Precision/NPV/FDR/FOR)
- L3: Likelihood ratios (PLR/NLR)
- L4: Balanced metrics (F1+/F1-, Balanced Accuracy, Youden's J)
- L5: Global agreement (Cohen's Kappa, MCC)
- L6: Accuracy as last, low-trust snapshot

## Security Interpretation Emphasis
The framework pushes teams to optimize for:
- **Missed vulnerability prevention** (Recall↑, FNR↓)
- **Trustworthiness of safe labels** (FOR↓, NLR↓)
- **Robustness under imbalance** (MCC↑, Balanced Accuracy↑)

## Evidence and Narrative Elements in Repo
- Main narrative and recommendations are in `README.md`.
- Supporting communication in `INFO.md` reiterates decision-SLA framing.
- `lala.md` clarifies this is an interpretation framework using standard statistics, not a novel proprietary algorithm.
- Images reinforce three ideas:
  1. Layered metric hierarchy (L0-L6)
  2. FN-vs-FP consequences across industries
  3. Trend dashboards (accuracy can look flat while FNR/NLR/MCC expose degradation)

## Where This Is Most Useful
1. Vulnerability intelligence correlation (CVE ↔ package ↔ distro mapping)
2. Risk-based vulnerability prioritization
3. SLA governance for triage and remediation
4. Executive reporting that separates "coverage risk" from "alert noise"
5. Continuous validation of third-party enrichment feeds

## Vulnerability Management Lifecycle Gaps It Can Enrich
1. Asset/Vuln Identification: confidence scoring and "safe-label" skepticism
2. Validation/Analysis: explicit FN/FOR/NLR gates before de-prioritization
3. Prioritization: include exploitability-weighted FN penalties
4. Remediation Planning: threshold tuning with Youden's J and BA
5. Verification/Closure: require post-fix metric deltas (MCC/FNR)
6. Continuous Monitoring: rolling trend alerts on FNR/NLR/MCC, not just accuracy

## Example Dashboard Signals to Operationalize
- **Hard guardrails**: FNR <= X, FOR <= Y, NLR <= Z
- **Drift/quality**: rolling MCC not below baseline band for N days
- **Triage load**: FPR and Precision tracked by source/channel
- **Exploit-aware overlays**: any exploited CVE miss triggers incident review

## Caveats / Major Adoption Risks
1. Requires reliable and timely ground truth (often delayed/disputed in CVE ecosystems)
2. Metric overload risk without role-specific views
3. Teams may still game easy metrics unless guardrails are policy-bound
4. Needs calibration per business context (critical infra vs consumer SaaS)
5. Requires data plumbing from CVE/NVD/CISA/vendor advisories to local asset truth

## Implementation Hypothesis for Open Source
An OSS "validation dashboard" based on this work is most impactful if it ships with:
- Ingestion adapters (CVE JSON 5.x, CISA KEV/vulnrichment, distro advisories)
- Reconciliation logic for conflicting labels (e.g., disputed vs affected)
- Time-windowed metrics with per-severity/per-asset segmentation
- Policy engine (SLOs for FNR/FOR/NLR/MCC)
- Audit trail and incident hooks for metric breaches

---

# Confusion-matrix metrics for "OSV affected state" drift across all 2025 CVEs

## Executive summary

This section defines a reproducible way to compute confusion-matrix metrics for 2025 CVEs by comparing the “affected state” as expressed in the CNA container at a record’s initial git commit versus the CNA container at the repository’s latest commit, while restricting population to records whose latest version contains valid CISA ADP enrichment (the “valid ADP field values” gate).

Interpretation guardrail: this measures CNA affectedness drift over time within the same CVE corpus, conditioned on later CISA ADP presence. It does **not** mean CISA overwrote CNA affectedness.

Because this requires iterating all 2025 records and walking git history, a local git workflow is the practical approach.

## Dataset definition, scope, and constraints

### Primary corpus

- Treat `cvelistV5/cves/2025/**/CVE-2025-*.json` as the analysis population.
- Use CVE JSON 5.x records containing `dataType: CVE_RECORD`, `containers.cna`, and optional `containers.adp`.

### Constraints

- Scope is GitHub-hosted CVE list data.
- Analysis does not require non-GitHub mirrors if the official CVE List mirror is used.

## Defining "affected state" aligned with OSV applicability

### Where affectedness lives

In CVE JSON 5.x, applicability is primarily represented in `containers.cna.affected[]`, using:
- `defaultStatus`
- `versions[].status`
- optional version bounds such as `lessThan`, `lessThanOrEqual`, and `versionType`.

### Why CNA is the signal

For “OSV affected state” comparisons, CNA `affected` is the cleanest upstream signal to track for drift at CVE level.

### Handling `defaultStatus`

Do not ignore `defaultStatus`. If `defaultStatus == "affected"`, treat the CVE-level label as affected unless the entry is structurally empty.

## Comparison definition and confusion-matrix semantics

### Requested comparison (operationalized)

- Compare initial vs latest CNA applicability signal (`containers.cna.affected[]` + `defaultStatus` + `versions[].status`).
- Apply “after ADP vulnrichment” as an inclusion gate on latest record state.

### Valid ADP gate

At HEAD, include only records where:
- `containers.adp[]` contains an entry with `providerMetadata.shortName == "CISA-ADP"`
- and that same entry includes `metrics[].other.type == "ssvc"`.

### Unit of analysis

Default unit: per-CVE boolean affectedness.

- Positive = CNA indicates any affectedness
- Negative = CNA indicates no affectedness

This avoids brittle joins across reordered/expanded `affected[]` entries.

### Label mapping from CNA to boolean

Given `A = containers.cna.affected`:

- If `A` missing or empty => `unknown`
- Else if any `A[i].defaultStatus == "affected"` => `affected`
- Else if any `A[i].versions[j].status == "affected"` => `affected`
- Else if all explicit statuses are unaffected/unknown and all defaultStatus are unaffected => `not_affected`
- Else => `unknown`

Recommended metric policy: compute confusion metrics only on rows where both initial and latest labels are in `{affected, not_affected}`; separately report unknown counts.

### Confusion matrix definition (latest as reference)

- TP: initial affected, latest affected
- FP: initial affected, latest not_affected
- FN: initial not_affected, latest affected
- TN: initial not_affected, latest not_affected

Derived metrics:
- Accuracy, Precision, Recall, Specificity, FPR, FNR

## Reproducible methodology and commands

### Efficient corpus acquisition

```bash
git clone --filter=blob:none --no-checkout https://github.com/CVEProject/cvelistV5.git
cd cvelistV5
git sparse-checkout init --cone
git sparse-checkout set cves/2025 README.md
git checkout main
```

### Enumerate files

```bash
find cves/2025 -type f -name 'CVE-2025-*.json' | sort > cve_2025_files.txt
wc -l cve_2025_files.txt
```

### Initial commit helper

```bash
initial_sha() {
  git log --diff-filter=A --format='%H' -- "$1" | tail -n 1
}
```

### Valid CISA-ADP gate helper

```bash
has_valid_cisa_adp() {
  jq -e '
    any(.containers.adp[]?; .providerMetadata.shortName == "CISA-ADP"
        and any(.metrics[]?; .other.type == "ssvc"))
  ' "$1" >/dev/null
}
```

### CNA label helper

```bash
cna_label_from_file() {
  jq -r '
    def cna_label:
      (.containers.cna.affected // []) as $a
      | if ($a|length) == 0 then "unknown"
        elif any($a[]; .defaultStatus == "affected") then "affected"
        elif any($a[]; any(.versions[]?; .status == "affected")) then "affected"
        elif all($a[]; (.defaultStatus // "unaffected") == "unaffected"
                  and all(.versions[]?; (.status // "unknown") != "affected")) then "not_affected"
        else "unknown"
        end;

    cna_label
  ' "$1"
}
```

### End-to-end comparison table

```bash
out=labels_2025_initial_vs_head.tsv
echo -e "cve_file\tcve_id\tinitial_sha\tinitial_label\thead_label\thead_has_valid_adp" > "$out"

while read -r f; do
  cve_id=$(basename "$f" .json)

  if has_valid_cisa_adp "$f"; then
    head_has_adp=true
  else
    head_has_adp=false
  fi

  init_sha=$(initial_sha "$f")
  if [ -z "$init_sha" ]; then
    continue
  fi

  tmp_init=$(mktemp)
  git show "${init_sha}:${f}" > "$tmp_init" 2>/dev/null || { rm -f "$tmp_init"; continue; }

  init_label=$(cna_label_from_file "$tmp_init")
  head_label=$(cna_label_from_file "$f")

  echo -e "${f}\t${cve_id}\t${init_sha}\t${init_label}\t${head_label}\t${head_has_adp}" >> "$out"
  rm -f "$tmp_init"
done < cve_2025_files.txt
```

### Metric computation example

```bash
python3 - <<'PY'
import csv

path = "labels_2025_initial_vs_head.tsv"
rows = []
with open(path, newline="") as f:
    r = csv.DictReader(f, delimiter="\t")
    for row in r:
        if row["head_has_valid_adp"] != "true":
            continue
        rows.append(row)

bin_rows = [x for x in rows if x["initial_label"] in ("affected", "not_affected")
                     and x["head_label"] in ("affected", "not_affected")]

TP = sum(1 for x in bin_rows if x["initial_label"] == "affected" and x["head_label"] == "affected")
FP = sum(1 for x in bin_rows if x["initial_label"] == "affected" and x["head_label"] == "not_affected")
FN = sum(1 for x in bin_rows if x["initial_label"] == "not_affected" and x["head_label"] == "affected")
TN = sum(1 for x in bin_rows if x["initial_label"] == "not_affected" and x["head_label"] == "not_affected")

def safe_div(a, b):
    return a / b if b else float("nan")

print({
    "n_total_2025_files": len(rows),
    "n_binary_comparable": len(bin_rows),
    "TP": TP, "FP": FP, "FN": FN, "TN": TN,
    "accuracy": safe_div(TP + TN, TP + TN + FP + FN),
    "precision": safe_div(TP, TP + FP),
    "recall": safe_div(TP, TP + FN),
    "specificity": safe_div(TN, TN + FP),
    "fpr": safe_div(FP, FP + TN),
    "fnr": safe_div(FN, FN + TP),
})
PY
```

### Discordant cases export

```bash
awk -F'\t' '
  NR==1 { next }
  $6=="true" && $4!="unknown" && $5!="unknown" && $4!=$5 { print }
' labels_2025_initial_vs_head.tsv > discordant_2025_initial_vs_head.tsv
```

## Expected outputs and sanity checks

### Expected artifacts

- `labels_2025_initial_vs_head.tsv`
- Summary counts (all 2025, ADP-gated, binary comparable)
- Confusion matrix and derived rates
- `discordant_2025_initial_vs_head.tsv`

### Minimum checks

- Ensure ADP gate matches `CISA-ADP` (not generic ADP entries).
- Spot-check cases with `defaultStatus == "affected"`.
- Manually inspect random FN flips with commit diffs.

## Risks, assumptions, and caveats

- ADP-gated subset is intentionally non-random and likely biasing toward triaged/high-interest CVEs.
- CNA data quality and schema usage inconsistency can create apparent flips that are data cleanup rather than model error.
- Per-CVE booleans are pragmatic for drift measurement but less precise than package-range-level OSV comparators.

## Appendix: concrete field examples to track

- CNA applicability: `containers.cna.affected[].defaultStatus`, `versions[].status`.
- ADP validity: `containers.adp[].providerMetadata.shortName == "CISA-ADP"` and `metrics[].other.type == "ssvc"`.
- Optional segmentation: KEV-related ADP metric/timeline content for exploited-only slices.
