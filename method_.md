# Methods, Experimental Design, and Evaluation for ML Papers

## Seminar sheet for CS / ML students
Audience: PhD students writing  papers 

## Goal
Learn how to:
- write the **Method section itself**,
- distinguish **Preliminaries** from **Method**,
- separate **method** from **experimental setup**,
- design experiments that support the paper’s claims,
- present evaluation in a way reviewers trust.

---

# 1. The four parts


| Part | Main question | Typical content |
|---|---|---|
| Preliminaries | What background does the reader need? | notation, standard definitions, task setup, known concepts |
| Method | What is the proposed approach? | model, architecture, algorithm, objective, novelty |
| Experimental Design | How will we test the claims? | tasks, datasets, baselines, metrics, protocol |
| Evaluation | What evidence do we report? | results, ablations, robustness, significance |

## Key distinction
- **Preliminaries** = shared language and standard setup
- **Method** = your new idea
- **Experimental design** = how you test it
- **Evaluation** = what happened when you tested it

If these are mixed together, the paper becomes hard to follow.

---

# 2. Preliminaries vs Method in ML papers

This distinction is especially important in ML writing.

## Preliminaries
The **Preliminaries** section gives the reader the background needed to understand the paper.

It usually contains:
- notation,
- standard definitions,
- problem setup,
- assumptions,
- short recap of known tools or objectives.

It is mostly **not your contribution**.

## Method
The **Method** section explains what **you propose**.

It usually contains:
- your model or algorithm,
- your architecture,
- your new loss / objective / update rule,
- your new mechanism,
- how the components interact,
- what is novel relative to prior work.

It is usually the **core contribution** of the paper.

## Teaching rule
> **Preliminaries = shared language**  
> **Method = your new idea**

## Quick test
- If removing it would make the notation or setup unclear, it belongs to **Preliminaries**.
- If removing it would remove the main contribution, it belongs to **Method**.

## Example in RL / MARL
### Preliminaries
- define MDP / Dec-POMDP,
- define observation, action, reward,
- define policy,
- define PPO objective if it is standard and reused.

### Method
- introduce your communication-aware PPO variant,
- define your message encoder,
- define your new regularizer,
- explain your modified training procedure.

---

# 3. When to include a separate Preliminaries section

Not every conference paper needs a section explicitly called **Preliminaries**.

Use it when:
- the paper depends on formal notation,
- the task setup is nontrivial,
- the audience may not know the exact framework,
- you need to define standard concepts before presenting your idea.

Skip or merge it when:
- the paper is short,
- the setup is standard and can be defined quickly inside Method,
- too much separation would make the paper fragmented.

## Common pattern
In many ML conference papers:

### 2. Preliminaries
- problem setting
- notation
- standard objective / background

### 3. Method
- proposed model
- proposed objective
- training algorithm

Another acceptable pattern is:

### 3. Method
#### 3.1 Problem formulation
#### 3.2 Proposed method
#### 3.3 Training objective

Here, the preliminaries are folded into the start of the Method section.

---

# 4. What belongs in the Method section?

The Method section should explain the proposed approach clearly enough that a technically trained reader can understand:
1. what problem you are solving,
2. what inputs and outputs the method uses,
3. how the method works,
4. how it is trained or optimized,
5. what is new relative to prior work.

It is not the place to describe all datasets, baselines, and result tables.

---

# 5. Core purpose of the Method section

A strong Method section must answer four questions:

| Question | What the reader wants to know |
|---|---|
| What is the formal problem? | task, notation, assumptions |
| What is the proposed method? | model, architecture, algorithm, procedure |
| How does it work? | mechanism, information flow, optimization |
| What is the novelty? | which part is new and why it matters |

---

# 6. Canonical structure of a Method section in ML

A common structure for ML conference papers is:

## 3. Method
### 3.1 Problem formulation
Define the task formally.

### 3.2 Proposed approach
Describe the model, algorithm, or framework.

### 3.3 Training objective / optimization
Explain loss functions, updates, learning rules, or inference.

### 3.4 Practical remarks
Complexity, implementation choices, or execution assumptions if needed.

This is different from:

