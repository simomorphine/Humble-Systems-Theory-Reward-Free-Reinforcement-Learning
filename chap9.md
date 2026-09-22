# Chapter 9 — The Two-Selector Formulation

*(Revised with exercises)*

## 9.1 Motivation

Chapter 8 established that the single-selector Bellman optimality operator $T$ is not obviously a contraction, and that the naive proof fails because the modulus-greedy rule collapses the bitopological structure of the framework into a single topology.

The two-selector formulation is the natural response. It maintains two value functions — one for the forward direction and one for the backward — and updates them jointly. The forward and backward selectors correspond to the two topologies of the bitopological space (Chapter 5), and their joint evolution reflects the framework's geometric structure.

The two-selector formulation does not resolve OP1 by itself. What it does is reframe the optimality problem in terms of the framework's geometry, identify the structure that a resolution would need to respect, and introduce the *disequilibrium gap* as the framework's natural measure of how far a system is from epistemic equilibrium.

## 9.2 Forward and backward selectors

**Definition 9.2.1 (Forward-greedy selector).** Given $Q \in \mathcal{Q}$ and a state $b \in \mathcal{B}$, the *forward-greedy selector* is
$$\pi_Q^+(b) = \arg\min_{a \in \mathcal{A}} |Q(b, a)|,$$
with ties broken by a fixed deterministic rule.

**Definition 9.2.2 (Backward-greedy selector).** Given $Q \in \mathcal{Q}$ and a state $b \in \mathcal{B}$, the *backward-greedy selector* is
$$\pi_Q^-(b) = \arg\min_{a \in \mathcal{A}} |Q(b, a)|,$$
with ties broken by the *reverse* deterministic rule.

**Remark 9.2.3 (When the selectors differ).** The forward and backward selectors differ only in the tie-breaking rule. In the absence of ties, they coincide. The distinction between them is therefore not about their definitions — both minimize the modulus at the current state — but about the *reachability direction* they encode. In a symmetric environment, forward and backward reachability coincide, and the two selectors agree. In an asymmetric environment, they may differ, and the difference is the source of the framework's distinctive structure.

**Definition 9.2.4 (Forward and backward value functions).** For a pair $(Q^+, Q^-) \in \mathcal{Q} \times \mathcal{Q}$:

- The *forward value function* $Q^+$ is the value function under the forward selector.
- The *backward value function* $Q^-$ is the value function under the backward selector.

## 9.3 The two-selector operator

**Definition 9.3.1 (Component operators).** Define $T^+, T^- : \mathcal{Q} \to \mathcal{Q}$ by

$$(T^+ Q)(b, a) = \mathbb{E}_{b' \sim p(\cdot \mid b, a)}\left[z(b, a, b') + \lambda \, Q(b', \pi^+_Q(b'))\right],$$

$$(T^- Q)(b, a) = \mathbb{E}_{b' \sim p(\cdot \mid b, a)}\left[z(b, a, b') + \lambda \, Q(b', \pi^-_Q(b'))\right].$$

**Definition 9.3.2 (Two-selector operator).** The *two-selector Bellman operator* is

$$T_{\rightarrow\leftarrow} : \mathcal{Q} \times \mathcal{Q} \to \mathcal{Q} \times \mathcal{Q},$$

$$T_{\rightarrow\leftarrow}(Q^+, Q^-) = (T^+ Q^-, \ T^- Q^+).$$

The forward component uses the backward selector of $Q^-$, and the backward component uses the forward selector of $Q^+$. This cross-coupling is the essential feature.

**Proposition 9.3.3 (Well-definedness).** $T_{\rightarrow\leftarrow}$ maps $\mathcal{Q} \times \mathcal{Q}$ into itself.

*Proof.* For $Q^+, Q^- \in \mathcal{Q}$ with bounded sup-norms, each component of $T_{\rightarrow\leftarrow}(Q^+, Q^-)$ is bounded by $Z_{\max} + \lambda \max(\mid Q^+\mid_\infty, \|Q^-\|_\infty)$ $\square$

