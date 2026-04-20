# Results, Storyline, and Findings for ML Papers

## Seminar sheet for CS / ML students
Audience: students writing scientific papers for NeurIPS, ICML, ICLR, AAAI, AISTATS, ACL, EMNLP, CVPR, ECCV, KDD, WWW.

## Goal
Learn how to:
- build a clear **results storyline**,
- present evidence that supports the paper’s claims,
- design readable **figures, tables, and infographics**,
- write result paragraphs that interpret rather than merely describe,
- synthesize results into **findings** and limitations.

---

# 1. What is the Results section doing?

The Results section is where the paper proves its case.

It should show that:
1. the experiments answer the research questions,
2. the evidence supports the claims,
3. the reader can understand the main message quickly,
4. the paper is honest about uncertainty, variance, and limitations.

A strong Results section is not a dump of numbers.  
It is a structured argument built from evidence.

---

# 2. Results are not the same as Discussion

Students often mix these up.

| Part | Main question | Typical content |
|---|---|---|
| Results | What did we observe? | main outcomes, tables, figures, statistical patterns |
| Discussion / Findings | What do the results mean? | interpretation, implications, mechanism, comparison to expectations |
| Limitations | What do the results not prove? | scope, threats to validity, missing evidence |

## Teaching rule
> **Results = evidence**  
> **Discussion / findings = interpretation**

In many ML conference papers, Results and Discussion are partly merged.  
But the writing should still distinguish:
- what the evidence is,
- what the authors infer from it.

---

# 3. Start from claims and research questions

A strong Results section is organized around the paper’s claims, not around the order in which experiments were run.

## Good organizing principle
For each claim or research question:
1. state what is being tested,
2. present the key evidence,
3. interpret the result,
4. explain what conclusion is justified.

## Example claim-to-results structure
| Claim | Evidence |
|---|---|
| Our method improves performance | main benchmark table |
| Our method is more stable | variance plot across seeds |
| Communication matters | ablation table |
| The method scales | result vs number of agents / graph size |
| The method is robust | perturbation or OOD test |

This keeps the section logical and reviewer-friendly.

---

# 4. Build a results storyline

A paper should tell one main story, not five unrelated mini-stories.

## Canonical ML results storyline
A useful order is:

1. **Headline result**  
   Does the method work on the main task?

2. **Breadth / generality**  
   Does it work across multiple benchmarks or settings?

3. **Why it works**  
   What do ablations reveal?

4. **How reliable it is**  
   What do variance, seeds, and robustness show?

5. **Where it fails / limits**  
   Where are the gains smaller, unstable, or absent?

## Example storyline
- Main table: our method beats strong baselines on realistic networks
- Learning curves: gains are not only final-score effects; training is also more stable
- Ablation: communication drives most of the improvement
- Stress test: benefits remain under increased demand and more agents
- Limitation: advantages shrink in very small networks with low congestion

That is a coherent narrative.

---

# 5. The headline result comes first

Do not hide the main contribution behind secondary analyses.

A reviewer should be able to answer within one minute:
- what is the main empirical result,
- where it is shown,
- how large it is,
- compared to what.

## Good headline sentence
> Table 1 shows that the proposed method achieves the lowest mean travel time on both urban networks, outperforming IPPO, MAPPO, QMIX, and shortest-path routing.

## Weak headline sentence
> We first report a number of experimental outcomes across several settings.

The reader should not have to guess what matters most.

---

# 6. How to write a results paragraph

A good results paragraph usually has four moves:

1. **Reference the evidence**  
   Point to the relevant figure or table.

2. **State the main pattern**  
   Say clearly what it shows.

3. **Interpret the pattern**  
   Explain why it matters.

4. **Qualify if needed**  
   Mention exceptions, uncertainty, or scope.

## Template
> **Figure/Table X** shows that **[main pattern]**.  
> Compared with **[baseline]**, **[method]** improves **[metric]** by **[amount]**.  
> This suggests that **[interpretation]**.  
> The effect is strongest in **[condition]**, while **[exception or limitation]**.

## Example
> Table 2 shows that the proposed method consistently reduces mean travel time relative to all learning-based baselines. The largest gains occur in the larger mixed-traffic network, where travel time falls by 14% compared with MAPPO and by 19% compared with QMIX. This suggests that the method benefits particularly from settings with stronger inter-agent coupling and route competition. In the smallest network, however, the gap narrows, indicating that coordination brings less benefit when congestion is limited.

---

# 7. Describe, do not merely read the table

A common mistake is “narrating the numbers” row by row.

## Weak style
> In Table 1, our method gets 12.3, MAPPO gets 13.7, QMIX gets 14.0, and IPPO gets 13.9.

This is not analysis.

## Better style
> Table 1 shows a consistent pattern: the proposed method outperforms both actor-critic and value-decomposition baselines on every benchmark, with the largest improvements in the most congested settings.

