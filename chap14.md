# Part V — Inventory

---

# Chapter 14 — Classification of Results

*(Revised with exercises)*

## 14.1 Purpose of this chapter

This chapter is not a conclusion. It is an inventory.

The book has developed a mathematical framework — complex cost geometry — and applied it to reinforcement learning and policy optimization. Along the way, it has stated theorems, propositions, and conjectures. Some are proven in full. Some are proven under stated conditions. Some are conjectural. Some are open problems.

This chapter classifies every result in the book. Its purpose is to make the framework's status explicit, so that a reader can see at a glance what has been established and what remains to be done.

**The classification has five categories:**

- **Proven:** the result is established by a complete proof given in the book (or in cited work).
- **Conditional:** the result is proven under stated hypotheses that are not always satisfied.
- **Conjectural:** the result is stated as a conjecture with supporting motivation, but no proof.
- **Open:** the result is stated as a problem; neither a proof nor a counterexample is known.
- **Axiom:** the result is assumed rather than proven; it is a foundational claim of the framework.

Every numbered result in the book is classified below.

## 14.2 Results by chapter

### Chapter 2 — The Complex Quasi-Metric

| Result | Status | Location |
|---|---|---|
| Definition of complex quasi-metric | Definition | §2.1 |
| Modulus is a classical quasi-metric | Proven | Prop 2.1.7 |
| Properties of potential-difference debt | Proven | Prop 2.2.3 |
| Characterization of potential-difference debt | Proven | Prop 2.2.4 |
| Reverse triangle inequality | Proven | Prop 2.3.1 |
| Modulus of expectation (Jensen) | Proven | Prop 2.3.2 |
| Continuity of the modulus | Proven | Prop 2.3.4 |
| $\gamma$-distance basic properties | Proven | Prop 2.4.2 |
| Triangle inequality for $d_\gamma$ | Proven | Prop 2.4.3 |

### Chapter 3 — The Potential-Difference Form

| Result | Status | Location |
|---|---|---|
| Telescoping identity | Proven | Thm 3.1.3 |
| Reduction to discounted average | Proven | Cor 3.1.5 |
| Non-negativity under submartingale | Proven | Prop 3.2.2 |
| Bayesian learning satisfies submartingale | Proven | Cor 3.2.3 |
| One-step imaginary utility equals mutual information | Conditional (Assumption 3.3.1) | Prop 3.3.3 |
| Imaginary Q-value as discounted mutual information | Conditional (Assumption 3.3.1) | Cor 3.3.4 |
| Real Q-value is discounted cumulative cost | Proven | Prop 3.4.1 |
| No telescoping for the real part | Proven | Prop 3.4.2 |
| Evaluation contraction | Proven | Thm 3.5.2 |
| Existence and uniqueness of $Q^\pi$ | Proven | Cor 3.5.3 |
| Bound on the fixed point | Proven | Cor 3.5.4 |
| Component Bellman equations | Proven | Cor 3.5.5 |

### Chapter 4 — The $\gamma$-Distance Family

| Result | Status | Location |
|---|---|---|
| Basic properties | Proven | Prop 4.1.2 |
| Monotonicity in $\gamma$ | Proven | Prop 4.1.3 |
| Endpoints | Proven | Prop 4.1.4 |
| Continuity in $\gamma$ | Proven | Prop 4.1.5 |
| Equivalence bounds | Proven | Prop 4.2.1 |
| Topological equivalence for $\gamma > 0$ | Proven | Cor 4.2.2 |
| Level sets as circles and ellipses | Proven | Prop 4.3.2 |
| Optimal paths depend on $\gamma$ | Proven | Prop 4.4.2 |
| Modulus-sup bound | Proven | Prop 4.5.1 |
| Sufficient contraction condition $\gamma < 1/\sqrt{2}$ | Proven (sufficient, not sharp) | Prop 4.5.2 |
| Phase information lost at $\gamma = 1$ | Proven | Prop 4.6.2 |

### Chapter 5 — Asymmetry and Bitopological Structure