## 4. Experimental setup
### 4.1 Benchmarks / datasets / environments
### 4.2 Baselines
### 4.3 Metrics
### 4.4 Training and evaluation protocol
### 4.5 Ablations / robustness tests

That separation is important.

---

# 7. 3.1 Problem formulation

This subsection defines the technical setting.

## It should include
- the task,
- input and output,
- symbols and notation,
- assumptions,
- what is observed at train and test time,
- any constraints that matter.

## Example
> We consider decentralized multi-agent route choice on a directed traffic network \(G=(V,E)\). At the beginning of each episode, each agent \(i\) is assigned an origin–destination pair and selects one route from a finite candidate set. During execution, agents observe only local traffic information and act independently. The objective is to minimize expected travel time under mixed human and autonomous traffic.

That is a Method subsection, not an experiment description.

## Common mistake
Writing only:
> We study routing with RL.

That is too vague. A reviewer cannot tell what the actual technical problem is.

---

# 8. 3.2 Proposed approach

This is the heart of the Method section.

It should explain:
- the overall idea,
- the architecture or algorithm,
- the sequence of operations,
- how information moves through the system,
- what component is new.

## Good structure for describing a method
1. High-level intuition
2. Formal definition
3. Component-by-component explanation
4. Training or inference workflow
5. Why it differs from prior work

## Recommended writing pattern
Start broad, then zoom in.

### A. One-paragraph overview
> We propose a decentralized communication-aware policy optimization framework in which each agent first encodes its local observation, exchanges a low-dimensional message with neighboring agents, and then selects a route using a shared policy network.

### B. Formal detail
Then define:
- observation \(o_i\),
- message \(m_i\),
- policy \(\pi_\theta(a_i \mid o_i, m_i)\),
- any value function, latent state, graph encoder, or loss term.

### C. Component explanation
Explain each new block and why it exists.

---

# 9. Writing the method: top-down principle

Students often start with equations too early.

A clearer order is:

1. **Intuition first**  
   What problem does the method solve?

2. **System view next**  
   What are the components?

3. **Formalization after that**  
   What are the equations?

4. **Algorithmic procedure last**  
   How is it trained or executed?

## Weak style
> Let \(h_i^t = f_\theta(o_i^t, m_i^t)\), where ...

The reader does not yet know what the method is for.

## Better style
> To stabilize decentralized coordination, each agent maintains a compact representation of nearby traffic and optional messages from its neighbors. This representation is then mapped to route preferences through a shared policy network. Formally, ...

---

# 10. What counts as novelty in the Method section?

The Method section should make the novelty explicit.

## Typical novelty types in ML methods
| Type | Example |
|---|---|
| New architecture | graph encoder with traffic-aware message passing |
| New objective | regularizer for belief consistency |
| New optimization rule | modified policy update |
| New decomposition | separate routing and coordination modules |
| New representation | latent state for opponent behavior |
| New framework | decentralized training-execution design |

## Good novelty sentence
> Unlike prior decentralized actor-critic methods, our approach augments each policy update with a belief-regularization term that explicitly models policy drift in neighboring agents.

This is much stronger than:
> We propose a novel framework.

---

# 11. 3.3 Training objective / optimization

After describing the model, explain how it is trained.

## Depending on the paper, this may include
- loss functions,
- policy gradients,
- Bellman targets,
- contrastive losses,
- variational objectives,
- regularizers,
- EM updates,
- inference procedure.

## Example structure
### Objective
> The overall objective combines expected return with a communication sparsity penalty:  
> \(L(\theta) = L_{\text{RL}}(\theta) + \lambda L_{\text{sparse}}(\theta)\).

### Update rule
> We optimize \(L(\theta)\) using PPO-style clipped updates with minibatch SGD.

### Execution
> At test time, agents communicate only one compressed message per decision step and act without centralized information.

## Common mistake
Only naming the optimizer:
> We use Adam.

That is not enough. The reader needs the training logic, not just the software detail.

---

# 12. Algorithms, pseudocode, and figures

For many ML papers, the Method section becomes much clearer if you add:
- one method diagram,
- one pseudocode block,
- one compact training loop description.

## Use a figure when
- the architecture has multiple interacting components,
- information flow is hard to explain in text,
- the method includes communication, memory, hierarchy, or graph structure.