The numbers stay in the table.  
The text should extract the pattern and meaning.

---

# 8. Presenting tables well

Tables are best when the reader needs exact values and direct comparison.

## Use a table when
- you compare several methods across several benchmarks,
- exact numbers matter,
- you want the reader to compare rows and columns precisely.

## Good table design rules
- keep only the essential metrics in the main paper,
- order rows and columns meaningfully,
- bold the best result when appropriate,
- include uncertainty if relevant,
- avoid overcrowding,
- use consistent decimal precision,
- explain abbreviations in the caption or note.

## Good caption
> **Table 1.** Mean travel time (lower is better) across two urban networks. Results are averaged over 10 random seeds; standard deviations are reported in parentheses.

A table without a caption is not self-explanatory.

---

# 9. Presenting figures well

Figures are best when the reader needs to see patterns, trends, or distributions.

## Use a figure when
- you show learning dynamics,
- you show scaling trends,
- variance matters,
- the shape of the effect matters,
- the visual pattern is more important than exact values.

## Common useful ML figures
- learning curves,
- bar charts for aggregate comparison,
- scatter plots for trade-offs,
- box plots / violin plots for distributions,
- sensitivity plots,
- calibration or reliability curves,
- confusion matrices,
- schematic infographics summarizing findings.

## Figure rule
One figure should communicate one main message.

Do not overload a figure with too many subplots unless they support a single unified claim.

---

# 10. Figures and tables should complement each other

A good paper often uses:
- **tables** for exact benchmark comparison,
- **figures** for trends, dynamics, and intuition.

## Example pairing
- Table 1: final performance across benchmarks
- Figure 2: learning curves over training
- Table 3: ablation results
- Figure 4: robustness under demand increase

This lets the reader see both precise outcomes and broader patterns.

---

# 11. Captions matter more than students think

A caption should let the figure or table make sense without the whole body text.

## Good caption includes
- what is shown,
- what metric is used,
- what direction is better,
- what conditions or datasets are included,
- what averaging or uncertainty is reported.

## Weak caption
> Results on our datasets.

## Better caption
> **Figure 3.** Mean episodic return during training on the Cologne network. Curves show averages over 10 seeds; shaded regions denote standard error. Higher is better.

---

# 12. Reporting uncertainty and variability

ML results are often noisy.  
If the method is unstable, the paper should not hide that.

## Good practice
- report mean and standard deviation, confidence interval, or standard error,
- use multiple seeds,
- show variance in plots where it matters,
- mention instability when present,
- avoid reporting only the best run.

## Good sentence
> Although the proposed method has the best mean performance, Figure 4 shows larger variance in the largest benchmark, suggesting sensitivity to initialization under extreme congestion.

That is honest and informative.

---

# 13. Statistical significance in ML papers

Not every conference paper requires formal hypothesis testing, but students should know the principle:

The question is not:
> Is the number bigger?

The question is:
> Is the difference reliable?

## When significance or reliability matters
- small gains,
- noisy tasks,
- high variance methods,
- strong claims about superiority,
- reviewer skepticism.

## Safer reporting style
> The gain is consistent across 10 seeds and exceeds one standard deviation on the two largest benchmarks.

This is often more useful than a superficial p-value with poor design.

---

# 14. Ablations are results, not methods

Ablation results should answer:
> Which part of the method explains the gain?

## Good ablation writing
> Table 4 shows that removing communication causes the largest performance drop, while removing the regularizer mainly increases variance rather than lowering the mean. This indicates that communication drives the performance gain, whereas the regularizer primarily stabilizes training.

Notice:
- evidence,
- pattern,
- interpretation.

Not just a list of numbers.

---

# 15. Negative results and limitations belong in the story

Strong papers do not pretend the method wins everywhere.

## You should say when
- the gain disappears in some settings,
- a baseline is stronger on a subset,
- the method is slower,
- the method is less stable in one regime,
- an ablation result is inconclusive.

## Example
> On the smallest benchmark, the heuristic baseline performs comparably to the learned methods, suggesting that the benefit of coordination is limited when congestion is weak and route interactions are sparse.

This increases credibility.

---

# 16. From results to findings

A **result** is an observed outcome.  
A **finding** is a synthesized conclusion supported by several results.

## Example
### Result
> Communication improves mean return by 8–12% in the large networks.

### Finding
> Lightweight inter-agent communication is most valuable in large, congested routing environments where decentralized agents must adapt to one another’s non-stationary choices.

The finding is broader and more interpretive, but still evidence-based.

---

# 17. How to synthesize results into findings

A good synthesis asks:
- what pattern repeats across experiments?
- what mechanism is supported?
- under what conditions does the effect appear?
- what conclusion is safe to claim?