| Result | Status | Location |
|---|---|---|
| Properties of asymmetry | Proven | Prop 5.1.2 |
| Forward and backward balls coincide iff symmetric | Proven | Prop 5.2.2 |
| Independence of $\gamma$ for $\gamma > 0$ | Proven | Prop 5.3.5 |
| $d_{\text{avg}}$ is a pseudometric | Proven | Prop 5.4.4 |
| Topological chain | Proven | Prop 5.4.6 |
| Equilibrium hierarchy | Proven | Thm 5.5.3 |
| Local asymmetry range $[0, 2]$ | Proven | Prop 5.6.2 |
| Symmetry points are closed | Proven | Prop 5.6.4 |
| Global symmetry implies local symmetry | Proven | Prop 5.6.5 |
| Fixed points are in all equilibrium sets | Proven | Prop 5.7.2 |

### Chapter 6 — Equilibrium Structure

| Result | Status | Location |
|---|---|---|
| Fixed points satisfy equilibrium condition | Conditional (continuity) | Prop 6.1.3 |
| Submartingale implies non-negative imaginary part | Proven | Prop 6.2.4 |
| Bounded potential gives bounded imaginary part | Proven | Prop 6.2.5 |
| Phase constraint under submartingale | Proven | Prop 6.2.8 |
| $E_\tau$ is closed | Proven | Prop 6.3.1 |
| Monotonicity of equilibrium sets | Proven | Prop 6.3.2 |
| Non-emptiness under compactness | Conditional (compactness) | Prop 6.3.4 |
| Equality conditions for equilibrium sets | Conditional | Prop 6.3.5 |
| Global symmetry collapses hierarchy | Proven | Prop 6.4.4 |
| Convergence under Lyapunov contraction | Conditional (Lyapunov condition) | Thm 6.6.2 |

### Chapter 7 — The Complex Bellman Equation

| Result | Status | Location |
|---|---|---|
| Absolute convergence of return | Proven | Prop 7.1.6 |
| Evaluation operator maps $\mathcal{Q}$ into itself | Proven | Prop 7.2.2 |
| Evaluation contraction | Proven | Thm 7.2.3 |
| Existence and uniqueness of $Q^\pi$ | Proven | Cor 7.2.4 |
| Bound on the fixed point | Proven | Cor 7.2.5 |
| Component Bellman equations | Proven | Prop 7.3.1 |
| Closed form for $Q_I^\pi$ | Conditional (potential-difference form) | Cor 7.3.3 |
| Real case is special case | Proven | Prop 7.4.1 |
| No order structure required for evaluation | Proven | Prop 7.4.2 |
| Two-state cMDP example | Illustration | Ex 7.5.4 |

### Chapter 8 — The Optimality Operator and Its Gap

| Result | Status | Location |
|---|---|---|
| Argument discrepancy bound | Proven | Prop 8.2.1 |
| Three faces of the obstruction | Discussion | §8.3 |
| Scalar modulus contraction | Proven | Prop 8.4.1 |
| Counterexample problem | Open | Problem 8.4.3 |
| Contraction conjecture | Conjectural | Conj 8.4.5 |
| Non-negative imaginary part at fixed point | Conditional (submartingale) | Prop 8.5.1 |
| Non-negative real part at fixed point | Proven | Prop 8.5.2 |
| First-quadrant fixed point | Conditional (submartingale) | Cor 8.5.3 |
| Contraction on phase cone | Conditional (phase cone + value bound) | Prop 8.6.2 |
| Contraction when $M \le \|Q_1 - Q_2\|$ | Conditional | Cor 8.6.3 |
| Local contraction near equilibrium | Conjectural | Conj 8.6.5 |

### Chapter 9 — The Two-Selector Formulation

| Result | Status | Location |
|---|---|---|
| Two-selector operator well-defined | Proven | Prop 9.3.3 |
| Product space is a Banach space | Proven | Prop 9.4.2 |
| Naive contraction proof fails | Proven (failure) | Thm 9.5.1 |
| Gap structure | Proven | Prop 9.6.3 |
| Gap is action-independent | Proven | Cor 9.6.4 |
| Gap identity | Proven | Cor 9.6.5 |
| Cross-term depends only on utility | Proven | Remark 9.6.6 |
| Gap-vanishing conjecture | Conjectural | Conj 9.6.7 |
| Gap-stable selector contraction | Conditional | Prop 9.7.2 |
| Soft Bellman operator is a contraction | Conditional (temperature) | Prop 9.7.5 |
| Contraction on phase-cone subspace | Conditional | Prop 9.7.8 |
| Phase-cone contraction problem | Open | Problem 9.7.10 |
| Single-selector fixed points are epistemic equilibria | Proven | Prop 9.9.2 |

### Chapter 10 — The Complex Policy Gradient Theorem