## Use pseudocode when
- the algorithm has multiple stages,
- the training loop is non-standard,
- the update rule is difficult to explain in prose.

## Rule
Figures and algorithms should clarify the logic, not repeat the text.

---

# 13. What does not belong in the Method section?

Usually do **not** put these in the Method section unless tightly connected to the algorithm:
- full dataset descriptions,
- benchmark catalog,
- baseline list,
- metric definitions,
- full hyperparameter tables,
- large result discussions.

Those belong in **Experimental Setup** or **Results**.

A clean paper separates:
- **Preliminaries**: what the reader needs to know first
- **Method**: what you propose
- **Setup**: how you test it
- **Results**: what you found

---

# 14. After the Method section comes Experimental Design

Once the proposed method is clear, the next question is:

> How do we test whether it actually works?

That is the role of experimental design.

---

# 15. Start from claims, not from code

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

# 16. Core anatomy of an ML evaluation

Most empirical ML papers should clearly specify these elements:

| Element | Main question |
|---|---|
| Task | What problem are you solving? |
| Data / environment | On what dataset, simulator, or benchmark? |
| Baselines | Compared to what? |
| Metrics | How is success measured? |
| Protocol | Under what training and evaluation setup? |
| Ablations | Which component matters? |
| Robustness | Does it hold under perturbation or scale? |

---

# 17. Datasets, environments, and benchmarks

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
- [ ] Is this a recognized benchmark or clearly motivated custom environment?
- [ ] Does it reflect the claim I want to test?
- [ ] Does it contain enough variation in scale/difficulty?
- [ ] Can I compare against prior work on it?
- [ ] If custom, have I explained why standard benchmarks are insufficient?

---

# 18. Baselines: the most important design choice

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

## Baseline rule
Compare against:
1. the strongest relevant prior method,
2. the most standard method in the area,
3. a simple non-ML baseline when appropriate.

---

# 19. Metrics: measure what your claim actually says

A metric is the operational definition of success.

## Examples by claim
| Claim | Possible metrics |
|---|---|
| Better performance | accuracy, reward, return, F1, BLEU, travel time |
| Faster learning | sample efficiency, area under learning curve, steps to threshold |
| More stable | variance across seeds, confidence intervals, collapse rate |
| More robust | performance under noise, shift, perturbation |
| Scales better | runtime, memory, reward vs number of agents |
| Better calibrated / safer | calibration error, violation rate, collision rate |

## Good metric practice
Use:
- one or two primary metrics,
- a few secondary metrics,
- metrics aligned with the application.

---

# 20. Experimental protocol: fairness matters

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

## Minimal protocol statement
> All methods were trained under the same interaction budget, evaluated over 10 random seeds, and selected using the same validation protocol.

---

# 21. Random seeds, variance, and statistical reliability

In ML, single-run results are rarely convincing.

## Good practice
- report mean and standard deviation or confidence intervals,
- run multiple seeds,
- show variance where relevant,
- avoid cherry-picking best runs.

## Better reporting
> Our method improves mean return by 14% over MAPPO across 10 seeds and reduces variance in final performance.

Not:
> Our best run outperforms the baseline.

---

# 22. Ablation studies

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

---

# 23. Robustness and stress tests

Top ML papers increasingly test not only average-case performance but also failure modes.

## Useful robustness checks
- different seeds,
- noisy observations,
- partial observability,
- out-of-distribution test tasks,
- more agents / larger graphs,
- changed demand / perturbation,
- missing communication,
- adversarial or non-stationary conditions.

---

# 24. Reproducibility and implementation details

A reviewer should be able to understand enough to reproduce your setup.

## Include
- architecture summary,
- important hyperparameters,
- optimizer and learning rate,
- training steps / epochs,
- hardware if relevant,
- software stack if relevant,
- release plans for code and benchmarks if possible.

## Good sentence
> Full implementation details, hyperparameter ranges, and environment settings are provided in Appendix A.

---

# 25. Threats to validity

Strong papers acknowledge what the study does not prove.

## Common threats in ML papers
| Threat type | Example |
|---|---|
| Benchmark validity | toy tasks may not reflect real deployments |
| Internal validity | gains may come from better tuning rather than the method |
| External validity | results may not generalize to other datasets or scales |
| Metric validity | metric may not capture the practical goal |
| Compute validity | method may perform well only with much higher compute |

