# Chapter 12 — Lyapunov Structure



## 12.1 The Lyapunov candidate

Let $Q^\* \in \mathcal{Q}$ be a fixed point of the Bellman optimality operator $T$, if one exists (Chapter 11). Define

$$\mathcal{L}(b, a) = |Q^\*(b, a)|^2 = Q_R^\*(b, a)^2 + Q_I^\*(b, a)^2.$$

This is the *candidate Lyapunov function*. It is non-negative, bounded, and decomposes into a cost component $\mathcal{L}_R = Q_R^{\*2}$ and an epistemic component $\mathcal{L}_I = Q_I^{\*2}$.

**Definition 12.1.1 (Lyapunov function).** A function $\mathcal{L} : \mathcal{B} \times \mathcal{A} \to \mathbb{R}_{\ge 0}$ is a *Lyapunov function* for the system if, along the system's trajectories,

$$\mathcal{L}(B_{t+1}, A_{t+1}) \le \mathcal{L}(B_t, A_t)$$

with equality only at the fixed point. It is a *strict Lyapunov function* if the inequality is strict whenever $(B_t, A_t)$ is not the fixed point.

**Problem 12.1.2.** Is $\mathcal{L}$ a Lyapunov function? A strict Lyapunov function?

## 12.2 The Bellman equation for the modulus

The Bellman equation for $Q^\*$ is

$$Q^\*(b, a) = \mathbb{E}_{b'}\left[z(b, a, b') + \lambda \, Q^\*(b', \pi_{Q^\*}(b'))\right].$$

Taking the squared modulus of both sides and expanding:

$$|Q^\*(b, a)|^2 = \left|\mathbb{E}_{b'}[z(b, a, b') + \lambda Q^\*(b', \pi_{Q^\*}(b'))]\right|^2.$$

By the modulus-of-expectation inequality (Proposition 2.3.2), $|\mathbb{E}[W]|^2 \le \mathbb{E}[|W|^2]$ for any $\mathbb{C}$-valued random variable $W$. Applying this with $W = z(b, a, b') + \lambda Q^\*(b', \pi_{Q^\*}(b'))$:

$$|Q^\*(b, a)|^2 \le \mathbb{E}_{b'}\left[\left|z(b, a, b') + \lambda Q^\*(b', \pi_{Q^\*}(b'))\right|^2\right].$$

The right-hand side is the *expected backup*.

**Definition 12.2.1 (Expected backup).** Define

$$\mathcal{B}(b, a) = \mathbb{E}_{b'}\left[\left|z(b, a, b') + \lambda Q^\*(b', \pi_{Q^\*}(b'))\right|^2\right].$$

**Proposition 12.2.2 (Jensen bound).** $\mathcal{L}(b, a) \le \mathcal{B}(b, a)$ for all $(b, a)$.

*Proof.* Modulus of expectation applied to $W = z + \lambda Q^\*$. $\square$

**Proposition 12.2.3 (Decomposition of the expected backup).**

