# Chapter 8 — The Optimality Operator and Its Gap



## 8.1 The optimality problem

**Definition 8.1.1 (Modulus-greedy policy).** Given $Q \in \mathcal{Q}$, define the *modulus-greedy policy* $\pi_Q : \mathcal{B} \to \mathcal{A}$ by

$$\pi_Q(b) = \arg\min_{a \in \mathcal{A}} |Q(b, a)|,$$

with ties broken by a fixed deterministic rule (e.g. the smallest action index).

**Definition 8.1.2 (Bellman optimality operator).** The *Bellman optimality operator* $T : \mathcal{Q} \to \mathcal{Q}$ is

$$(TQ)(b, a) = \mathbb{E}_{b' \sim p(\cdot \mid b, a)}\left[z(b, a, b') + \lambda \, Q(b', \pi_Q(b'))\right].$$

**Remark 8.1.3 (Nonlinearity).** The operator $T$ differs from the evaluation operator $T^\pi$ in that the policy at the next state is not fixed; it is chosen by the modulus-greedy rule applied to $Q$. This introduces a nonlinear dependence of the operator on its argument, and the dependence involves only the *magnitudes* of $Q(b, \cdot)$, not the arguments. This is the source of the optimality gap.

**Problem 8.1.4 (OP1).** Is $T$ a $\lambda$-contraction on $(\mathcal{Q}, \|\cdot\|_\infty)$? Equivalently, does there exist $\kappa < 1$ such that

$$\|TQ_1 - TQ_2\|_\infty \le \kappa \, \|Q_1 - Q_2\|_\infty$$

for all $Q_1, Q_2 \in \mathcal{Q}$?

**Remark 8.1.5 (Status of OP1).** The problem is open. No proof and no counterexample are known. This chapter presents the obstruction, the partial results that are available, and the structural facts about the fixed point that may lead to a resolution.

## 8.2 Why the naive proof fails

The classical proof of the optimality contraction uses the inequality

$$\left| \max_a f(a) - \max_a g(a) \right| \le \max_a |f(a) - g(a)|,$$

which holds for real-valued functions. The analogous inequality holds for $\min$ in place of $\max$.

In the complex case, the selector is $\arg\min_a |Q(b, a)|$. The analogous inequality for the *moduli* is

$$\left| \min_a |f(a)| - \min_a |g(a)| \right| \le \max_a \left| |f(a)| - |g(a)| \right| \le \max_a |f(a) - g(a)|.$$

Both inequalities hold (the first is the scalar case applied to $|f|$ and $|g|$; the second is the reverse triangle inequality).

What fails is the next step. Having bounded the difference between the *moduli* of the selected values, we need to bound the difference between the *selected complex values* themselves, and the moduli bound does not control the arguments.

