# Methods, Experimental Design, and Evaluation 

## Seminar sheet for CS  students

Audience: PhD students writing CS papers

## Goal

Turn a research idea into a convincing study:
- define the **claim**,
- choose the right **baselines**,
- select **metrics**,
- design fair **experiments**,
- write the Methods section clearly.

---

# 1. What is the Methods section doing?

The Methods section is not just a technical description of your model - it is for the reader to **believe in your claim**.

> Intro: "I do this (important and new)" --> Method: "I really do this" --> Results: "See?"

Its job is to make the reader believe that:
1. your method is clearly defined,
2. your experiments actually test your claims,
3. your comparisons are fair,
4. your evidence is reproducible.

A strong paper does not only ask:
> Is the method new?

It also asks:
> Is the evaluation credible?

---

# 2. Start from claims, not from code

Almost every paper makes claims (hypotheses).  
Your experiments should be designed to test/support those claims directly.

## Typical claims
| Claim type | Example |
|---|---|
| Performance claim | Our method achieves higher accuracy  |
| Efficiency claim | Our method learns faster or with fewer samples |
| Robustness claim | Our method performs better under noise, shift, perturbation |
| Scalability claim | Our method handles more agents |
| Component claim | Component X is responsible for the gain |
| Generalization claim | The method transfers to new tasks / seeds / environments |
| Theory-linked claim | The empirical behavior matches a theoretical property |

## Rule
For every major claim, ask:

> What experiment would convince a skeptical reviewer?

If you cannot answer that, the study design is not ready.

---

# 3. Core anatomy of an evaluation

Most empirical ML papers should clearly specify:

| Element | Main question |
|---|---|
| Task | What problem are you solving? |
| Data / environment | On what dataset, simulator, or benchmark? |
| **Method** | What exactly is your approach? |
| Baselines | Compared to what? |
| Metrics | How is success measured? |
| Setup | Under what training and evaluation setup? |
| Ablations / robustness | Why does it work? |

---

# 4. Task formulation

A Methods section should begin by stating the task precisely.

## Good task description includes
- problem input,
- desired output,
- constraints,
- what is observed at train and test time.

## Example
> We study decentralized route choice in mixed traffic. At each episode, each autonomous vehicle selects one route from a discrete candidate set connecting its origin and destination. Agents observe local information and execute policies independently at test time.


## Be explicit 

---

# 5. Datasets, environments, and benchmarks

Your benchmark choice is part of your argument.

Reviewers often ask:
- Why these datasets?
- Are they standard?
- Are they realistic?
- Are they diverse enough?
- Are they too easy?

## Good benchmark selection should justify
- relevance,
- difficulty,
- diversity,
- comparability to prior work.