---

# 26. Reviewer-driven design

A useful way to design both the Method and the experiments is to imagine reviewer questions first.

## Typical reviewer attacks on the Method
- What exactly is new here?
- Is the method clearly defined?
- Why should this mechanism help?
- Is the objective well motivated?
- Is the algorithm reproducible?

## Typical reviewer attacks on the experiments
- Why these baselines?
- Why these benchmarks?
- Why this metric?
- Is the gain statistically reliable?
- Is the method just bigger or more tuned?
- What part of the method matters?
- Does it scale?
- Does it generalize?
- Is the comparison fair?

Design the paper so these questions are already answered.

---

# 27. Fill-in templates for students

## A. Preliminaries statement
> We consider **[problem setting]** with **[standard assumptions]**.  
> Let **[notation]** denote **[meaning]**.

## B. Problem formulation
> We study **[task]** under **[setting/assumptions]**.  
> The input is **[x]**, the output is **[y]**, and the objective is **[z]**.

## C. Method overview
> We propose **[method name]**, a **[type of approach]** that **[core idea]**.

## D. Novelty statement
> Unlike prior work, our method **[key distinction]**, which allows **[why it matters]**.

## E. Objective / training
> The method is trained by optimizing **[objective]**, which combines **[term 1]** and **[term 2]**.

## F. Claim to experiment
> We claim that **[method]** improves **[property]** relative to **[baseline]**.  
> To test this, we evaluate on **[benchmarks]** using **[metrics]** under **[protocol]**.

---

# 28. One bad example and one better example

## Weak method description
> We propose a novel framework for routing. The model uses neural networks and is trained with reinforcement learning.

Problems:
- no task definition,
- no mechanism,
- no novelty,
- no formalization,
- no training logic.

## Better method description
> We propose a decentralized communication-aware routing policy for simultaneous route choice in mixed traffic. Each agent encodes its local traffic observation, exchanges a compressed message with neighboring agents, and selects one route from a discrete candidate set using a shared policy network. To stabilize learning under non-stationarity, we add a belief-regularization term that penalizes inconsistent updates across neighboring policies. The resulting objective combines PPO-style policy optimization with communication sparsity regularization. Unlike prior decentralized routing methods that ignore inter-agent belief drift, our approach explicitly models coordination under changing policies.

---

# 29. Fast checklist before submission

## Preliminaries
- [ ] I include only background needed to understand the paper
- [ ] I define notation, setup, and standard concepts clearly
- [ ] I do not hide my novelty inside Preliminaries

## Method section
- [ ] I clearly define the task, inputs, outputs, and assumptions
- [ ] I explain the method top-down: intuition, components, equations, algorithm
- [ ] I state explicitly what is new
- [ ] I explain how the method is trained or optimized
- [ ] A technically trained reader could reproduce the core idea

## Experimental design
- [ ] My experiments directly test my main claims
- [ ] My benchmark choice is justified
- [ ] I include strong and relevant baselines
- [ ] My metrics match the claims I make
- [ ] My protocol is fair across methods
- [ ] I report multiple seeds and variance
- [ ] I include ablations for key components
- [ ] I include at least one robustness or stress test
- [ ] I disclose important implementation details
- [ ] I acknowledge the main limitations of the study

---

# 30. In-class exercise

Choose one planned paper or project and fill in:

## Preliminaries
> The reader needs to know ...

## Problem
> We study ...

## Inputs / outputs
> The input is ... and the output is ...

## Method idea
> Our method works by ...

## Main novelty
> Unlike prior work, we ...

## Training objective
> We optimize ...

## Main claim
> We claim that ...

## Benchmarks
> We evaluate on ...

## Baselines
> We compare against ...

## Metrics
> We measure ...

## Ablation
> We test the role of ...

## Limitation
> Our study still does not show ...

---

# Key takeaway

A strong ML paper has four clean layers:
1. **Preliminaries** — what the reader needs to know first,
2. **Method** — what you propose,
3. **Experimental design** — how you test it,
4. **Evaluation** — what evidence you obtain.

Students should learn to write them separately.
