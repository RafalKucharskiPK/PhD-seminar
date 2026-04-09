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


## Common mistake
Using only one narrow benchmark and making a broad claim.

### Weak
> Our method is better for multi-agent coordination.

### Better
> On six cooperative and mixed-motive benchmarks spanning 4 to 100 agents, our method improves return and remains stable under increasing non-stationarity.

---

# 6. Baselines

Weak baseline selection is one of the fastest ways to lose reviewer trust.

## Good baselines should be
- relevant,
- strong,
- representative,
- fairly tuned.

## Baseline categories
| Type | Purpose | Example |
|---|---|---|
| Standard baseline | Compare to common prior methods | PPO, DQN, MAPPO, QMIX |
| Closest prior work | Compare to the most similar published method | direct comparator paper |
| Simple heuristic | Show whether ML is actually needed | shortest path, greedy, random |
| Ablated version | Show the value of your own component | your method without communication |
| Oracle / upper bound | Provide reference if applicable | centralized or full-information variant |

## Reviewer question
> Why did you compare only against weak baselines?

If a strong relevant baseline exists and is omitted, reviewers will notice.

## Baseline rule
Compare against:
1. the strongest relevant prior method,
2. the most standard method in the area,
3. a simple non-ML or naive baseline when appropriate.

---

# 7. Metrics

A metric measure what your claim actually says.  


## Examples by claim
| Claim | Possible metrics |
|---|---|
| Better performance | accuracy, reward, return, F1, BLEU, travel time |
| Faster learning | sample efficiency, area under learning curve, steps to threshold |
| More stable | variance across seeds, confidence intervals, training collapse rate |
| More robust | performance under perturbation, domain shift, noise |
| Scales better | runtime, memory, reward vs number of agents |
| Better calibrated / safer | calibration error, violation rate, collision rate |

## Good metric practice
Use:
- one or two primary metrics,
- a few secondary metrics,
- metrics aligned with the actual application.

---

# 8. Design protocol

The protocol tells the reviewer whether the comparison is fair.

## Must specify
- train/test split or evaluation episodes,
- number of random seeds,
- compute budget,
- hyperparameter tuning policy,
- stopping criterion,
- model selection criterion,
- whether baselines use their best known settings,
- whether all methods see the same data and budget.

## Essential rule
Do not give your method advantages that baselines do not receive.

### Example of unfairness
- your model tuned for 100 runs,
- baselines run with default settings,
- different training budgets,
- different action spaces,
- different observations.

That is not a valid comparison.

## Minimal protocol statement
> All methods were trained under the same interaction budget, evaluated over 10 random seeds, and selected using the same validation protocol.

---

# 9. Random seeds, variance, and statistical reliability

In ML, single-run results are rarely convincing.

## Good practice
- report mean and standard deviation or confidence intervals,
- run multiple seeds,
- show variance where relevant,
- avoid cherry-picking best runs.

## In many ML settings
3 seeds is weak,  
5 is acceptable,  
10 is much stronger for noisy training.

## Better reporting
> Our method improves mean return by 14% over MAPPO across 10 seeds and reduces variance in final performance.

Not:
> Our best run outperforms the baseline.

---

# 10. Ablation studies

Ablations test which part of your method actually matters.

Without ablations, reviewers may think:
> The gain comes from extra parameters, more compute, or a hidden design choice.

## Typical ablation questions
- What happens if component X is removed?
- What happens if communication is disabled?
- What if reward shaping is removed?
- What if architecture depth changes?
- What if the regularizer weight is zero?

## Good ablation table
| Variant | Change | Result | Interpretation |
|---|---|---|---|
| Full model | none | best | full method |
| No module A | remove communication | lower performance | A contributes to coordination |
| No module B | remove regularizer | less stable | B stabilizes training |
| Larger model control | more parameters only | similar | gains are not only from size |

## Rule
Ablations should test the causal story of your method.

---

# 11. Robustness and stress tests

Top papers increasingly test not only average-case performance but also failure modes.

## Useful robustness checks
- different seeds,
- noisy observations,
- partial observability,
- out-of-distribution test tasks,
- more agents / larger graphs,
- changed demand / perturbation,
- missing communication,
- adversarial or non-stationary conditions.

## Why this matters
A method that works only in one narrow clean setup is often not convincing.

---

# 12. Reproducibility and implementation details

A reviewer should be able to understand enough to reproduce your setup.

## Include
- architecture summary,
- important hyperparameters,
- optimizer and learning rate,
- training steps / epochs,
- hardware if relevant,
- software stack if relevant,
- release plans for code and benchmarks if possible.

## Do not overload the main text
Put long parameter tables in the appendix if needed.

## Good sentence
> Full implementation details, hyperparameter ranges, and environment settings are provided in Appendix A.

Image, Docker, Capsule, ...

---

# 14. Canonical structure of a Methods section in ML

A practical structure for conference papers:

## 3. Method
### 3.1 Problem formulation
### 3.2 Proposed approach
### 3.3 Training objective / algorithm

## 4. Experimental setup
### 4.1 Benchmarks / datasets / environments
### 4.2 Baselines
### 4.3 Evaluation metrics
### 4.4 Training protocol and implementation details
### 4.5 Ablations and robustness tests

For more empirical benchmark papers:

## 3. Experimental design
### 3.1 Research questions
### 3.2 Tasks and datasets
### 3.3 Compared methods
### 3.4 Metrics
### 3.5 Evaluation protocol

---


# Reviewer-driven design

A useful way to design experiments is to imagine the reviewer questions first.

## Typical reviewer attacks
- Why these baselines?
- Why these benchmarks?
- Why this metric?
- Is the gain statistically reliable?
- Is the method just bigger or more tuned?
- What part of the method matters?
- Does it scale?
- Does it generalize?
- Is the comparison fair?

Design the study so these questions are already answered.

---

# Fill-in templates for students

## A. Claim to experiment
> We claim that **[method]** improves **[property]** relative to **[baseline]**.  
> To test this, we evaluate on **[benchmarks]** using **[metrics]** under **[protocol]**.

## B. Baseline justification
> We compare against **[baseline 1]**, **[baseline 2]**, and **[baseline 3]** because they represent **[standard family]**, **[closest prior work]**, and **[simple reference]**, respectively.

## C. Metric justification
> We use **[primary metric]** as the main measure of **[goal]**, and report **[secondary metrics]** to capture **[stability / efficiency / robustness]**.

## D. Protocol statement
> All methods are trained with the same **[budget / data / seeds / stopping rule]** and evaluated under the same **[test conditions]**.

## E. Ablation statement
> To isolate the effect of each component, we evaluate variants that remove **[A]**, **[B]**, and **[C]** while keeping the rest of the pipeline fixed.



---

# Fast checklist before submission

- [ ] My experiments directly test my main claims
- [ ] I clearly define the task, inputs, outputs, and assumptions
- [ ] My benchmark choice is justified
- [ ] I include strong and relevant baselines
- [ ] I explain why each baseline is included
- [ ] My metrics match the claims I make
- [ ] My protocol is fair across methods
- [ ] I report multiple seeds and variance
- [ ] I include ablations for key components
- [ ] I include at least one robustness or stress test
- [ ] I disclose important implementation details
- [ ] I acknowledge the main limitations of the study




