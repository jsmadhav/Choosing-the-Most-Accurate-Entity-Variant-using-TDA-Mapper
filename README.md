# Choosing the Most Accurate Entity Variant using TDA Mapper

## Overview
This project tackles a classic **Entity Resolution (ER)** problem: when the same real-world entity appears in multiple slightly different versions (e.g., misspellings, incomplete fields), which record should represent the truth?  
We use **Topological Data Analysis (TDA)**—specifically **UMAP** for dimensionality reduction and **Mapper (KeplerMapper)** for graph-based topology—to measure how “well-connected” each candidate record is to the rest of the dataset. The record with the most neighbors in the Mapper graph is considered the most representative.

---

## Problem
Multiple versions of an entity exist across sources. Even humans struggle to pick the best one; algorithms struggle even more. We need a scalable, data-driven way to choose the most accurate/complete variant.

---

## Proposed Solution
1. Take the dataset that includes multiple variants of the same entity.
2. For a pair (or set) of variants, iteratively **remove one**, run the TDA pipeline, and count how many neighbors the remaining variant has in the **Mapper graph**.
3. Repeat by swapping which variant is removed.
4. **Pick the variant with the largest neighbor count**. For >2 variants, leave one in at a time and measure its connectivity.

---

## Data
Unstructured person-like records with fields such as:RecID, fname, lname, mname, address, city, state, zip, ssn