| Result | Status | Location |
|---|---|---|
| Bounded return | Proven | Prop 10.2.2 |
| Log-derivative identity | Proven | Lem 10.3.2 |
| Score function identity | Proven | Lem 10.3.3 |
| Complex policy gradient theorem | Proven | Thm 10.4.1 |
| Component form of gradient | Proven | Cor 10.4.3 |
| Gradient of squared modulus | Proven | Thm 10.5.1 |
| Explicit gradient form | Proven | Cor 10.5.2 |
| Complex baseline | Proven | Prop 10.6.1 |
| Advantage form | Proven | Cor 10.6.2 |
| Gradient with advantage | Proven | Cor 10.6.3 |
| Two-channel decomposition | Proven | Prop 10.7.1 |
| Bounded exploration signal | Proven | Prop 10.8.3 |
| Exploration signal decays at equilibrium | Conditional (Axiom 13.1.1) | Prop 10.8.4 |
| Fisher matrix properties | Proven | Prop 10.9.2 |
| Reparameterization invariance | Proven | Prop 10.9.5 |
| CNAC algorithm well-defined | Proven | Prop 10.10.2 |

### Chapter 11 — Fixed Points and Their Existence

| Result | Status | Location |
|---|---|---|
| Existence under contraction | Conditional (OP1) | Thm 11.2.1 |
| Evaluation fixed point | Proven | Cor 11.2.2 |
| Optimality fixed point | Conditional (OP1) | Cor 11.2.3 |
| Continuity of $T$ away from ties | Proven | Prop 11.3.3 |
| Schauder existence for finite cMDPs | Proven | Thm 11.3.4 |
| Uniqueness in the real case | Proven | Prop 11.4.1 |
| Uniqueness under phase-cone restriction | Conditional | Prop 11.4.2 |
| Uniqueness in general | Open | Problem 11.4.3 |
| Uniqueness conjecture | Conjectural | Conj 11.4.5 |
| Closedness of fixed-point set | Proven | Prop 11.5.2 |
| Structure of fixed-point set | Open | Problem 11.5.5 |
| Lyapunov candidate properties | Proven | Props 11.6.1–11.6.4 |

### Chapter 12 — Lyapunov Structure

| Result | Status | Location |
|---|---|---|
| Jensen bound on $\mathcal{L}$ | Proven | Prop 12.2.2 |
| Decomposition of the backup | Proven | Prop 12.2.3 |
| Lyapunov inequality | Proven | Prop 12.3.1 |
| Sufficient condition for decrease | Proven | Cor 12.3.2 |
| Lyapunov decrease under small utility | Conditional (restrictive hypotheses) | Thm 12.4.1 |
| Deterministic decrease | Conditional (phase alignment) | Prop 12.5.2 |
| Modulus decrease along value iteration | Conditional (OP1) | Prop 12.6.2 |
| Modulus of iterates converges | Conditional (OP1) | Prop 12.6.3 |
| Convergence without contraction | Open | Problem 12.6.5 |
| Phase equation | Proven | Prop 12.7.2 |
| Phase convergence | Conjectural | Conj 12.7.4 |
| Decomposition of $\mathcal{L}$ | Proven | Prop 12.8.1 |
| Vanishing epistemic component | Conditional (Axiom 13.1.1) | Prop 12.8.2 |
| Exploration signal bounded by $\mathcal{L}_I$ | Proven | Prop 12.8.3 |
| Automatic exploration-exploitation transition | Conditional (Axiom 13.1.1) | Cor 12.8.4 |

### Chapter 13 — The HST Equilibrium Axiom

| Result | Status | Location |
|---|---|---|
| Axiom | Axiom | Ax 13.1.1 |
| Vanishing epistemic component | Conditional (Axiom 13.1.1) | Prop 13.3.1 |
| Vanishing exploration signal | Conditional (Axiom 13.1.1) | Prop 13.3.2 |
| Real-valued limit | Conditional (Axiom 13.1.1) | Prop 13.3.3 |
| Recovery of classical value | Conditional (Axiom 13.1.1) | Prop 13.3.4 |
| Automatic transition | Conditional (Axiom 13.1.1) | Prop 13.4.1 |
| Partial derivations | Conditional | §13.5 |
| Failure modes | Discussion | §13.6 |
| Three readings of the axiom | Discussion | §13.7 |

## 14.3 Summary of the framework's status

**Proven without conditions:**