$$\mathcal{B}(b, a) = \mathbb{E}_{b'}[|z|^2] + 2\lambda \, \mathbb{E}_{b'}\left[\mathrm{Re}\left(z \, \overline{Q^\*(b', \pi_{Q^\*}(b'))}\right)\right] + \lambda^2 \, \mathbb{E}_{b'}\left[|Q^\*(b', \pi_{Q^\*}(b'))|^2\right].$$

*Proof.* Expand $|z + \lambda Q|^2 = |z|^2 + 2\lambda \mathrm{Re}(z \overline{Q}) + \lambda^2 |Q|^2$ and take expectations. $\square$

**Remark 12.2.4 (Equality condition).** Jensen's inequality is an equality if and only if $W$ has constant argument almost surely. In that case, the expected backup equals the Lyapunov candidate. Otherwise, the expected backup is strictly larger.

## 12.3 The Lyapunov inequality

The Bellman fixed-point equation gives

$$\mathcal{L}(b, a) \le \mathcal{B}(b, a).$$

We want to compare $\mathcal{B}(b, a)$ to the expected value of $\mathcal{L}$ at the next step:

$$\mathbb{E}_{b'}[\mathcal{L}(b', \pi_{Q^\*}(b'))] = \mathbb{E}_{b'}[|Q^\*(b', \pi_{Q^\*}(b'))|^2].$$

**Proposition 12.3.1 (Lyapunov inequality).**

$$\mathcal{B}(b, a) - \mathbb{E}_{b'}[\mathcal{L}(b', \pi_{Q^\*}(b'))] = \mathbb{E}_{b'}\left[|z|^2\right] + 2\lambda \, \mathbb{E}_{b'}\left[\mathrm{Re}\left(z \, \overline{Q^\*}\right)\right] + (\lambda^2 - 1) \, \mathbb{E}_{b'}[\mathcal{L}(b', \pi_{Q^\*}(b'))].$$

*Proof.* Substitute the decomposition of $\mathcal{B}$ (Proposition 12.2.3) and rearrange. $\square$

**Corollary 12.3.2 (Sufficient condition for decrease).** $\mathcal{B}(b, a) \le \mathbb{E}_{b'}[\mathcal{L}(b', \pi_{Q^\*}(b'))]$ if and only if the right-hand side of Proposition 12.3.1 is non-positive.

**Remark 12.3.3 (The condition is not automatic).** The right-hand side of Proposition 12.3.1 involves three terms with opposite signs: $\mathbb{E}[|z|^2] \ge 0$, $2\lambda \mathbb{E}[\mathrm{Re}(z \overline{Q^\*})]$ of either sign, and $(\lambda^2 - 1) \mathbb{E}[\mathcal{L}] \le 0$. The decrease condition requires the negative terms to dominate the positive ones. This is not automatic; it depends on the relative magnitudes of $z$ and $Q^*$.

## 12.4 Sufficient conditions for Lyapunov decrease

**Theorem 12.4.1 (Lyapunov decrease under small utility and bounded value).** Suppose there exist constants $\epsilon > 0$ and $M > 0$ such that:

- (i) $|z(b, a, b')| \le \epsilon$ for all $(b, a, b')$.
- (ii) $|Q^\*(b, a)| \le M$ for all $(b, a)$.
- (iii) There exists $\theta \in [0, \pi]$ such that the angle between $z(b, a, b')$ and $Q^\*(b', \pi_{Q^\*}(b'))$ is at most $\theta$ for all $(b, a, b')$ in the support of the transition kernel.

If

$$\epsilon^2 + 2\lambda \epsilon M \cos\theta + (\lambda^2 - 1) m^2 \le 0,$$

where $m = \inf_{b, a} |Q^\*(b, a)|$ over the reachable region, then

$$\mathcal{B}(b, a) \le \mathbb{E}_{b'}[\mathcal{L}(b', \pi_{Q^\*}(b'))]$$

and $\mathcal{L}$ is a Lyapunov function.

*Proof.* Bound each term in Proposition 12.3.1:

$$\mathbb{E}[|z|^2] \le \epsilon^2,$$

$$2\lambda \mathbb{E}[\mathrm{Re}(z \overline{Q^*})] \le 2\lambda \epsilon M \cos\theta,$$

$$(\lambda^2 - 1) \mathbb{E}[\mathcal{L}] \le (\lambda^2 - 1) m^2.$$

Combining and using the stated condition gives the result. $\square$

**Remark 12.4.2 (The conditions are restrictive).** Theorem 12.4.1 requires the utility to be small, the fixed point to be bounded away from zero in the reachable region, and the angle between $z$ and $Q^\*$ to be acute. These conditions may hold near the fixed point but not in the transient. The theorem gives a *local* Lyapunov decrease, not a global one.

**Remark 12.4.3 (The case $\theta = 0$).** If $z$ and $Q^\*$ point in the same direction (i.e. $\theta = 0$), the cross-term is positive and the condition becomes $\epsilon^2 + 2\lambda \epsilon M + (\lambda^2 - 1) m^2 \le 0$. This requires $m$ to be large enough relative to $\epsilon$ and $M$, which is a substantial restriction.

**Remark 12.4.4 (The case $\theta = \pi$).** If $z$ and $Q^\*$ point in opposite directions (i.e. $\theta = \pi$), the cross-term is negative, and the condition becomes $\epsilon^2 - 2\lambda \epsilon M + (\lambda^2 - 1) m^2 \le 0$. This is easier to satisfy. The decrease condition is therefore *easier* when the utility and the value point in opposite directions, which is counter-intuitive but consistent with the framework's structure: when the cost and the value have opposite phases, the modulus decreases along the Bellman update.

## 12.5 Lyapunov decrease in the deterministic case

When transitions are deterministic, the analysis simplifies.

**Proposition 12.5.1 (Deterministic transitions).** Suppose $p(b' \mid b, a) = \delta(b' - f(b, a))$ for a deterministic function $f$. Then

$$\mathcal{L}(b, a) = \left|z(b, a, f(b, a)) + \lambda Q^\*(f(b, a), \pi_{Q^\*}(f(b, a)))\right|^2.$$

*Proof.* The expectation over a Dirac measure is evaluation at $f(b, a)$. $\square$

**Proposition 12.5.2 (Decrease under phase alignment).** In the deterministic case, if the argument of $z(b, a, f(b, a))$ is within $\theta$ of the argument of $Q^\*(f(b, a), \pi_{Q^\*}(f(b, a)))$, then

$$\mathcal{L}(b, a) \le |z|^2 + 2\lambda |z| |Q^\*| \cos\theta + \lambda^2 \mathcal{L}(f(b, a), \pi_{Q^\*}(f(b, a))),$$

where $z = z(b, a, f(b, a))$ and $Q^\* = Q^\*(f(b, a), \pi_{Q^\*}(f(b, a)))$.

*Proof.* Expand the square and bound the cross-term using $\cos\theta$. $\square$

**Corollary 12.5.3 (Small utility case).** If $|z| \le \epsilon$ and $\cos\theta \ge 0$, then
$$\mathcal{L}(b, a) \le \epsilon^2 + 2\lambda \epsilon M + \lambda^2 \mathcal{L}(f(b, a), \pi_{Q^*}(f(b, a))).$$

**Remark 12.5.4 (Interpretation).** In the deterministic case, the Lyapunov function at $(b, a)$ is bounded by a discounted version at the successor, plus a term that measures the utility of the transition. The decrease is not automatic; it depends on the ratio between the utility and the value at the successor.

## 12.6 Connection to value iteration

**Definition 12.6.1 (Value iteration).** The *value iteration* sequence is $Q_{n+1} = T Q_n$ for an initial $Q_0 \in \mathcal{Q}$.

**Proposition 12.6.2 (Modulus decrease along value iteration).** If $T$ is a $\lambda$-contraction on $\mathcal{Q}$ (Conjecture 8.4.5), then $\|Q_n - Q^*\|_\infty \to 0$ at rate $\lambda^n$.

*Proof.* Banach fixed-point theorem. $\square$

**Proposition 12.6.3 (Modulus of iterates).** Under contraction, $|Q_n(b, a)| \to |Q^*(b, a)|$ for every $(b, a)$.

*Proof.* $|\,|Q_n(b, a)| - |Q^*(b, a)|\,| \le |Q_n(b, a) - Q^*(b, a)| \le \|Q_n - Q^*\|_\infty \to 0$. $\square$

**Remark 12.6.4 (Modulus convergence is weaker than value convergence).** The convergence of the modulus does not imply convergence of the complex value. Two sequences with the same modulus but different arguments are indistinguishable at the level of $|Q_n|$. This is the same phase loss that appears in the optimality obstruction of Chapter 8.

**Problem 12.6.5 (Convergence without contraction).** If $T$ is not a contraction, does value iteration still converge? This is open. Even in the classical real case, there are operators that are not contractions but still have unique fixed points and convergent iterations (e.g. non-expansive operators on compact spaces). Whether the complex Bellman operator falls in this class is unknown.

## 12.7 The phase dynamics

The Lyapunov analysis in terms of the modulus loses phase information. A finer analysis tracks the phase of $Q_n$.

**Definition 12.7.1 (Phase).** The *phase* of $Q_n(b, a)$ is $\theta_n(b, a) = \operatorname{Arg}(Q_n(b, a)) \in (-\pi, \pi]$.

**Proposition 12.7.2 (Phase equation).** If $T$ were a contraction on the phase, the phase would satisfy a Bellman-like equation. In general, the phase evolves discontinuously when the modulus-greedy selector switches.

*Proof.* The phase of $TQ$ depends on the phases of the $Q(b', \pi_Q(b'))$ terms, which in turn depend on the selector $\pi_Q$. When $\pi_Q$ switches discontinuously, the phase of $TQ$ jumps. $\square$

**Remark 12.7.3 (Phase dynamics are the source of the optimality obstruction).** The modulus decreases smoothly, but the phase can jump, and the jumps are what defeat the naive contraction proof (Chapter 8).

**Conjecture 12.7.4 (Phase convergence under submartingale).** Under the submartingale condition on the potential, the phase of the optimal value function converges to zero:
$$\operatorname{Arg} Q^*(b, a) \to 0 \quad \text{as the system approaches equilibrium.}$$

**Remark 12.7.5 (Motivation for the conjecture).** The conjecture is motivated by Corollary 8.5.3 (the fixed point is in the first quadrant) and by the heuristic that at equilibrium, the imaginary component vanishes. If the phase converges to zero, then the phase cone of Chapter 8 shrinks, and the local contraction conjecture (Conjecture 8.6.5) becomes plausible.

## 12.8 The Lyapunov function and the exploration-exploitation transition

**Proposition 12.8.1 (Decomposition of the Lyapunov function).** $\mathcal{L}(b, a) = \mathcal{L}_R(b, a) + \mathcal{L}_I(b, a)$ where
$$\mathcal{L}_R(b, a) = Q_R^*(b, a)^2, \qquad \mathcal{L}_I(b, a) = Q_I^*(b, a)^2.$$

*Proof.* $|Q^*|^2 = Q_R^{*2} + Q_I^{*2}$. $\square$

**Proposition 12.8.2 (Imaginary component vanishes at equilibrium).** Under the HST Equilibrium Axiom (Chapter 13), $\mathcal{L}_I(b, a) \to 0$ for all $(b, a)$.

*Proof.* The axiom states $Q_I^*(b, a) \to 0$. $\square$

**Proposition 12.8.3 (Exploration signal bounded by $\mathcal{L}_I$).** The exploration signal $\mathcal{E}(b)$ of Chapter 10 is bounded by $4 \sup_a \mathcal{L}_I(b, a)$.

*Proof.* The variance of a random variable bounded by $M$ is at most $M^2/4$. Applying this to $\operatorname{Im} A^\pi(b, A)$, which is bounded by $2 \max_a |Q_I^*(b, a)|$, gives the result. $\square$

**Corollary 12.8.4 (Automatic exploration-exploitation transition).** As the system approaches equilibrium, $\mathcal{L}_I \to 0$, hence $\mathcal{E} \to 0$. The exploration signal decays automatically, without an external schedule.

**Remark 12.8.5 (The transition is conditional on the axiom).** The transition is a consequence of the HST Equilibrium Axiom. Without the axiom, there is no guarantee that $\mathcal{L}_I$ vanishes, and the exploration signal may persist indefinitely. The axiom is the framework's assumption about what information processing systems do.

## 12.9 Summary

The Lyapunov candidate $\mathcal{L}(b, a) = |Q^*(b, a)|^2$ is non-negative, bounded, and decomposes into a cost component $\mathcal{L}_R$ and an epistemic component $\mathcal{L}_I$.

**The Lyapunov decrease is not automatic.** It depends on the ratio of the utility to the value at successors and on the phase alignment between $z$ and $Q^*$. Sufficient conditions for the decrease are given in Theorem 12.4.1 (small utility, bounded value, acute phase angle) and Corollary 12.5.3 (deterministic transitions with small utility). These conditions are restrictive and may hold only near the fixed point.

**Under the HST Equilibrium Axiom,** the epistemic component $\mathcal{L}_I$ vanishes. This gives a formal account of the exploration-exploitation transition: the exploration signal is the variance of the imaginary advantage, bounded by $\mathcal{L}_I$, which decays automatically as the system approaches equilibrium.

**The phase dynamics are the source of the optimality obstruction.** The modulus decreases smoothly, but the phase can jump. Whether the phase converges under the submartingale condition (Conjecture 12.7.4) is an open problem.

## Exercises

**Exercise 12.1.** Verify the Jensen bound (Proposition 12.2.2) for a specific cMDP. Compute $\mathcal{L}(b, a)$ and $\mathcal{B}(b, a)$ and check the inequality.

**Exercise 12.2.** Verify the decomposition of the expected backup (Proposition 12.2.3) for a specific cMDP.

**Exercise 12.3.** Verify the Lyapunov inequality (Proposition 12.3.1) for a specific cMDP with $\lambda = 0.5$ and small utility.

**Exercise 12.4.** For a cMDP with small utility ($\epsilon = 0.1$) and bounded value ($M = 1$), check the condition of Theorem 12.4.1 for $\theta = 0$, $\theta = \pi/2$, and $\theta = \pi$. In which cases does the Lyapunov decrease hold?

**Exercise 12.5.** For the deterministic case (Proposition 12.5.2), compute the Lyapunov value at a specific state and verify the bound.

**Exercise 12.6.** Construct a cMDP where the Lyapunov candidate is *not* decreasing along some trajectory. Compute the trajectory and show that $\mathcal{L}(b_{t+1}, a_{t+1}) > \mathcal{L}(b_t, a_t)$ for some $t$.

**Exercise 12.7.** For a cMDP where $T$ is a contraction, verify Proposition 12.6.2 by computing $Q_n$ for several iterations and showing that $\|Q_n - Q^*\|_\infty \to 0$.

**Exercise 12.8.** Compute the phase $\theta_n(b, a)$ along a value iteration sequence for a specific cMDP. Does the phase converge? Does it oscillate?

**Exercise 12.9.** Verify the decomposition of $\mathcal{L}$ into $\mathcal{L}_R$ and $\mathcal{L}_I$ (Proposition 12.8.1) for a specific cMDP.

**Exercise 12.10.** Verify the bound $\mathcal{E}(b) \le 4 \sup_a \mathcal{L}_I(b, a)$ for a specific policy.

**Exercise 12.11.** For a cMDP with a submartingale potential, verify that $\mathcal{L}_I$ is non-negative and bounded by $(2M/(1-\lambda))^2$.

**Exercise 12.12 (Discussion).** The Lyapunov decrease requires restrictive conditions (Theorem 12.4.1). Is this a limitation of the framework, or a fundamental property of the dynamics? Discuss.

**Exercise 12.13 (Discussion).** The phase dynamics are the source of the optimality obstruction. Would a phase-aware Lyapunov function (using the argument of $Q^*$ rather than just its modulus) help? Discuss.

**Exercise 12.14 (Open).** Prove or disprove the phase convergence conjecture (12.7.4). If the phase converges under the submartingale condition, prove it. If not, construct a counterexample.

**Exercise 12.15 (Open).** The Lyapunov analysis uses the squared modulus $|Q^*|^2$. Would a different function — e.g., the distance to the fixed point $\|Q - Q^*\|_\infty$ — be a better Lyapunov function? Compare the two.

**Exercise 12.16 (Open).** Under what conditions on the cMDP is the Lyapunov candidate $\mathcal{L} = |Q^*|^2$ a *strict* Lyapunov function? Characterize the cMDPs for which strict decrease holds.

**Exercise 12.17 (Open).** The phase dynamics are discontinuous at the tie set. Is there a smoothed version of the dynamics for which the phase converges continuously? What would that look like?