**Proposition 8.2.1 (Argument discrepancy).** For any $Q_1, Q_2 \in \mathcal{Q}$ and any $b'$, let $a_1 = \pi_{Q_1}(b')$ and $a_2 = \pi_{Q_2}(b')$. Then

$$|Q_1(b', a_1) - Q_2(b', a_2)| \le \|Q_1 - Q_2\|_\infty + |Q_2(b', a_1)| + |Q_2(b', a_2)|.$$

*Proof.* By the triangle inequality,

$$|Q_1(b', a_1) - Q_2(b', a_2)| \le |Q_1(b', a_1) - Q_2(b', a_1)| + |Q_2(b', a_1) - Q_2(b', a_2)|.$$

The first term is at most $\|Q_1 - Q_2\|_\infty$. The second is at most $|Q_2(b', a_1)| + |Q_2(b', a_2)|$. $\square$

**Remark 8.2.2 (The obstruction).** The bound in Proposition 8.2.1 involves $|Q_2(b', a_1)|$ and $|Q_2(b', a_2)|$, which are bounded by $\mid Q_2\mid_\infty$, not by $\mid Q_1 - Q_2\mid_\infty$. As $Q_1 \to Q_2$, the cross-term does not vanish unless $Q_2(b', a_1)$ and $Q_2(b', a_2)$ both vanish. This is the obstruction.

**Remark 8.2.3 (The bound is not tight in general).** The bound in Proposition 8.2.1 is the triangle-inequality bound and may be very loose. In practice, the selected values $Q_2(b', a_1)$ and $Q_2(b', a_2)$ are often close to each other, and the cross-term is small. The failure of the naive proof is a failure of the *proof technique*, not necessarily a failure of the operator. This is why the contraction question is open rather than resolved in the negative.

## 8.3 The three faces of the obstruction

The obstruction has three distinguishable aspects, each of which can be seen independently.

**Face 1 — No total order on $\mathbb{C}$.** The real line is totally ordered, so "the maximum of a set" is well-defined and satisfies the equality $|\max f - \max g| \le \max |f - g|$. The complex plane is not totally ordered. The modulus provides a partial order by magnitude, but two complex numbers of equal modulus may differ in argument, and the tie-breaking rule must choose one. This choice may not respect the geometry of the problem.

**Face 2 — Discontinuity of the selector.** The map $Q \mapsto \pi_Q$ is discontinuous at any $Q$ where two actions have equal modulus at some state. An arbitrarily small perturbation of $Q$ can switch the selected action, causing a discrete jump in the selected value. The Bellman operator therefore inherits a discontinuity at the tie set.

**Face 3 — Phase cancellation.** Even when the selected actions agree, the *values* selected by the two functions may differ in argument. If $Q_1$ and $Q_2$ are close in modulus but point in opposite directions, their difference can be large relative to $\|Q_1 - Q_2\|_\infty$, because the sup-norm measures the maximum modulus of the difference, not the maximum difference of arguments.

**Remark 8.3.1 (The three faces are one).** The three aspects are different views of the same phenomenon: the modulus discards phase information, and phase differences between nearly-equal-modulus values can be arbitrary. The obstruction is structural, not a deficiency of any particular proof.

**Remark 8.3.2 (Where the obstruction is active).** The obstruction is active only when the arguments of the selected values differ. In the symmetric case, or in the phase-cone case (Section 8.6), the arguments are confined and the obstruction is controlled. The question is whether the arguments can be confined in general.

## 8.4 The status of the counterexample question

**Proposition 8.4.1 (Restricted positive result).** Define the *scalar modulus operator* 

$$\hat{T} : \mathcal{B}(\mathcal{B}, \mathbb{R}_{\geq 0}) \rightarrow \mathcal{B}(\mathcal{B}, \mathbb{R}_{\geq 0})$$ 

by

$$(\hat{T}V)(b) = \min_{a \in \mathcal{A}} \mathbb{E}_{b' \sim p(\cdot \mid b, a)}\left[|z(b, a, b')| + \lambda \, V(b')\right].$$

Then $\hat{T}$ is a $\lambda$-contraction on 

$$(\mathcal{B}(\mathcal{B}, \mathbb{R}_{\ge 0}), \|\cdot\|_\infty)$$ 

with a unique fixed point $V^\dagger$, and value iteration converges at rate $\lambda^n$.

*Proof.* For $V_1, V_2$:

$$|(\hat{T}V_1)(b) - (\hat{T}V_2)(b)| \le \max_a \left|\mathbb{E}_{b'}\left[\lambda V_1(b') - \lambda V_2(b')\right]\right| \le \lambda \, \|V_1 - V_2\|_\infty.$$

The first inequality is the scalar case applied to the real-valued functions $f(a) = \mathbb{E}[|z| + \lambda V_1]$ and $g(a) = \mathbb{E}[|z| + \lambda V_2]$; the second is the modulus of expectation. $\square$

**Remark 8.4.2 (What the scalar modulus operator computes).** The operator $\hat{T}$ computes the *modulus* of the optimal value function. It does not compute the complex value itself, and it does not recover the phase. The framework's optimality problem is therefore only partially resolved by $\hat{T}$: the magnitude is tractable, the phase is not.

**Problem 8.4.3 (Counterexample).** Does there exist a cMDP, a discount $\lambda \in (0, 1)$, and two functions $Q_1, Q_2 \in \mathcal{Q}$ such that

$$\|TQ_1 - TQ_2\|_\infty > \lambda \, \|Q_1 - Q_2\|_\infty?$$

**Remark 8.4.4 (Status of the counterexample problem).** Open. Attempts to construct a counterexample have been unsuccessful, and attempts to prove contraction have also been unsuccessful. The naive proof fails (Proposition 8.2.1), but no failure of the operator itself has been exhibited.

**Conjecture 8.4.5 (Contraction conjecture).** The Bellman optimality operator $T$ is a $\lambda$-contraction on $(\mathcal{Q}, \|\cdot\|_\infty)$.

**Remark 8.4.6 (Why the conjecture is plausible).** The conjecture is motivated by three observations. First, the moduli of the selected values are controlled by the scalar modulus operator $\hat{T}$ (Proposition 8.4.1). Second, the arguments of the fixed point are confined to the first quadrant under the submartingale condition (Proposition 8.5.1 below). Third, in the phase-cone case (Proposition 8.6.2), the contraction goes through. Together these suggest that the operator contracts in general, but the proof requires controlling the cross-term in Proposition 8.2.1, which has not been done.

**Remark 8.4.7 (Why a counterexample would matter).** If a counterexample exists, the framework's value-based optimality theory is incomplete: the Bellman optimality operator would not have the contraction property that justifies Banach's theorem, and value iteration might not converge. This would force a reformulation, either via the two-selector formulation (Chapter 9) or via a different fixed-point argument (Schauder, monotonicity, etc.).

## 8.5 The fixed point in the upper half-plane

Despite the uncertainty about contraction, the fixed point (if it exists) has a constrained location.

**Proposition 8.5.1 (Non-negative imaginary part at the fixed point).** If $Q^\* \in \mathcal{Q}$ satisfies $TQ^\* = Q^\*$ and the potential $\phi$ satisfies the submartingale condition, then

$$\mathrm{Im} Q^\*(b, a) \ge 0 \qquad \text{for all } (b, a).$$

*Proof.* The imaginary part of the fixed point satisfies the evaluation equation for the policy $\pi_{Q^\*}$:

$$Q_I^\*(b, a) = \mathbb{E}_{b'}[d(b, a, b') + \lambda \, Q_I^\*(b', \pi_{Q^\*}(b'))].$$

By Proposition 3.2.2, $Q_I^\* \ge 0$. $\square$

**Proposition 8.5.2 (Real part is non-negative).** Under the same conditions, $\mathrm{Re} Q^\*(b, a) \ge 0$ for all $(b, a)$.

*Proof.* The real part satisfies

$$Q_R^\*(b, a) = \mathbb{E}_{b'}[c(b, a, b') + \lambda \, Q_R^*(b', \pi_{Q^\*}(b'))].$$

