# Chapter 13 — The HST Equilibrium Axiom



## 13.1 Statement of the axiom

**Axiom 13.1.1 (HST Equilibrium Axiom).** Every information processing system evolves toward epistemic equilibrium. Formally, under the dynamics induced by the Bellman optimality operator $T$ (or the two-selector operator $T_{\rightarrow\leftarrow}$), the imaginary component of the value function converges to zero:

$$\lim_{t \to \infty} Q_I^\*(B_t, A_t) = 0 \quad \text{almost surely},$$

and the phase of the value function converges to zero:

$$\lim_{t \to \infty} \mathrm{Arg} Q^\*(B_t, A_t) = 0 \quad \text{almost surely}.$$

**Remark 13.1.2 (The two statements are equivalent).** Under the submartingale condition, $Q_I^\* \ge 0$ and $Q_R^\* \ge 0$ (Propositions 8.5.1 and 8.5.2), so $\mathrm{Arg} Q^\* \in [0, \pi/2]$. The statement that $Q_I^\* \to 0$ is then equivalent to the statement that $\mathrm{Arg} Q^\* \to 0$ (given that $Q^\*$ does not converge to zero in both components simultaneously, which would make the argument undefined). The axiom is stated in both forms for emphasis.

**Remark 13.1.3 (The axiom is not a theorem).** The axiom is not derivable from the framework's other assumptions. It is a foundational claim about what information processing systems do. The framework's technical results — the evaluation contraction, the policy gradient theorem, the telescoping identity, the topological structure — do not depend on the axiom. The axiom is required only for the *interpretive* claims about learning and equilibrium.

## 13.2 Why an axiom, and not a theorem

The axiom is not derivable from the framework's other assumptions, for three reasons.

**First, the axiom is a statement about convergence to a specific state.** The framework provides the machinery for convergence — contractions, Lyapunov functions, fixed points — but it does not specify *which* fixed point the system converges to. In general there may be multiple fixed points, and the system may converge to any of them. The axiom selects one: the fixed point with vanishing imaginary component.

**Second, the axiom is a statement about all systems.** It is not a conditional statement of the form "if the system satisfies such-and-such, then it converges." It is an unconditional claim about the class of all information processing systems. Such a claim cannot be derived from the framework's assumptions about any particular system.

**Third, the axiom is a statement about the *end* of a process.** The framework describes the dynamics; the axiom describes the asymptotic behavior. In general, the asymptotic behavior of a dynamical system cannot be deduced from its local dynamics without additional assumptions (compactness, monotonicity, etc.).

**Remark 13.2.1 (The axiom is not a gap in the framework's logic).** It is an explicit assumption that the framework makes, and it should be stated as such. The framework's honesty about the axiom is part of its content. A framework that claims to *derive* the convergence of information processing systems to equilibrium would be overclaiming; a framework that says "here is the structure, and here is an assumption about how systems behave within it" is honest and defensible.

## 13.3 Consequences of the axiom

Under the axiom, several results follow.

**Proposition 13.3.1 (Vanishing epistemic component).** Under Axiom 13.1.1, the epistemic component $\mathcal{L}_I(b, a) = Q_I^\*(b, a)^2$ of the Lyapunov candidate vanishes:

$$\mathcal{L}_I(b, a) \to 0 \quad \text{as } t \to \infty.$$

*Proof.* $Q_I^\* \to 0$ implies $Q_I^{\*2} \to 0$. $\square$

**Proposition 13.3.2 (Vanishing exploration signal).** Under Axiom 13.1.1, the exploration signal $\mathcal{E}(b)$ defined in Chapter 10 vanishes.

*Proof.* By Proposition 12.8.3, $\mathcal{E}(b) \le 4 \sup_a \mathcal{L}_I(b, a)$. Since $\mathcal{L}_I \to 0$, $\mathcal{E} \to 0$. $\square$

**Proposition 13.3.3 (Real-valued limit).** Under Axiom 13.1.1, the limiting value function $Q_\infty^\*(b, a) = \lim_{t \to \infty} Q_t^\*(b, a)$ is real and non-negative:

$$Q_\infty^\*(b, a) \in \mathbb{R}_{\ge 0}.$$

*Proof.* $Q_I^\* \to 0$ and $Q_R^\* \ge 0$, so $Q^\* \to |Q^\*| \ge 0$. $\square$

**Proposition 13.3.4 (Recovery of classical value).** In the limit, the complex framework reduces to the classical framework applied to the real cost $c$. The limiting optimal policy is the classical cost-minimizing policy.

*Proof.* By Proposition 13.3.3, the limit is a non-negative real value function. The Bellman equation in the limit reduces to

$$Q_\infty^\*(b, a) = \mathbb{E}_{b'}[c(b, a, b') + \lambda Q_\infty^\*(b', \pi_{Q_\infty^\*}(b'))],$$

