# Finding the Gap, Reviewing Literature, and Positioning Your ML Paper

## Audience
CS / ML students writing conference papers.

## Goal
Learn how to:
1. find a real research gap,
2. write a literature review that synthesizes instead of listing papers,
3. position your contribution against prior work.

---
## 1. What counts as a research gap in ML/CS?

A **research gap** is not "nobody did exactly my dataset + my model."
A gap is a **meaningful limitation or unresolved question** in prior work.

In ML, good gaps usually come from one of these:

| Gap type | ML-style question | Example |
|---|---|---|
| Problem gap | What part of the problem is still not solved? | Existing MARL methods do not handle non-stationary mixed traffic well. |
| Assumption gap | What unrealistic assumption do prior papers make? | Prior work assumes centralized training signals or full observability. |
| Evaluation gap | What is not tested rigorously enough? | Methods are evaluated only on toy benchmarks, not realistic urban networks. |
| Comparison gap | What important baseline or ablation is missing? | Papers compare against weak baselines and omit decentralized alternatives. |
| Scalability gap | What breaks when the setting becomes realistic? | Performance degrades when the number of agents or graph size grows. |
| Robustness gap | What happens under noise, shift, or perturbation? | Methods are not tested under demand fluctuations or partial observability. |
| Theory gap | What is not explained formally? | Empirical improvements exist, but convergence behavior is not understood. |

### Bad gap
> Deep RL is important, but more work is needed.

### Better gap
> Existing decentralized MARL approaches for route choice are mainly evaluated in small synthetic settings and rarely model mixed autonomy, leaving their stability and scalability in realistic urban networks unclear.

---

## 2. How to find a gap from papers

When reading each paper, extract:

| Item | Question |
|---|---|
| Task | What problem do they solve? |
| Setting | What environment / data / benchmark do they use? |
| Method | What method family do they use? |
| Assumptions | What do they assume? |
| Evidence | What experiments / theory support the claim? |
| Limitation | What is missing, weak, or unrealistic? |

### Practical reading prompt
For each paper, write 2 lines:

> This paper shows that ...  
> However, it assumes / does not test / does not explain ...

Example:
> This paper shows that value-decomposition methods improve cooperative routing efficiency.  
> However, it assumes homogeneous agents and does not test mixed traffic with decentralized execution.

---

## 3. A gap formula that works in ML papers

Use this pattern:

> Prior work has shown **[what is known]**, but still relies on **[limiting assumption / weak evaluation / missing comparison]**, making it unclear whether **[important unresolved question]**.

Example:
> Prior work has shown that MARL can improve network-level traffic efficiency, but still relies heavily on small synthetic benchmarks and centralized training assumptions, making it unclear whether these methods remain stable under realistic mixed-traffic route choice.

---

## 4. Literature review in ML: synthesize, do not enumerate

A weak ML background section looks like this:

> Paper A uses PPO. Paper B uses QMIX. Paper C uses communication. Paper D studies routing.

That is a list, not a review.

A strong ML background section does three things:
1. **groups papers into families,**
2. **compares their assumptions and strengths,**
3. **shows what remains missing.**

### Good review paragraph template
> Existing work on **[topic]** can be grouped into **[family 1]**, **[family 2]**, and **[family 3]**.  
> **[Family 1]** performs well when **[condition]**, but struggles with **[limitation]**.  
> **[Family 2]** addresses **[advantage]**, although it typically assumes **[assumption]**.  
> **[Family 3]** improves **[property]**, yet has rarely been evaluated on **[important setting]**.  
> As a result, **[your gap statement]**.

### Example
> Existing work on multi-agent routing can be grouped into value-decomposition methods, actor-critic methods, and communication-based approaches. Value-decomposition methods are efficient in strongly cooperative tasks, but often struggle when coordination incentives are weak or partially misaligned. Actor-critic methods support richer policy classes, though they frequently depend on carefully tuned centralized training. Communication-based methods improve coordination, yet are rarely tested in realistic mixed-traffic route-choice settings. As a result, the empirical trade-offs between scalability, decentralization, and robustness remain unclear.

---

## 5. Best structure for ML background sections

For ML conference papers, this structure usually works best:

### Structure A — by method family
- value-based methods
- actor-critic methods
- communication / world-model / planning methods

### Structure B — by challenge
- non-stationarity
- partial observability
- scalability
- credit assignment
- evaluation realism

### Structure C — by benchmark setting
- toy benchmarks
- synthetic graphs
- realistic simulators
- real-world datasets

For most ML papers, combine **method family + challenge**.

## 6. Building your contribution

