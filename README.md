<p align="center">
  <h1 align="center">Global History Branch Predictor</h1>
  <p align="center">Group 5 · Advanced Branch Prediction using Global Control-Flow History · ChampSim Simulator</p>
</p>

---

##  Overview
The **Global History Branch Predictor (GlobalBP)** enhances prediction accuracy by exploiting **global inter-branch correlations**, which local predictors often miss. It is implemented and evaluated in the **ChampSim** simulation environment and compared against standard predictors like gshare, perceptron, bimodal, and hashed_perceptron.

---

## Problem Statement
In superscalar processors, **branch mispredictions** cause pipeline stalls and performance drops. While **local branch predictors** can track individual branch behavior, they fail to detect **global patterns** that arise from control-flow dependencies across multiple branches.

---

## Our Solution
We designed a **Global History Branch Predictor** that leverages global behavior for accurate predictions:

- **Global History Register (GHR):** Tracks recent global branch outcomes as a binary shift register.
- **Pattern History Table (PHT):** Indexed using a hash of the program counter (PC) and GHR.
- **2-bit Saturating Counters:** Predict direction and adapt based on confidence.
- **Update Policy:** Adjusts counters on every misprediction or low-confidence decision.

---

## Results

### ▶Accuracy on 50M Instructions

| Trace                 | GlobalBP | gshare | perceptron | bimodal | hashed_perceptron |
|-----------------------|----------|--------|------------|---------|--------------------|
| 400.perlbench-41B     | 95.16%   | 96.51% | 97.56%     | 95.24%  | **99.10%**         |

### ▶Accuracy on 402M Instructions

| Trace              | GlobalBP  | gshare | perceptron | bimodal | local  |
|--------------------|-----------|--------|------------|---------|--------|
| 403.gcc-16B        | **99.83%**| 99.71% | 99.83%     | XX.XX   | XX.XX  |
| 445.gobmk-17B      | **94.22%**| 85.69% | 87.49%     | 86.15%  | 86.21% |



##  File Structure

| File/Directory | Description |
|----------------|-------------|
| `branch/myglobalbranchpred.bpred` | Main implementation of Global History Branch Predictor |
| `branch/my_predictor.bpred`       | Variant implementation for ablation/experiments |
| `branch/`                         | Contains baseline predictors (gshare, perceptron, bimodal, etc.) |
| `dpc3_traces/`                    | Input traces for evaluation (DPC-3) |

---