which is the classical Bellman optimality equation for cost minimization. $\square$

**Remark 13.3.5 (The complex structure is transient).** Under the axiom, the complex framework reduces, asymptotically, to the classical framework applied to the real cost. The imaginary component is transient; it vanishes at equilibrium; the asymptotic behavior is purely real. This is a strong consequence: the framework's distinctive geometric structure is a *transient* phenomenon, relevant during learning but not at the fixed point.

## 13.4 The axiom and the exploration-exploitation transition

The axiom gives a formal account of the exploration-exploitation transition.

**Proposition 13.4.1 (Automatic transition).** Under Axiom 13.1.1, the CNAC algorithm (Chapter 10) transitions from a two-channel update (cost and debt) to a single-channel update (cost only), without an external schedule.

*Proof.* The debt channel is weighted by $\mathrm{Im}(\overline{\eta})$. By Proposition 13.3.3, $\mathrm{Im}(Q^*) \to 0$, hence $\mathrm{Im}(\overline{\eta}) \to 0$, and the debt channel vanishes. The cost channel remains active, driven by $\mathrm{Re}(\overline{\eta})$. $\square$

**Remark 13.4.2 (Comparison to classical exploration).** Classical methods — $\epsilon$-greedy, entropy regularization, count-based bonuses — require an explicit annealing schedule. The exploration parameter must be decreased over time, and the schedule is a design choice. The complex framework has no such parameter; the transition is a consequence of the axiom and the system's dynamics.

**Remark 13.4.3 (The framework's strongest interpretive claim).** This is the framework's strongest interpretive claim: that the exploration-exploitation trade-off, which in classical RL is handled by an external schedule, is here handled automatically by the system's own dynamics. The claim depends on the axiom; without it, there is no guarantee that the imaginary component vanishes, and the exploration signal may persist indefinitely.

## 13.5 Partial derivations of the axiom

While the axiom is not derivable in general, it can be derived under additional assumptions. Four such derivations are available.

**Derivation 1: From the submartingale condition and boundedness.** If the potential $\phi$ is a submartingale and is bounded above, then $\phi(B_t)$ converges almost surely. Under the information-theoretic reading, this says that the system's uncertainty about $\Theta$ converges. If the limit is zero — i.e. if the system becomes certain of $\Theta$ — then $Q_I^* \to 0$, and the axiom holds.

*Proof sketch.* The submartingale $\phi(B_t) = -H(\Theta \mid B_t)$ is bounded above by $0$ and non-decreasing in expectation. By the martingale convergence theorem, it converges almost surely to a limit $\phi_\infty \le 0$. If the limit is $0$ — which requires the system to become certain of $\Theta$ — then $H(\Theta \mid B_t) \to 0$, and $Q_I^* \to 0$. Whether the limit is $0$ depends on whether the system can become certain; in a finite latent space with informative observations, it can. $\square$

**Derivation 2: From contraction on a phase cone.** If $T$ is a contraction on a phase cone $C_\theta$ (Proposition 8.6.2), and if the fixed point lies in $C_\theta$, then the imaginary component of the fixed point is bounded by $\sin\theta \cdot |Q^\*|$, and if the fixed point is the limit of iterates, the imaginary component converges to a value bounded by $\sin\theta \cdot M$ for some $M$. If $\theta$ can be made arbitrarily small (by making the cone arbitrarily tight), then $Q_I^\* \to 0$.

*Proof sketch.* The contraction on $C_\theta$ gives $\mid Q_n - Q^\*\mid_\infty \le \lambda^n \mid Q_0 - Q^\*\mid_\infty$. If $Q^\* \in C_\theta$, then $|Q_I^\*| \le \tan\theta \cdot Q_R^\*$, which can be made small by making $\theta$ small. $\square$

**Derivation 3: From finite state space and irreducibility.** If the cMDP has finite state space and the Markov chain under the optimal policy is irreducible and aperiodic, then the potential $\phi$ converges to a stationary distribution. If the stationary distribution concentrates on states with $\phi = 0$ (i.e. states of zero uncertainty), then $Q_I^* \to 0$.

*Proof sketch.* Standard Markov chain convergence. The stationary distribution of the chain under the optimal policy determines the asymptotic value of the potential. If the stationary distribution concentrates on states with $\phi = 0$, then $Q_I^* \to 0$. $\square$

**Derivation 4: From vanishing utility at the fixed point.** If the fixed point is in the first quadrant (Corollary 8.5.3) and the utility $z$ vanishes at the fixed point, then the imaginary component of the fixed point is zero.

*Proof sketch.* At a fixed point with $z \equiv 0$, the Bellman equation becomes $Q^\*(b, a) = \lambda \mathbb{E}[Q^\*(b', \pi_{Q^\*}(b'))]$. Iterating gives $Q^\* \equiv 0$. This is a trivial case (zero cost, zero debt), but it illustrates the principle: if the driving terms vanish, so does the fixed point. $\square$