- The complex quasi-metric and its modulus (Chapter 2).
- The properties of potential-difference debt (Chapter 2).
- The triangle inequality for $d_\gamma$ for all $\gamma \in [0, 1]$ (Chapter 2).
- The telescoping identity for the imaginary Q-value (Chapter 3).
- The non-negativity of the imaginary Q-value under the submartingale condition (Chapter 3).
- The evaluation contraction and the existence and uniqueness of $Q^\pi$ (Chapter 7).
- The topological chain and equilibrium hierarchy (Chapter 5).
- The complex policy gradient theorem (Chapter 10).
- Existence of a fixed point for finite cMDPs (Chapter 11).
- The scalar modulus contraction (Chapter 8).
- The gap structure and gap identity (Chapter 9).
- The two-state cMDP example (Chapter 7, Example 7.5.4).

**Conditional on stated assumptions:**

- The mutual-information interpretation (Chapter 3, Assumption 3.3.1).
- The phase constraint on the fixed point (Chapter 6, submartingale).
- The contraction of the Bellman operator under the phase-cone restriction (Chapter 8, Proposition 8.6.2, with value bound).
- The Lyapunov decrease under small utility and bounded value (Chapter 12, Theorem 12.4.1).
- The automatic exploration-exploitation transition (Chapter 13, Axiom 13.1.1).
- The topological equivalence for $\gamma > 0$ (Chapter 4, Corollary 4.2.2).
- The contraction threshold $\gamma < 1/\sqrt{2}$ (Chapter 4, Proposition 4.5.2; sufficient, not sharp).
- The gap-stable selector contraction (Chapter 9, Proposition 9.7.2).
- The soft Bellman operator contraction (Chapter 9, Proposition 9.7.5).

**Conjectural:**

- Contraction of the Bellman optimality operator (Chapter 8, Conjecture 8.4.5).
- Local contraction near equilibrium (Chapter 8, Conjecture 8.6.5).
- Gap-vanishing (Chapter 9, Conjecture 9.6.7).
- Uniqueness of the fixed point in general (Chapter 11, Conjecture 11.4.5).
- Phase convergence under the submartingale condition (Chapter 12, Conjecture 12.7.4).

**Open:**

- Counterexample to contraction (Chapter 8, Problem 8.4.3).
- Contraction of the two-selector operator (Chapter 9, Theorem 9.5.1).
- Phase-cone contraction (Chapter 9, Problem 9.7.10).
- Uniqueness of the fixed point in general (Chapter 11, Problem 11.4.3).
- Structure of the fixed-point set (Chapter 11, Problem 11.5.5).
- Convergence without contraction (Chapter 12, Problem 12.6.5).

**Axioms:**

- The HST Equilibrium Axiom (Chapter 13, Axiom 13.1.1).

## 14.4 The framework's open problems, ordered

**OP1. Contraction of the Bellman optimality operator.** (Chapter 8, Problem 8.4.3.) This is the framework's central open problem. A positive resolution would restore the Banach fixed-point machinery and give existence, uniqueness, and convergence. A negative resolution would force a reformulation of the optimality theory.

**OP2. Contraction of the two-selector operator.** (Chapter 9, Theorem 9.5.1.) The two-selector formulation was proposed as a resolution of OP1, but the naive contraction proof fails. Whether a modified formulation resolves the problem is open.

**OP3. Gap-vanishing conjecture.** (Chapter 9, Conjecture 9.6.7.) Does the disequilibrium gap vanish at every fixed point of the two-selector operator? Supported by examples, unproven.

**OP4. Uniqueness of the fixed point.** (Chapter 11, Problem 11.4.3.) Existence is established for finite cMDPs; uniqueness is not.

**OP5. Structure of the fixed-point set.** (Chapter 11, Problem 11.5.5.) When the fixed point is not unique, what is the structure of the fixed-point set?

**OP6. Convergence without contraction.** (Chapter 12, Problem 12.6.5.) If the Bellman operator is not a contraction, does value iteration still converge?

**OP7. Phase convergence under submartingale.** (Chapter 12, Conjecture 12.7.4.) Does the phase of the optimal value function converge to zero under the submartingale condition?

**OP8. Phase-cone contraction.** (Chapter 9, Problem 9.7.10.) Under what conditions does the fixed point lie in a phase cone of half-width less than $\pi/4$?

**OP9. Convergence of CNAC.** (Chapter 10, not addressed.) Does the CNAC algorithm converge to a local minimum of $|\eta|^2$?