Your contribution is not "we apply method X."
Your contribution should state:

1. **what is new,**
2. **relative to what,**
3. **why it matters,**
4. **what evidence supports it.**

### Contribution formula
> We propose / present / show **[what]**, which differs from prior work by **[key distinction]** and enables **[why it matters]**.

Examples:
> We propose a decentralized communication-aware MARL framework for route choice that explicitly targets mixed-traffic settings, unlike prior work focused on cooperative toy benchmarks.

> We present a benchmark across realistic traffic networks that enables controlled comparison of IPPO, MAPPO, VDN, and QMIX under the same training budget.

> We show empirically that lightweight communication improves convergence stability, especially under non-stationary human–AV interaction.

---

## 7. Contribution ladder for ML papers

State contribution at 3 levels:

| Level | Question | Example |
|---|---|---|
| Method | What did you build? | A decentralized communication-aware policy learner |
| Evidence | What did you demonstrate? | It improves stability and travel time on realistic networks |
| Significance | Why should the field care? | It closes part of the gap between toy MARL benchmarks and deployment-relevant routing problems |

A strong paper usually has all 3.

---

## 8. CARS for ML introductions

Use **CARS = Create A Research Space**.

| Move | What it does | ML-style example |
|---|---|---|
| 1. Establish territory | Show the problem matters | Multi-agent learning in non-stationary environments remains a central challenge in RL. |
| 2. Establish niche | Show what is missing | Existing approaches often assume centralized information or evaluate only simplified benchmarks. |
| 3. Occupy niche | Present your paper | We propose and evaluate a decentralized framework for mixed-traffic route choice on realistic urban networks. |

### 5-sentence intro skeleton for ML papers
1. **Problem:** What technical problem matters?  
2. **Limitation:** What is wrong with prior work?  
3. **Method / study:** What do you do?  
4. **Evidence:** What do experiments / theory show?  
5. **Contribution:** Why does this matter?

---

## 9. Comparison table: the best tool for positioning

Fill this in before writing.

| Study | Task / setting | Method family | Strong point | Main limitation | Relation to our work |
|---|---|---|---|---|---|
| Paper A | Cooperative routing on small graphs | QMIX / VDN | Efficient coordination | No mixed traffic, toy scale | We test larger realistic networks |
| Paper B | Decentralized MARL | IPPO / MAPPO | Decentralized execution | No route-choice realism | We apply to realistic route choice |
| Paper C | Communication MARL | Message passing | Better coordination | Not evaluated in transportation | We test communication in routing |
| This work | Mixed-traffic route choice | Your method | ... | ... | ... |

### Why this table matters
It prevents vague novelty claims.
It forces you to answer:
- Who are the closest prior papers?
- What exactly do they assume?
- Where exactly is your contribution?

---

## 10. Fast checklist before writing

[ ] I can name the 3–5 closest papers to mine
[ ] I know their task, assumptions, and evaluation setting
[ ] My gap is specific, not generic
[ ] My gap is about a meaningful unresolved issue
[ ] My literature review is organized by ideas, not author names
[ ] I compare papers instead of just summarizing them
[ ] My contribution directly addresses the identified gap
[ ] I can explain in one sentence how my paper differs from prior work
[ ] I can defend why the difference matters
[ ] My introduction follows problem -> limitation -> method -> evidence -> contribution


⸻

## Fill-in exercise for students

A. Gap statement

Prior work on [topic] has shown [known result], but it still assumes / misses [limitation], making it unclear [open question].

B. Literature review paragraph

Existing work on [topic] can be grouped into [family 1], [family 2], and [family 3].
[Family 1] is strong at [x] but weak at [y].
[Family 2] addresses [x] yet assumes [y].
[Family 3] improves [x] but has not been tested on [y].
Therefore, [gap].

C. Contribution statement

We [propose / benchmark / analyze / show] [your contribution], which differs from prior work by [key distinction] and demonstrates [main finding / value].

⸻

### 12. One example from ML

Weak positioning

> We study MARL for routing and propose a new approach. Prior work has looked at routing, but not our exact setting.

Stronger positioning

> Prior work on MARL for routing has mainly focused on cooperative or simplified benchmark settings, often with centralized training assumptions. This leaves open whether decentralized agents can learn stable route-choice policies in mixed traffic with realistic network structure. We address this by evaluating communication-aware decentralized MARL on large urban traffic networks and comparing it against IPPO, MAPPO, VDN, and QMIX under a unified protocol. Our results show that communication improves convergence stability and reduces mean travel time in the harder mixed-traffic settings.