**Remark 13.5.1 (The partial derivations show the axiom is a limit case).** The four derivations show that the axiom holds under additional assumptions. They do not prove the axiom in general. The axiom remains an axiom; the partial derivations are useful for identifying the specific conditions under which the axiom is a theorem.

## 13.6 Failure modes of the axiom

It is worth considering what happens when the axiom fails.

**Failure mode 1: Persistent uncertainty.** If the system's uncertainty about $\Theta$ does not vanish — for instance, if the environment is non-stationary, or if the observations are uninformative — then $\phi$ does not converge to zero, and $Q_I^*$ does not vanish. The system remains in a state of ongoing epistemic tension.

**Failure mode 2: Non-convergent dynamics.** If the Bellman operator is not a contraction and the value iteration does not converge, then the limit $Q_\infty^*$ may not exist. The axiom presupposes convergence; if convergence fails, the axiom is vacuous.

**Failure mode 3: Multiple fixed points.** If the fixed-point set is not a singleton, the system may converge to a fixed point with non-zero imaginary component. The axiom selects the fixed point with zero imaginary component, but the dynamics may not select it.

**Failure mode 4: Non-stationary environments.** If the environment changes over time, the fixed point itself changes, and the notion of "convergence to equilibrium" needs to be reinterpreted. In a non-stationary environment, the system may track a moving equilibrium rather than converge to a static one.

**Remark 13.6.1 (The failure modes are not just theoretical).** They correspond to real phenomena: persistent uncertainty in non-stationary environments; failure to converge in ill-conditioned problems; convergence to suboptimal fixed points in multi-modal problems. The axiom, if it holds, says that these phenomena do not occur in the class of systems the framework is about. Whether this is true is an empirical question.

## 13.7 The axiom as a research program

The axiom can be read in three ways.

**Reading 1: The axiom is a hypothesis.** "Every information processing system converges to epistemic equilibrium." As a hypothesis, it makes a testable prediction: systems in the class should show a decay of the imaginary component of their value functions over time. If they do not, the axiom is falsified.

**Reading 2: The axiom is a definition.** "An information processing system is, by definition, a system that converges to epistemic equilibrium." Under this reading, the axiom is not testable; it defines the class of systems the framework is about. Systems that do not satisfy the axiom are, by definition, outside the class.

**Reading 3: The axiom is an orientation.** "The framework is oriented toward systems that converge to epistemic equilibrium." Under this reading, the axiom is neither a hypothesis nor a definition; it is a statement about the framework's focus. The framework is not attempting to describe all systems; it is attempting to describe a particular kind of system, and the axiom names that kind.

**Remark 13.7.1 (The three readings have different consequences).** Under Reading 1, the framework is empirical and testable. Under Reading 2, the framework is definitional and the axiom is not negotiable. Under Reading 3, the framework is partial and the axiom marks its boundary. The choice of reading is a matter of what the framework is for.

**Remark 13.7.2 (The framework does not commit to a reading).** The book presents the three readings and leaves the choice to the reader. The framework's mathematical results hold regardless of which reading is adopted; the difference is in how the axiom is used to interpret those results. Under all three readings, the axiom is an explicit assumption, not a derived theorem.

