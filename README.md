# Loan Application Process Mining
> Real-world process mining analysis on 1.2M+ banking events using Python & pm4py

## Overview
This project applies process mining techniques to the **BPI Challenge 2017** dataset — a real event log from a Dutch bank containing 1,202,267 events across 31,509 loan applications.

The goal is to discover the as-is loan application process, identify customer drop-off patterns, and generate data-driven recommendations to reduce passive cancellation.

## Key Findings

| Metric | Value |
|--------|-------|
| Total loan applications | 31,509 |
| Passive cancellation rate | **49.8%** |
| Active rejection rate | 11.9% |
| Cases exposed to rework loop | **47%** |
| Avg. rework loop repetitions | **12.8×** |
| Cancellation timing | Step 31.5 / 35 (~88% completion) |

**Critical insight:** Nearly half of all applicants abandoned the process before completion. Of those who encountered the incomplete-file rework loop (47% of cases), 34.8% eventually cancelled — after being asked to resubmit materials an average of 12.8 times.

## Methodology

1. **Data Loading & Exploration** — Loaded XES event log with pm4py; identified case structure, activity types, and timestamps
2. **Process Discovery** — Applied Inductive Miner algorithm to automatically discover the as-is process model
3. **Case Outcome Analysis** — Classified all cases into: completed, actively rejected, passively cancelled
4. **Root-Cause Analysis** — Investigated the `W_Call incomplete files` → `A_Incomplete` rework loop as a primary driver of cancellation

## Recommendations

1. **Merge the rework loop** *(High Impact)* — Consolidate `W_Call incomplete files` and `A_Incomplete` into a single step with upfront document requirements to reduce 12.8× average repetitions
2. **Streamline offer-decision branching** *(Medium Impact)* — Consolidate parallel XOR branches into a single decision point to reduce overall process complexity
3. **Front-load document validation** *(Preventive)* — Introduce a completeness checklist at application creation, before significant processing costs are incurred

## Tech Stack
- Python 3
- pm4py — process mining library
- pandas
- Google Colab

## Dataset
BPI Challenge 2017 — available at [4TU.ResearchData](https://data.4tu.nl/articles/dataset/BPI_Challenge_2017/12696884)

> Van Dongen, B. (2017). BPI Challenge 2017. 4TU.ResearchData.
