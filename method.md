# Methods, Experimental Design, and Evaluation for ML Papers

## Seminar sheet for CS / ML students
Audience: students writing empirical papers for NeurIPS, ICML, ICLR, AAAI, AISTATS, ACL, EMNLP, CVPR, ECCV, KDD, WWW.

## Goal
Learn how to turn a research idea into a convincing empirical study:
- define the claim,
- choose the right baselines,
- select metrics,
- design fair experiments,
- write the Methods section clearly.

---

# 1. What is the Methods section doing?

The Methods section is not just a technical description of your model.

Its job is to make the reader believe that:
1. your method is clearly defined,
2. your experiments actually test your claims,
3. your comparisons are fair,
4. your evidence is reproducible.

A strong ML paper does not only ask:
> Is the method new?

It also asks:
> Is the evaluation credible?

---

# 2. Start from claims, not from code

Every ML paper makes claims.  
Your experiments should be designed to test those claims directly.

## Typical ML claims
| Claim type | Example |
|---|---|
| Performance claim | Our method achieves higher return / accuracy / reward |
| Efficiency claim | Our method learns faster or with fewer samples |
| Robustness claim | Our method performs better under noise, shift, perturbation |
| Scalability claim | Our method handles larger graphs, more agents, longer horizons |
| Component claim | Component X is responsible for the gain |
| Generalization claim | The method transfers to new tasks / seeds / environments |
| Theory-linked claim | The empirical behavior matches a theoretical property |

## Rule
For every major claim, ask:

> What experiment would convince a skeptical reviewer?

If you cannot answer that, the study design is not ready.

---

# 3. Core anatomy of an ML evaluation

Most empirical ML papers should clearly specify these seven elements:

| Element | Main question |
|---|---|
| Task | What problem are you solving? |
| Data / environment | On what dataset, simulator, or benchmark? |
| Method | What exactly is your approach? |
| Baselines | Compared to what? |
| Metrics | How is success measured? |
| Protocol | Under what training and evaluation setup? |
| Ablations / robustness | Why does it work, and does it hold up? |

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

That is much better than:
> We study traffic routing with RL.

## For ML students
Be explicit about:
- supervised / unsupervised / RL / MARL,
- offline vs online,
- centralized training vs decentralized execution,
- full vs partial observability,
- single-shot vs sequential decision making.

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

## Benchmark checklist
```md
[ ] Is this a recognized benchmark or clearly motivated custom environment?
[ ] Does it reflect the claim I want to test?
[ ] Does it contain enough variation in scale/difficulty?
[ ] Can I compare against prior work on it?
[ ] If custom, have I explained why standard benchmarks are insufficient?