**Remark 9.3.4 (Why the cross-coupling?).** The cross-coupling ensures that each selector is informed by the value function optimized under the other selector. If the coupling were same-sided (i.e. $T^+$ using $Q^+$), the two selectors would evolve independently, and the operator would reduce to the single-selector case applied twice. The cross-coupling is what enforces the bitopological structure and is the natural expression of the framework's geometry.

## 9.4 The product sup-norm

**Definition 9.4.1 (Product sup-norm).** For $(Q^+, Q^-) \in \mathcal{Q} \times \mathcal{Q}$, define

$$\|(Q^+, Q^-)\|_{\infty, \times} = \max\left(\|Q^+\|_\infty, \|Q^-\|_\infty\right).$$

**Proposition 9.4.2 (Product space is a Banach space).** $(\mathcal{Q} \times \mathcal{Q}, \|\cdot\|_{\infty, \times})$ is a Banach space.

*Proof.* $\mathcal{Q}$ is a Banach space, and the product of two Banach spaces with the max-norm is a Banach space. $\square$

## 9.5 The contraction question for the two-selector operator

The natural question is whether $T_{\rightarrow\leftarrow}$ is a contraction. The expectation is that the two-selector formulation avoids the obstruction that defeats the single-selector operator. This expectation is not met.

**Theorem 9.5.1 (Naive proof fails).** The naive contraction proof for $T_{\rightarrow\leftarrow}$ fails. The obstruction of Chapter 8 reappears in each component.

*Proof.* Consider the forward component:

$$(T^+ Q_1^-)(b, a) - (T^+ Q_2^-)(b, a) = \lambda \, \mathbb{E}_{b'}\left[Q_1^-(b', \pi^+_{Q_1^-}(b')) - Q_2^-(b', \pi^+_{Q_2^-}(b'))\right].$$

The selector

$$
\pi^+_{Q^-}
$$

depends on

$$
Q^-
$$

itself, so the two terms in the difference are evaluated at *different* actions

$$
a_1 = \pi^+_{Q_1^-}(b')
$$

and

$$
a_2 = \pi^+_{Q_2^-}(b').
$$

The triangle-inequality bound gives

$$|Q_1^-(b', a_1) - Q_2^-(b', a_2)| \le \|Q_1^- - Q_2^-\|_\infty + |Q_2^-(b', a_1)| + |Q_2^-(b', a_2)|,$$

which is the same bound as in Proposition 8.2.1. The bound involves $|Q_2^-(b', a_1)|$ and $|Q_2^-(b', a_2)|$, which do not vanish as $Q_1^- \to Q_2^-$. The same obstruction applies to the backward component. $\square$

**Remark 9.5.2 (The cross-coupling does not resolve the obstruction).** The intuition that guided the two-selector formulation — that cross-coupling would separate the selectors and prevent the modulus-greedy discontinuity from affecting both components at once — is incorrect. The discontinuity is in the selector itself, not in the coupling. Each component of the two-selector operator inherits the same selector-induced discontinuity as the single-selector operator. The cross-coupling changes the dynamics but does not remove the obstruction.

## 9.6 The disequilibrium gap

Even though the two-selector operator does not resolve OP1, it introduces a natural quantity: the *gap* between the forward and backward value functions.

**Definition 9.6.1 (Disequilibrium gap).** For $(Q^+, Q^-) \in \mathcal{Q} \times \mathcal{Q}$, the *disequilibrium gap* is
$$\Delta Q = Q^+ - Q^- \in \mathcal{Q}.$$

**Definition 9.6.2 (Epistemic equilibrium).** A pair $(Q^{\*+}, Q^{\*-})$ is in *epistemic equilibrium* if it is a fixed point of $T_{\rightarrow\leftarrow}$ and $\Delta Q^\* = 0$.

**Proposition 9.6.3 (Gap structure).** At a fixed point of $T_{\rightarrow\leftarrow}$,

$$\Delta Q^\*(b, a) = \lambda \left(C^+(b) - C^-(b)\right),$$

where

$$C^+(b) = \mathbb{E}_{b'}[Q^{\*-}(b', \pi^+_{Q^{\*-}}(b'))], \qquad C^-(b) = \mathbb{E}_{b'}[Q^{\*+}(b', \pi^-_{Q^{\*+}}(b'))].$$

*Proof.* Subtract the two fixed-point equations:

$$Q^{\*+}(b, a) - Q^{\*-}(b, a) = \lambda \left(C^+(b) - C^-(b)\right). \qquad \square$$

**Corollary 9.6.4 (Gap is action-independent).** The disequilibrium gap $\Delta Q^\*(b, a)$ does not depend on $a$. It is a function of $b$ alone.

**Corollary 9.6.5 (Gap identity).** Let $\Theta(b') = Q^{*-}(b', a^+(b')) - Q^{*+}(b', a^-(b'))$ where $a^+(b') = \pi^+_{Q^{*-}}(b')$ and $a^-(b') = \pi^-_{Q^{*+}}(b')$. Then
$$\Delta Q^*(b) = \lambda \, \mathbb{E}_{b'}[\Theta(b')].$$
Iterating:
$$\Delta Q^*(b) = \sum_{k=0}^\infty \lambda^{k+1} \, \mathbb{E}[\Theta(B_{t+k+1}) \mid B_t = b].$$
The gap is the discounted sum of future cross-terms.

*Proof.* Substitute the fixed-point equation for $\Delta Q^*$ at $b'$ back into the expression for $\Delta Q^*(b)$. $\square$

**Remark 9.6.6 (The cross-term depends only on the utility).** Let $Z(b, a) = \mathbb{E}_{b'}[z(b, a, b')]$. At a fixed point, $Q^{*\pm}(b, a) = Z(b, a) + \lambda C^\pm(b)$, so
$$\Theta(b') = Z(b', a^+(b')) - Z(b', a^-(b')).$$
The cross-term depends only on the utility $Z$ and the two selectors, not on the value functions themselves. This is a key structural simplification.

**Conjecture 9.6.7 (Gap-vanishing).** At any fixed point of the two-selector operator, $\Delta Q^* = 0$.

**Remark 9.6.8 (Status of the conjecture).** The conjecture is supported by extensive but non-exhaustive hand-computed examples. No proof and no counterexample are known. The gap identity (Corollary 9.6.5) reduces the conjecture to the question of whether the cross-terms $\Theta(b')$ can be non-zero in a way that survives the discounted sum.

## 9.7 Reformulations

If the two-selector formulation is to yield a contraction theorem, one of several modifications is necessary. Three directions are available.

### 9.7.1 Gap-stable selectors

**Definition 9.7.1 (Gap-stable selector).** A selector $\pi_Q$ is *gap-stable with margin $\delta > 0$* on a set $\mathcal{G} \subseteq \mathcal{Q}$ if, for every $Q \in \mathcal{G}$ and every $b \in \mathcal{B}$,
$$|Q(b, \pi_Q(b))| \le |Q(b, a)| - \delta \qquad \text{for all } a \neq \pi_Q(b).$$

**Proposition 9.7.2 (Contraction with gap-stable selectors).** Let $\mathcal{G}$ be a subset of $\mathcal{Q}$ on which the selector $\pi_Q$ is gap-stable with margin $\delta > 0$. Then on $\mathcal{G}$, the Bellman optimality operator $T$ is a contraction with modulus $\lambda$, provided the perturbation radius is small enough that the selector remains constant.

*Proof.* On a ball of radius $\delta/2$ around any $Q \in \mathcal{G}$, the gap condition ensures the selector $\pi_{Q'}$ is constant for all $Q'$ in the ball. Hence on this ball, $T$ reduces to an evaluation operator with a fixed policy, and the evaluation contraction (Theorem 7.2.3) applies. $\square$

**Remark 9.7.3 (Gap-stability is not preserved).** The gap-stable condition is not preserved under the Bellman iteration in general. It is a condition on the fixed point, not on the operator. Whether the fixed point of $T$ satisfies gap-stability depends on the cMDP.

### 9.7.2 Smoothed selectors

**Definition 9.7.4 (Soft modulus-greedy selector).** For $\tau > 0$, the *soft modulus-greedy selector* is
$$\pi_\tau(a \mid b, Q) = \frac{\exp(-|Q(b, a)| / \tau)}{\sum_{a' \in \mathcal{A}} \exp(-|Q(b, a')| / \tau)}.$$

**Proposition 9.7.5 (Soft Bellman operator is a contraction).** Define $T_\tau$ by replacing the hard selector with the soft selector. Then $T_\tau$ is a contraction on $(\mathcal{Q}, \|\cdot\|_\infty)$ for sufficiently large $\tau$ relative to $\lambda$, and its fixed point $Q_\tau^*$ satisfies $Q_\tau^* \to Q^*$ as $\tau \to 0$ whenever $Q^*$ exists.

*Sketch.* The soft selector is Lipschitz in $Q$ with Lipschitz constant $O(1/\tau)$. The Bellman operator with a Lipschitz selector is a contraction when $\lambda(1 + \text{Lip}(\pi_\tau)) < 1$, i.e. for sufficiently large $\tau$ relative to $\lambda$. The limit $\tau \to 0$ recovers the hard selector. $\square$

**Remark 9.7.6 (The price of smoothing).** The soft selector resolves the contraction problem by making the operator Lipschitz, but the contraction modulus depends on the temperature $\tau$, and as $\tau \to 0$ the modulus approaches $1$ (or fails). The smoothed operator is a useful tool for existence and approximation results (Chapter 11), but it does not give a contraction for the hard problem.

### 9.7.3 Phase-cone restriction

**Definition 9.7.7 (Phase-cone subspace).** For $\theta \in [0, \pi/2)$, the *phase-cone subspace* is
$$\mathcal{Q}_\theta = \{Q \in \mathcal{Q} : Q(b, a) \in C_\theta \text{ for all } (b, a)\}.$$

**Proposition 9.7.8 (Contraction on the phase-cone subspace).** On $\mathcal{Q}_\theta \cap \overline{B(0, M)}$ for sufficiently small $\theta$ and $M$, the Bellman optimality operator $T$ is a contraction.

*Proof.* Proposition 8.6.2 and Corollary 8.6.3 applied to the phase-cone subspace. $\square$

**Remark 9.7.9 (Why the phase-cone restriction is the most promising).** The fixed point of $T$ lies in the first quadrant under the submartingale condition (Corollary 8.5.3). If the arguments of the fixed point are further restricted — e.g. by the submartingale condition plus additional structure — then the phase cone shrinks, and the contraction applies. The phase-cone restriction is the most closely tied to the framework's structure and the most likely to give a global result.

**Problem 9.7.10 (Phase-cone contraction).** Under what conditions on the cMDP does the fixed point of $T$ lie in $\mathcal{Q}_\theta$ for some $\theta < \pi/4$? This is the essential open question for the phase-cone approach.

## 9.8 What the two-selector formulation achieves

Despite the failure of the naive contraction proof, the two-selector formulation achieves several things.

**First, it isolates the difficulty.** The single-selector operator is a special case of the two-selector operator (when $Q^+ = Q^-$). The two-selector formulation makes the source of the difficulty visible: the discontinuity of the selector, not the structure of the operator.

**Second, it provides a natural interpretation of asymmetry.** The two value functions $Q^+$ and $Q^-$ correspond to the forward and backward reachability structures of the framework. Their difference,
$$\Delta Q^* = Q^{*+} - Q^{*-},$$
is the framework's measure of disequilibrium. It is a complex-valued function on state space, and it vanishes when forward and backward selectors agree.

**Third, it opens a path to a fixed-point theory via Schauder.** Even if the contraction is not established, the two-selector operator has a fixed point for finite cMDPs, by Schauder's theorem applied to a smoothed version (Theorem 11.3.4). The two-selector formulation gives a natural setting for this argument.

**Fourth, it matches the framework's geometry.** The bitopological structure of Chapter 5 predicts two value functions, not one. The two-selector formulation is the natural expression of this prediction. Even without a contraction proof, the formulation is correct as a description of the framework's geometry.

**Fifth, it introduces the disequilibrium gap as the framework's central state variable.** The gap $\Delta Q^*$ is the natural measure of how far the system is from epistemic equilibrium. Its structure — action-independent, discounted sum of cross-terms, bounded by the utility's argument spread — is a genuine structural result.

## 9.9 Epistemic equilibrium in the two-selector formulation

**Definition 9.9.1 (Epistemic equilibrium).** A pair $(Q^{*+}, Q^{*-})$ is in *epistemic equilibrium* if it is a fixed point of $T_{\rightarrow\leftarrow}$ and $Q^{*+} = Q^{*-}$.

**Proposition 9.9.2 (Single-selector fixed points are epistemic equilibria).** If $Q^*$ is a fixed point of the single-selector operator $T$, then $(Q^*, Q^*)$ is a fixed point of $T_{\rightarrow\leftarrow}$.

*Proof.* If $\pi_{Q^*} = \pi^+_{Q^*} = \pi^-_{Q^*}$ (which holds whenever there are no ties), then $T^+ Q^* = T^- Q^* = TQ^* = Q^*$. Hence $T_{\rightarrow\leftarrow}(Q^*, Q^*) = (Q^*, Q^*)$. $\square$

**Remark 9.9.3 (Equilibrium and disequilibrium).** At epistemic equilibrium, the forward and backward value functions agree. The system has no preferred direction. When they differ, the system has a preferred direction, and the gap $\Delta Q^*$ measures the disequilibrium. The framework's central interpretive claim (Chapter 13) is that the system converges to epistemic equilibrium under the HST Equilibrium Axiom.

**Remark 9.9.4 (The gap-vanishing conjecture and epistemic equilibrium).** If the gap-vanishing conjecture (9.6.7) is true, then every fixed point of $T_{\rightarrow\leftarrow}$ is an epistemic equilibrium, and the distinction between "fixed point" and "epistemic equilibrium" collapses. If the conjecture is false, then there are fixed points that are not equilibria — states of *persistent disequilibrium*, where the system has a preferred direction that the dynamics cannot resolve.

## 9.10 Summary

The two-selector formulation was proposed as a natural expression of the framework's bitopological structure. It maintains forward and backward value functions and updates them jointly through a cross-coupled operator.

**The naive contraction proof fails for the two-selector operator** (Theorem 9.5.1). The obstruction of Chapter 8 reappears in each component; the cross-coupling does not remove the selector-induced discontinuity.

**The disequilibrium gap** $\Delta Q = Q^+ - Q^-$ is the framework's natural measure of disequilibrium. It has the following properties:

- At a fixed point, it is action-independent (Corollary 9.6.4).
- It satisfies the identity $\Delta Q^*(b) = \sum_k \lambda^{k+1}\mathbb{E}[\Theta(b_k)]$ (Corollary 9.6.5).
- The cross-term $\Theta(b')$ depends only on the utility (Remark 9.6.6).

**The gap-vanishing conjecture** (9.6.7) states that the gap vanishes at every fixed point. It is supported by examples but unproven.

**Three reformulations are available:** gap-stable selectors (§9.7.1), smoothed selectors (§9.7.2), and phase-cone restriction (§9.7.3). The phase-cone restriction is the most promising.

**The two-selector formulation has content even without a contraction theorem.** It isolates the difficulty, provides a natural interpretation of asymmetry, opens a path to fixed-point existence via Schauder, matches the framework's geometry, and introduces the disequilibrium gap.

The chapter is honest that the two-selector formulation, as originally proposed, does not resolve OP1. It reframes the problem in terms of the framework's geometry and introduces the gap as the central state variable, but the contraction question remains open.

## Exercises

**Exercise 9.1.** For a cMDP with two states and two actions, choose specific utilities such that the forward and backward selectors differ at some state (i.e., there is a tie). Identify the state and the actions.

**Exercise 9.2.** Compute $T_{\rightarrow\leftarrow}(Q^+, Q^-)$ for a specific pair $(Q^+, Q^-)$ in the cMDP of Exercise 9.1. Verify that the result is in $\mathcal{Q} \times \mathcal{Q}$.

**Exercise 9.3.** Verify Proposition 9.3.3 (well-definedness) for the cMDP of Exercise 9.1. Compute the bound $Z_{\max} + \lambda \max(\|Q^+\|_\infty, \|Q^-\|_\infty)$.

**Exercise 9.4.** For the same cMDP, compute the gap $\Delta Q = Q^+ - Q^-$ and verify Corollary 9.6.4 (gap is action-independent at a fixed point).

**Exercise 9.5.** Verify the gap identity (Corollary 9.6.5) for a specific cMDP. Compute $\Delta Q^*(b)$ and the sum $\sum_k \lambda^{k+1}\mathbb{E}[\Theta(b_k)]$ and check that they agree.

**Exercise 9.6.** Verify that the cross-term $\Theta(b')$ depends only on the utility $Z$, not on the value functions. Construct a specific cMDP and compute $\Theta(b')$ from both expressions.

**Exercise 9.7.** Find a cMDP where the two-selector operator has a fixed point with non-zero gap (i.e., a counterexample to the gap-vanishing conjecture). If you can't, explain why.

**Exercise 9.8.** Verify Proposition 9.7.2 (contraction with gap-stable selectors) for a specific cMDP. Identify the gap-stable set $\mathcal{G}$ and the margin $\delta$.

**Exercise 9.9.** For the soft modulus-greedy selector (Definition 9.7.4), compute the Lipschitz constant in $Q$ for fixed $\tau$. Show that it scales as $O(1/\tau)$.

**Exercise 9.10.** Verify Proposition 9.7.8 for a specific cMDP with a phase-cone restriction. Identify the cone $\mathcal{Q}_\theta$ and verify the contraction.

**Exercise 9.11.** Show that at a single-selector fixed point, the two-selector operator has a fixed point $(Q^*, Q^*)$ (Proposition 9.9.2).

**Exercise 9.12.** For a cMDP where the potential is a submartingale, verify that the fixed point of $T_{\rightarrow\leftarrow}$ (if it exists) lies in the first quadrant. Does the gap-vanishing conjecture hold for this cMDP?

**Exercise 9.13 (Discussion).** The two-selector formulation is the natural expression of the bitopological structure. But it doesn't resolve OP1. Is the formulation still worthwhile? Argue for and against.

**Exercise 9.14 (Discussion).** The disequilibrium gap is the framework's measure of how far a system is from epistemic equilibrium. Is this interpretation correct? Give an example of a system where the gap is non-zero but the system is "at rest" in some other sense.

**Exercise 9.15 (Open).** Prove or disprove the gap-vanishing conjecture (9.6.7). If the conjecture is true, prove it. If false, construct a counterexample.

**Exercise 9.16 (Open).** The gap identity (Corollary 9.6.5) reduces the gap-vanishing problem to the question of whether cross-terms can persist. Characterize the utilities $Z$ for which cross-terms are always zero.

**Exercise 9.17 (Open).** The phase-cone contraction (Proposition 9.7.8) requires $\theta < \pi/4$. Can this be relaxed? Under what conditions on the cMDP does the fixed point lie in a smaller cone?

**Exercise 9.18 (Open).** The two-selector formulation uses two value functions. Can it be generalized to *multiple* selectors, one for each direction of a more complex bitopological structure? What would that look like?