## 13.8 Summary

**The HST Equilibrium Axiom (Axiom 13.1.1)** states that every information processing system converges to epistemic equilibrium, in the sense that the imaginary component of the value function vanishes and the phase converges to zero. It is an axiom, not a theorem: it cannot be derived from the framework's other assumptions.

**Consequences of the axiom:**

- The epistemic component of the Lyapunov candidate vanishes.
- The exploration signal decays.
- The asymptotic value function is real and non-negative.
- The complex framework reduces, asymptotically, to the classical framework applied to the real cost.
- The exploration-exploitation transition is automatic, without an external schedule.

**Partial derivations** of the axiom are available under additional assumptions: submartingale potential with vanishing uncertainty; contraction on a phase cone with a fixed point in the cone; finite state space with irreducible dynamics and concentrated stationary distribution; vanishing utility at the fixed point.

**Failure modes** of the axiom include persistent uncertainty, non-convergent dynamics, multiple fixed points, and non-stationary environments. These correspond to real phenomena.

**The axiom can be read as a hypothesis, a definition, or an orientation.** The choice of reading determines the framework's scope and its relationship to empirical work.

This completes Part IV. The equilibrium theory of the framework has been developed: fixed points and their existence (Chapter 11), the Lyapunov structure and its conditions (Chapter 12), and the HST Equilibrium Axiom and its consequences (this chapter).

## Exercises

**Exercise 13.1.** Verify that the two forms of the axiom (imaginary component vanishes, phase converges to zero) are equivalent under the submartingale condition.

**Exercise 13.2.** For a cMDP with a submartingale potential, verify that $Q_I^* \ge 0$ at the fixed point.

**Exercise 13.3.** Verify Proposition 13.3.3 (real-valued limit) for a specific cMDP with a submartingale potential. Show that $Q_\infty^* = |Q_\infty^*|$.

**Exercise 13.4.** For a cMDP with a submartingale potential, verify that the limiting optimal policy is the classical cost-minimizing policy.

**Exercise 13.5.** Verify Proposition 13.4.1 (automatic transition) for the CNAC algorithm on a specific cMDP. Show that the debt channel vanishes as training proceeds.

**Exercise 13.6.** Derive the axiom from the submartingale condition and boundedness. State the conditions under which the derivation holds.

**Exercise 13.7.** Give an example of a system that does *not* satisfy the HST Equilibrium Axiom. Explain which failure mode applies.

**Exercise 13.8.** For a non-stationary environment (Failure Mode 4), describe what "convergence to equilibrium" would mean and whether the axiom can be generalized.

**Exercise 13.9.** Under Reading 1 of the axiom (hypothesis), what experiments would test the axiom? Design a testable experiment.

**Exercise 13.10 (Discussion).** The axiom is the framework's strongest interpretive claim. Is this a strength or a weakness? Discuss.

**Exercise 13.11 (Discussion).** Under Reading 2 (definition), the axiom defines the class of systems the framework is about. What other systems might exist outside this class? Are they interesting?

**Exercise 13.12 (Discussion).** The framework does not commit to a reading of the axiom. Is this a virtue or a problem? Discuss.

**Exercise 13.13 (Open).** The partial derivations of the axiom (13.5) all require additional assumptions. Can the axiom be derived under weaker conditions? For instance, is the submartingale condition plus bounded potential sufficient, without the requirement that the limit of the potential is zero?

**Exercise 13.14 (Open).** The HST Equilibrium Axiom states that all information processing systems converge to equilibrium. But real systems often do not — they oscillate, they fail, they persist in non-equilibrium states. How does the framework account for these observations? Is the axiom simply wrong, or does it describe an idealized limit?

**Exercise 13.15 (Open).** The axiom's consequences include the recovery of the classical value function in the limit. Does this mean the complex framework is "just" a transient correction to classical RL? Or does the transient have properties that the classical framework cannot capture?

**Exercise 13.16 (Open).** The failure modes of the axiom (13.6) correspond to real phenomena. Can the framework be extended to handle these cases? What would a "non-equilibrium" version of the framework look like?

**Exercise 13.17 (Open).** The axiom can be stated in terms of the imaginary component of the value function, the phase of the value function, or the epistemic component of the Lyapunov function. Are these three formulations equivalent in general? Under what conditions?
