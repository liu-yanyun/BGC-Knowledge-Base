# Domain Modules in BGCs

This page introduces the most common **biosynthetic domains** found in biosynthetic gene clusters (BGCs), especially in **polyketide synthases (PKSs)** and **nonribosomal peptide synthetases (NRPSs)**. It also explains how **domain detection using HMMs (Hidden Markov Models)** is performed using tools like **HMMER**.

---

## 🔧 Core PKS Domains

| Domain           | Name                                                      | Function                                                           |
| ---------------- | --------------------------------------------------------- | ------------------------------------------------------------------ |
| **KS**           | Ketosynthase                                              | Catalyzes chain elongation by forming C–C bonds between acyl units |
| **AT**           | Acyltransferase                                           | Loads extender units (e.g., malonyl-CoA) onto ACP                  |
| **DH**           | Dehydratase                                               | Removes water to create double bonds in the growing chain          |
| **KR**           | Ketoreductase                                             | Reduces keto groups to hydroxyl groups (C=O to C–OH)               |
| **ACP** / **PP** | Acyl Carrier Protein / Phosphopantetheinyl-binding domain | Carries the growing molecule on a flexible arm                     |

Each **elongation module** in a Type I PKS typically contains:

> **\[KS] – \[AT] – \[DH] – \[KR] – \[ACP]**

These domains work together in an assembly-line fashion to build complex polyketide molecules.

---

## 🔧 Core NRPS Domains

| Domain  | Name                                    | Function                                 |
| ------- | --------------------------------------- | ---------------------------------------- |
| **A**   | Adenylation                             | Selects and activates an amino acid      |
| **C**   | Condensation                            | Forms peptide bonds between amino acids  |
| **PCP** | Peptidyl Carrier Protein (aka T domain) | Carries the growing peptide              |
| **TE**  | Thioesterase                            | Releases the final product from the NRPS |

NRPS modules often follow the logic:

> **\[C] – \[A] – \[PCP]**

Each module is responsible for incorporating **one specific amino acid** into the final nonribosomal peptide.

---

## 🧠 What Are HMMs and How Do They Detect Domains?

### Hidden Markov Models (HMMs)

HMMs are statistical models trained on **multiple sequence alignments** of known domains. They capture:

* Which residues are conserved
* Which positions tolerate insertions or deletions
* The likelihood of observing certain amino acids in specific positions

### HMMER Workflow (Simplified)

1. A database of trained HMM profiles (e.g., for KS, AT, KR domains) is built from known sequences
2. A protein is scanned using **HMMER** (`hmmscan`), comparing it to all profiles
3. For each domain match, HMMER reports:

   * **Domain type** (e.g., PKS\_KS)
   * **E-value** and **bitscore** (confidence)
   * **Start/end positions** in the protein

This allows tools like **antiSMASH** and **GECCO** to precisely identify domain types and their coordinates within large multi-domain enzymes.

---

## 🧬 Visual Representation

Imagine this example PKS gene (protein):

```
[KS]---[AT]---[DH]---[KR]---[ACP]
```

Each block is a domain detected by matching to an HMM profile.

These domains are annotated in `.gbk` files using tags like `/aSDomain="PKS_KS"` or `/sec_met_domain="PKS_AT"`.

---

## 📌 Summary

* PKSs and NRPSs are modular enzymes with repeatable domains
* Domain detection is powered by HMMs and tools like HMMER
* Understanding which domains are present helps predict the structure of the resulting natural product

Next up: see how these domain predictions appear in **antiSMASH output files**.