Since $c \ge 0$ and the expectation preserves non-negativity, iterating the Bellman equation gives $Q_R^\* \ge 0$. $\square$

**Corollary 8.5.3 (First quadrant).** Under the conditions of Propositions 8.5.1 and 8.5.2, $Q^\*(b, a)$ lies in the first quadrant:

$$Q^\*(b, a) \in \lbrace w \in \mathbb{C} : \mathrm{Re}(w) \ge 0, \mathrm{Im}(w) \ge 0\rbrace$$

*Proof.* Combine the two propositions. $\square$

**Remark 8.5.4 (The fixed point is confined to a quarter-plane).** Under the submartingale condition, the fixed point of $T$ lies in the first quadrant. This is a substantial structural constraint: the arguments of $Q^\*(b, a)$ lie in $[0, \pi/2]$. Whether this constraint can be leveraged to prove contraction is the subject of Section 8.6.

## 8.6 The phase cone

The quarter-plane constraint suggests a refinement: if the arguments of the selected values are confined to a small range, the obstruction may weaken.

**Definition 8.6.1 (Phase cone).** For $\theta \in [0, \pi]$, the *phase cone* of half-width $\theta$ is

$$C_\theta = \{w \in \mathbb{C} \setminus \{0\} : |\mathrm{Arg}(w)| \le \theta\} \cup \{0\}.$$

**Proposition 8.6.2 (Contraction on a phase cone).** Let $M > 0$ and suppose $Q_1, Q_2 \in \mathcal{Q}$ satisfy $Q_i(b, a) \in C_\theta \cap \overline{B(0, M)}$ for all $(b, a)$, $i = 1, 2$. Then