**OP10. Sample complexity.** (Chapter 10, not addressed.) What is the sample complexity of value iteration, policy gradient, or CNAC?

**OP11. Applications.** (Not addressed in this book.) What are the concrete applications of the framework?

## 14.5 Final remarks

The framework presented in this book is an investigation. It is not a finished theory.

**Its central positive result** — the evaluation contraction — is proven and complete. The evaluation problem in the complex framework is tractable, and the complex structure does not complicate it.

**Its central interpretive result** — the telescoping identity and the mutual-information interpretation — is proven under a semantic assumption. The algebra is complete; the interpretation is conditional.

**Its central open problem** — the contraction of the Bellman optimality operator — is unresolved. Neither a proof nor a counterexample is known. The obstruction is structural: the modulus discards phase, and phase differences can be arbitrary.

**Its practical contribution** — the CNAC algorithm and the complex policy gradient theorem — is proven and does not depend on OP1. The policy-based approach bypasses the optimality obstruction.

**Its equilibrium theory** — the HST Equilibrium Axiom and its consequences — is interpretive. The axiom is not a theorem; its consequences are conditional on the axiom.

**Its most recent structural insight** — the disequilibrium gap and the two-selector formulation — is a genuine contribution to the framework's structure. The gap-vanishing conjecture is supported by examples, and the gap identity (Corollary 9.6.5) reduces the conjecture to a question about cross-terms.

What the framework offers is a coherent geometric language for describing systems that pay two kinds of cost: an energetic cost and an epistemic cost. The language is new. The results are partial. The open problems are genuine.

The framework's honesty about its own status is not a weakness. It is the correct posture for a theory at this stage. A theory that claims more than it has shown is a theory that will not survive contact with its critics. A theory that is clear about what it has and has not done is a theory that can be built upon.

The book is written in this posture. If the framework is useful, it will be extended by others. If it is not, the record of what was attempted will be clear.

— M.E., Casablanca

## Exercises

**Exercise 14.1.** Categorize each of the following statements as proven, conditional, conjectural, or open: (a) the evaluation operator is a contraction; (b) the Bellman optimality operator is a contraction; (c) the gap vanishes at every two-selector fixed point; (d) the real part of the Q-value is non-negative.

**Exercise 14.2.** For each conditional result in the inventory, state the condition under which it holds. For each conjectural result, state the motivation.

**Exercise 14.3.** Consider the phase-cone contraction (Proposition 8.6.2). The result is conditional on $M \le \|Q_1 - Q_2\|_\infty$. Is this condition reasonable? Under what circumstances does it hold?

**Exercise 14.4.** For each open problem (OP1–OP11), state what would be required to resolve it. Be as specific as possible.

**Exercise 14.5.** Which open problem do you think is most important? Which is most tractable? Are the two the same?

**Exercise 14.6.** Suppose OP1 is resolved in the positive (contraction holds). Which other results would become unconditional? Suppose it is resolved in the negative (counterexample exists). Which results would be invalidated?

**Exercise 14.7.** Suppose the gap-vanishing conjecture (OP3) is true. What would this imply about the two-selector formulation and the HST Equilibrium Axiom?

**Exercise 14.8.** Suppose the gap-vanishing conjecture is false. What would this imply about the framework's interpretation as a theory of equilibrium?

**Exercise 14.9 (Discussion).** The framework has one axiom (the HST Equilibrium Axiom). Is one axiom too many? Too few? Discuss.

**Exercise 14.10 (Discussion).** The framework has multiple conditional results. Is this a sign of weakness or of richness? Discuss.

**Exercise 14.11 (Discussion).** The book classifies each result as proven, conditional, conjectural, or open. Is this classification useful? Would a different classification (e.g., by importance, by chapter) be better?

**Exercise 14.12 (Discussion).** The framework's practical contribution (CNAC) does not depend on OP1. Is this a virtue (the framework is useful even with open problems) or a limitation (the theory is incomplete)?

**Exercise 14.13 (Open).** Design a new open problem (OP12 or beyond) that is not listed. What is the problem, and why is it important?

**Exercise 14.14 (Open).** The framework has been developed over Chapters 1–13. If you had to write a one-paragraph summary of the framework for a research paper, what would it say? What are the two or three most important results?

**Exercise 14.15 (Open).** Consider the framework's relationship to classical RL. Is the complex framework a strict generalization, a reparameterization, or a genuinely different approach? Justify your answer.