## Synthesis template
> Taken together, the results indicate that **[main finding]**.  
> This conclusion is supported by **[main evidence 1]**, **[main evidence 2]**, and **[main evidence 3]**.  
> The effect appears strongest under **[condition]** and weaker under **[condition]**.

## Example
> Taken together, the results indicate that communication-aware decentralization improves route-choice performance primarily by reducing instability in strongly coupled traffic settings. This conclusion is supported by the main benchmark gains, the reduced variance across seeds, and the communication ablation. The effect is strongest in larger congested networks and weaker in small low-congestion scenarios.

---

# 18. A useful structure for the Results section

A practical Results section for ML papers can look like this:

## 5. Results
### 5.1 Main benchmark comparison
Does the method outperform strong baselines?

### 5.2 Learning dynamics and stability
How does training evolve? Is it stable across seeds?

### 5.3 Ablation study
Which components matter?

### 5.4 Robustness / scalability / stress tests
Does the method hold up under harder conditions?

### 5.5 Summary of findings
What broader conclusions can be drawn?

This structure usually reads much better than a random experiment order.

---

# 19. Results paragraphs should not overclaim

Students often move too quickly from evidence to grand claims.

## Weak
> These results prove that our method is the best approach for multi-agent routing.

## Better
> These results suggest that the proposed method is a strong option for decentralized mixed-traffic routing, particularly in larger congested networks.

Use language that matches the evidence:
- shows,
- suggests,
- indicates,
- is consistent with,
- supports.

Avoid:
- proves,
- definitively establishes,
- universally outperforms,
unless the evidence is truly overwhelming.

---

# 20. Common mistakes in ML Results sections

| Mistake | Why it is weak |
|---|---|
| Dumping many tables without a story | reader cannot tell what matters |
| Reporting only best runs | hides variance and instability |
| Reading numbers row by row | no synthesis or interpretation |
| Hiding weak cases | reduces trust |
| Using unreadable plots | evidence becomes inaccessible |
| Mixing methods and results | logic becomes confusing |
| Claiming too much from one benchmark | poor external validity |
| No ablation interpretation | unclear why the method works |

---

# 21. Fast checklist before submission

## Storyline
- [ ] I know the one main empirical story of the paper
- [ ] The Results section is organized around claims, not experiment chronology
- [ ] The headline result appears early

## Evidence presentation
- [ ] Each table or figure supports a clear point
- [ ] Captions explain what is shown and how to read it
- [ ] I report uncertainty or variance where needed
- [ ] I use tables for exact comparison and figures for patterns

## Writing
- [ ] My paragraphs interpret patterns, not just repeat numbers
- [ ] I distinguish evidence from inference
- [ ] I state limitations or weak cases honestly
- [ ] My conclusions do not overclaim beyond the evidence

---

# 22. Fill-in templates for students

## A. Headline result
> Table/Figure **[X]** shows that **[main result]** compared with **[baseline(s)]** on **[task/benchmark]**.

## B. Pattern and interpretation
> The main pattern is that **[pattern]**.  
> This suggests that **[interpretation]**.

## C. Qualification
> The effect is strongest in **[condition]**, while **[exception or weaker case]**.

## D. Ablation
> Removing **[component]** causes **[change]**, indicating that **[role of component]**.

## E. Synthesis into finding
> Taken together, these results indicate that **[finding]**, especially under **[condition]**.

---

# 23. One bad example and one better example

## Weak results writing
> Table 2 reports all benchmark results. Our method gets the best score on most tasks. Figure 3 shows the learning curves. Table 4 shows the ablations. These results demonstrate the effectiveness of our method.

Problems:
- generic,
- no pattern extraction,
- no interpretation,
- no qualification,
- no storyline.

## Better results writing
> Table 2 provides the main benchmark comparison and shows that the proposed method achieves the best average performance on four of five routing settings, with the largest gains on the two most congested networks. Figure 3 complements this result by showing that the improvement is not only a final-score effect: training is also more stable across seeds, with fewer collapses in late training. Table 4 helps explain this pattern, as removing the communication module substantially reduces performance while removing the regularizer mostly increases variance. Taken together, these results suggest that the method’s advantage comes primarily from improved decentralized coordination rather than from increased model capacity alone.

---

# 24. In-class exercise

Choose one of your current projects and fill in:

## Main claim
> Our paper claims that ...

## Headline result
> The main result is shown in ...

## Figure or table
> We should use a table / figure here because ...

## Main pattern
> The pattern is ...

## Interpretation
> This suggests ...

## Qualification
> The effect is weaker when ...

## Ablation finding
> Removing ... shows that ...

## Final finding
> Taken together, the results indicate that ...

---

# Key takeaway

A strong Results section is not a warehouse of outputs.

It is a carefully ordered evidence-based story where:
- claims are matched to experiments,
- tables and figures make the evidence readable,
- paragraphs extract patterns and meaning,
- multiple results are synthesized into findings,
- limitations are acknowledged honestly.