$$\|TQ_1 - TQ_2\|_\infty \le \lambda \, (1 + 2\sin\theta) \, \|Q_1 - Q_2\|_\infty + \lambda \, 2\sin\theta \cdot M.$$

*Proof.* For each $b'$, let $a_1 = \pi_{Q_1}(b')$ and $a_2 = \pi_{Q_2}(b')$. By Proposition 8.2.1,

$$|Q_1(b', a_1) - Q_2(b', a_2)| \le \|Q_1 - Q_2\|_\infty + |Q_2(b', a_1) - Q_2(b', a_2)|.$$

Since $Q_2(b', a_2)$ minimizes the modulus and both values are in $C_\theta$, we have $|Q_2(b', a_2)| \le |Q_2(b', a_1)| \le M$, and the arguments of $Q_2(b', a_1)$ and $Q_2(b', a_2)$ differ by at most $2\theta$. Hence

$$|Q_2(b', a_1) - Q_2(b', a_2)| \le 2\sin\theta \cdot |Q_2(b', a_1)| \le 2\sin\theta \cdot M.$$

Substituting gives the bound. Taking expectations and multiplying by $\lambda$ gives the stated result. $\square$

**Corollary 8.6.3 (Contraction when $M \le \|Q_1 - Q_2\|_\infty$).** If the bound $M$ on the cone values satisfies $M \le \|Q_1 - Q_2\|_\infty$, then

$$\|TQ_1 - TQ_2\|_\infty \le \lambda \, (1 + 4\sin\theta) \, \|Q_1 - Q_2\|_\infty.$$

If in addition $\theta < \arcsin((1/\lambda - 1)/4)$, the factor $\lambda(1 + 4\sin\theta) < 1$ and $T$ is a contraction.

*Proof.* Substituting $M \le \|Q_1 - Q_2\|_\infty$ into Proposition 8.6.2 gives the bound. The condition on $\theta$ ensures the factor is less than $1$. $\square$

**Remark 8.6.4 (The cone bound is conditional).** Proposition 8.6.2 requires both the phase-cone assumption and a bound $M$ on the values. In the neighborhood of a fixed point with $Q^*$ small, the bound $M$ is small, and the contraction condition is easier to satisfy. Globally, the cone assumption may not hold.

**Conjecture 8.6.5 (Local contraction near equilibrium).** Let $Q^\*$ be a fixed point of $T$ with $\mathrm{Im} Q^\* \ge 0$. Then there exists a neighborhood $U$ of $Q^\*$ in $(\mathcal{Q}, \|\cdot\|_\infty)$ on which $T$ is a contraction.

**Remark 8.6.6 (The path to a local theory).** Conjecture 8.6.5 is weaker than Conjecture 8.4.5 (global contraction) and may be more tractable. If true, it would give a local convergence result for value iteration near the fixed point, which is the regime of practical interest. The proof would likely proceed by showing that $Q_I \to 0$ near $Q^\*$, so the phase cone shrinks, and the bound of Proposition 8.6.2 becomes effective with $M$ small.

## 8.7 Summary

The Bellman optimality operator for the complex framework is not obviously a $\lambda$-contraction. The naive proof fails because the modulus-greedy selector is discontinuous at ties and discards phase information, so the selected values of two nearby functions can differ by more than $\|Q_1 - Q_2\|_\infty$.

**The obstruction has three faces:** no total order on $\mathbb{C}$, discontinuity of the selector, and phase cancellation between nearly-equal-modulus values.

**Two positive results are established:**

- The scalar modulus operator $\hat{T}$ is a $\lambda$-contraction on the space of non-negative real functions (Proposition 8.4.1). It computes the modulus of the optimal value but not the value itself.
- The Bellman optimality operator $T$ is a contraction on a phase cone of sufficiently small half-width, with a bound on the values in the cone (Proposition 8.6.2, Corollary 8.6.3).

**Structural facts about the fixed point:**

- Under the submartingale condition, the imaginary part of the fixed point is non-negative (Proposition 8.5.1).
- The real part is non-negative (Proposition 8.5.2).
- The fixed point lies in the first quadrant (Corollary 8.5.3).

**The contraction question (OP1) is open:** no proof, no counterexample. The conjecture is that $T$ is a contraction, but the naive proof fails and no alternative proof is known. A local contraction result (Conjecture 8.6.5) is a weaker target that may be attainable.

This chapter establishes the optimality problem and the gap that remains. The next chapter introduces the two-selector formulation, which reframes the problem by working on the product space $\mathcal{Q} \times \mathcal{Q}$.

## Exercises

**Exercise 8.1.** For a cMDP with two states and two actions, choose specific utilities and transitions such that the modulus-greedy policy is not unique at some state (i.e., two actions have equal modulus). Identify the tie set.

**Exercise 8.2.** For the cMDP of Exercise 8.1, compute $\pi_Q$ for two different tie-breaking rules. Show that the resulting policies differ.

**Exercise 8.3.** Verify Proposition 8.2.1 for a specific pair $Q_1, Q_2 \in \mathcal{Q}$. Compute the left-hand side and the right-hand side of the inequality. Is the bound tight? If not, how loose is it?

**Exercise 8.4.** Construct a cMDP and two functions $Q_1, Q_2 \in \mathcal{Q}$ such that the argument discrepancy bound (Proposition 8.2.1) is tight.

**Exercise 8.5.** Verify Proposition 8.4.1 for a specific cMDP. Compute the fixed point $V^\dagger$ of $\hat{T}$ and compare it to $|Q^*|$ (if $Q^*$ exists).

**Exercise 8.6.** Prove that the scalar modulus operator $\hat{T}$ is a $\lambda$-contraction. (This is a specific case of the more general evaluation contraction; write out the proof.)

**Exercise 8.7.** Construct a cMDP where the scalar modulus operator's fixed point $V^\dagger$ equals $|Q^*|$ for the fixed point $Q^*$ of the complex Bellman operator (if it exists). Is this always the case? If not, give a counterexample.

**Exercise 8.8.** Verify Proposition 8.5.1 for a specific cMDP with a submartingale potential. Compute $Q_I^*$ and check that it is non-negative.

**Exercise 8.9.** Verify Corollary 8.5.3 (first quadrant) for a specific cMDP. Compute $Q^*$ and check that both real and imaginary parts are non-negative.

**Exercise 8.10.** For a cMDP where the potential is not a submartingale, give an example where $Q_I^*$ has negative entries. What does the fixed point look like?

**Exercise 8.11.** Verify Proposition 8.6.2 for a specific pair $Q_1, Q_2$ in a phase cone. Compute both sides of the contraction inequality.

**Exercise 8.12.** For $M = 1$ and $\lambda = 0.5$, compute the threshold $\theta^*$ such that the contraction factor is $< 1$. Verify Corollary 8.6.3.

**Exercise 8.13 (Discussion).** The three faces of the obstruction (no total order, discontinuous selector, phase cancellation) are different views of the same phenomenon. Is this a fair assessment? Give an example where one face is more prominent than the others.

**Exercise 8.14 (Discussion).** The scalar modulus operator computes the modulus of the optimal value, not the value itself. In what applications would this be sufficient? In what applications would the phase be essential?

**Exercise 8.15 (Open).** Try to construct a counterexample to Conjecture 8.4.5: find a cMDP, a discount $\lambda \in (0,1)$, and two functions $Q_1, Q_2$ such that $\mid TQ_1 - TQ_2\mid_\infty > \lambda \mid Q_1 - Q_2\mid_\infty$. If you can't, try to prove the conjecture under additional hypotheses.

**Exercise 8.16 (Open).** The local contraction conjecture (8.6.5) is weaker than the global contraction conjecture (8.4.5). Prove the local version, or find a counterexample.

**Exercise 8.17 (Open).** The phase-cone contraction (Proposition 8.6.2) requires $M \le \|Q_1 - Q_2\|_\infty$. Can this condition be relaxed? For instance, is the contraction valid if $M$ is merely bounded (not necessarily small)?

**Exercise 8.18 (Open).** The fixed point $Q^\*$ lies in the first quadrant under the submartingale condition. Does this constrain the phase cone of $Q^\*$? Specifically, is the argument spread of $Q^\*(b, \cdot)$ across actions bounded?
