# Chapter 4 — The $\gamma$-Distance Family

*(Revised with exercises)*

## 4.1 Definition and basic properties

**Definition 4.1.1 ($\gamma$-distance).** For $\gamma \in [0, 1]$, the $\gamma$-*distance* on $\mathcal{B}$ is

$$
d_\gamma(b, b') = \sqrt{c(b, b')^2 + \gamma^2 \, d(b, b')^2}.
$$

**Proposition 4.1.2 (Basic properties).** For every $\gamma \in [0, 1]$:

- (i) $d_\gamma(b, b) = 0$ for all $b$.
- (ii) $d_\gamma(b, b') \ge 0$ for all $b, b'$.
- (iii) $d_\gamma$ satisfies the triangle inequality.

*Proof.* (i) and (ii) are immediate from the definition. (iii) is Proposition 2.4.3. $\square$

**Proposition 4.1.3 (Monotonicity in $\gamma$).** For $\gamma_1 < \gamma_2$ and any $b, b'$,
$$d_{\gamma_1}(b, b') \le d_{\gamma_2}(b, b').$$
Equality holds if and only if $d(b, b') = 0$.

*Proof.* Immediate from the definition: $\gamma^2 d^2$ is increasing in $\gamma^2$, and the square root is monotone. If $d(b, b') = 0$, both sides equal $c(b, b')$. If $d(b, b') \neq 0$ and $\gamma_1 < \gamma_2$, the inequality is strict. $\square$

**Proposition 4.1.4 (Endpoints).** $d_0(b, b') = c(b, b')$ and $d_1(b, b') = |Q(b, b')|$.

*Proof.* Immediate from the definition. $\square$

**Proposition 4.1.5 (Continuity in $\gamma$).** For fixed $b, b'$, the map $\gamma \mapsto d_\gamma(b, b')$ is continuous on $[0, 1]$. Moreover, the map is Lipschitz in $\gamma$ with constant $|d(b, b')|$.

*Proof.* $d_\gamma^2 = c^2 + \gamma^2 d^2$ is a polynomial in $\gamma$, hence continuous. For the Lipschitz bound: $\partial_\gamma d_\gamma = \gamma d^2 / d_\gamma \le \gamma |d| \le |d|$ when $d_\gamma > 0$. The case $d_\gamma = 0$ requires $c = d = 0$, and the derivative is zero in a neighborhood. $\square$

## 4.2 Metric equivalence

The family $\{d_\gamma : \gamma \in [0, 1]\}$ consists of quasi-metrics related to each other in a controlled way.

**Proposition 4.2.1 (Equivalence bounds).** For any $\gamma_1, \gamma_2 \in [0, 1]$ with $\gamma_1 \le \gamma_2$:

- (i) If $\gamma_1 > 0$, then
$$d_{\gamma_1}(b, b') \le d_{\gamma_2}(b, b') \le \frac{\gamma_2}{\gamma_1} \, d_{\gamma_1}(b, b').$$
- (ii) If $\gamma_1 = 0$, then
$$c(b, b') \le d_{\gamma_2}(b, b') \le c(b, b') + \gamma_2 |d(b, b')|.$$

*Proof.* (i) The left inequality is Proposition 4.1.3. For the right:
$$d_{\gamma_2}^2 = c^2 + \gamma_2^2 d^2 \le \left(\frac{\gamma_2}{\gamma_1}\right)^2 \left(c^2 + \gamma_1^2 d^2\right) = \left(\frac{\gamma_2}{\gamma_1}\right)^2 d_{\gamma_1}^2.$$
Take square roots. (ii) The left inequality is $c \le \sqrt{c^2 + \gamma_2^2 d^2}$. For the right: $\sqrt{c^2 + \gamma_2^2 d^2} \le c + \gamma_2 |d|$ by Minkowski in $\mathbb{R}^2$ applied to $(c, 0)$ and $(0, \gamma_2 |d|)$. $\square$

**Corollary 4.2.2 (Topological equivalence for $\gamma > 0$).** For any $\gamma_1, \gamma_2 \in (0, 1]$, the quasi-metrics $d_{\gamma_1}$ and $d_{\gamma_2}$ induce the same topology on $\mathcal{B}$ (up to the forward/backward distinction, developed in Chapter 5).

*Proof.* By Proposition 4.2.1(i), the two quasi-metrics are equivalent in the standard sense: there exist positive constants $A = 1$ and $B = \gamma_2/\gamma_1$ such that $A \, d_{\gamma_1} \le d_{\gamma_2} \le B \, d_{\gamma_1}$. Equivalent quasi-metrics generate the same topology. $\square$

**Remark 4.2.3 (The case $\gamma = 0$ is special).** If $\gamma_1 = 0$, the equivalence with $\gamma_2 > 0$ fails whenever $|d|$ is unbounded relative to $c$. The $\gamma = 0$ topology is genuinely distinct. This is why the framework treats $\gamma = 0$ as a separate case throughout: it is the pure-cost geometry, and it does not see the debt at all.

## 4.3 Geometric interpretation

**Definition 4.3.1 ($\gamma$-ball).** The $\gamma$-*ball of radius* $r$ *centered at* $b$ is

$$B_\gamma(b, r) = \lbrace b' \in \mathcal{B} : d_\gamma(b, b') < r\rbrace.$$

**Proposition 4.3.2 (Level sets).** For fixed $b$ and $r > 0$, the $\gamma$-ball is the set of $b'$ satisfying

$$c(b, b')^2 + \gamma^2 \, d(b, b')^2 < r^2.$$

In the $(c, d)$-plane, this is the interior of an ellipse with semi-axes $r$ (in the $c$ direction) and $r/\gamma$ (in the $d$ direction).

*Proof.* The condition is a quadratic form in $(c, d)$. The principal axes of the ellipse are along the coordinate axes, with semi-axes determined by the coefficients. $\square$

**Corollary 4.3.3 (Endpoints).** At $\gamma = 1$, the $\gamma$-ball is a disk of radius $r$ in the $(c, d)$-plane. At $\gamma = 0$, it is the region $c(b, b') < r$, independent of $d$.

**Remark 4.3.4 (Deformation as $\gamma$ varies).** As $\gamma$ increases from $0$ to $1$:

- The ball expands in the $d$ direction by a factor of $1/\gamma$.
- The ball is unchanged in the $c$ direction.
- States with small cost but large debt, excluded from small $\gamma$ balls, may be included in large $\gamma$ balls.

This is the geometric picture: $\gamma$ is an anisotropy parameter of the quasi-metric, weighting the debt axis relative to the cost axis.

## 4.4 Sensitivity interpretation

The geometric interpretation of $\gamma$ as an anisotropy parameter admits a system-level reading.

**Definition 4.4.1 (Debt sensitivity).** A system is said to have *debt sensitivity* $\gamma$ if its quasi-metric is $d_\gamma$.

Under this interpretation:

- $\gamma = 0$: the system is insensitive to debt. It acts as a pure cost minimizer.
- $\gamma = 1$: the system is fully sensitive to debt. It weighs debt equally with cost.
- $0 < \gamma < 1$: the system has partial sensitivity.

**Proposition 4.4.2 (Optimal paths depend on sensitivity).** Let $\gamma_1 < \gamma_2$. There exist states $b, b'$ and two paths $P_1, P_2$ from $b$ to $b'$ such that $P_1$ is $d_{\gamma_1}$-optimal and $P_2$ is $d_{\gamma_2}$-optimal, with $P_1 \neq P_2$.

*Proof.* Construct $b, b'$ with two paths: $P_1$ has low cost and high debt, $P_2$ has higher cost and low debt. At $\gamma_1 = 0$, $P_1$ is preferred. At $\gamma_2 = 1$, $P_2$ is preferred if the debt difference is large enough. The threshold at which the preference flips is $\gamma^* \in (0, 1)$. $\square$

**Remark 4.4.3 (Sensitivity is not a parameter choice).** The interpretation of $\gamma$ as sensitivity is not a free parameter choice by the designer. It is a *property of the system*: how much of its own epistemic state does the system have access to? A system that has no introspective access to its uncertainty behaves as if $\gamma = 0$. A system that fully models its uncertainty behaves as if $\gamma = 1$. The value of $\gamma$ for a given system is determined by the system's architecture, not by a tuning procedure.

**Remark 4.4.4 (The framework's strongest claim is at $\gamma = 1$).** The modulus criterion $|z|$ corresponds to $\gamma = 1$. This is the framework's canonical point on the trade-off, and it is the choice that gives the framework its distinctive character. The $\gamma$-family is useful for interpolation and comparison, but the framework's results are stated at $\gamma = 1$ unless otherwise noted.

## 4.5 The contraction threshold

There is a threshold phenomenon in the $\gamma$-family that is relevant to the Bellman operator, though not to the metric itself.

**Proposition 4.5.1 (Modulus-sup bound).** For any $z = c + i\, d \in \mathbb{C}$,
$$|z| \le \sqrt{2} \, \max(|c|, |d|).$$

*Proof.* $|z|^2 = c^2 + d^2 \le 2 \max(c^2, d^2)$. $\square$

**Proposition 4.5.2 (Sufficient contraction condition).** If $T_\gamma$ denotes a Bellman operator acting with $d_\gamma$-modulus on the imaginary component, then $T_\gamma$ is a $\lambda$-contraction in the sup-norm whenever $\gamma < 1/\sqrt{2}$.

*Sketch of proof.* The standard proof of the evaluation contraction uses the triangle inequality for $d_\gamma$. The modulus inequality introduces a factor of $\sqrt{2}$ when comparing $d_\gamma$ to the sup-norm of the pair $(c, d)$. Chasing constants gives $\gamma \sqrt{2} < 1$, i.e. $\gamma < 1/\sqrt{2}$. $\square$

**Remark 4.5.3 (The threshold is not sharp).** The constant $1/\sqrt{2}$ is an artifact of the $\ell^2$ - $\ell^\infty$ equivalence in $\mathbb{R}^2$. It is sufficient, not necessary. A sharper argument using the phase structure of the complex values may extend the contraction to all $\gamma \in [0, 1]$. This is one of the open problems of the framework (OP1 in Part V).

**Remark 4.5.4 (Distinction from the metric property).** The metric property of $d_\gamma$ (Proposition 2.4.3) holds for *all* $\gamma \in [0, 1]$. The contraction of the Bellman operator in $d_\gamma$-modulus holds only for $\gamma < 1/\sqrt{2}$ under the naive proof. These are different results about different objects and should not be conflated. The metric property is about the geometry of state space; the contraction property is about the convergence of a specific operator.

## 4.6 The $\gamma = 1$ case

The case $\gamma = 1$ deserves separate attention, because it is the case in which the metric is exactly the modulus of the complex cost.

**Proposition 4.6.1 (Complex structure at $\gamma = 1$).** At $\gamma = 1$, $d_1(b, b') = |Q(b, b')|$ where $Q = c + i\,d$. The quasi-metric is the modulus of a complex-valued function.

**Proposition 4.6.2 (Phase information).** The quasi-metric $d_1$ loses the argument of $Q$. Two transitions with the same modulus but different arguments are indistinguishable at the level of $d_1$, but distinguishable at the level of $Q$.

*Proof.* $d_1 = |Q|$ is invariant under $Q \mapsto e^{i\alpha} Q$ for any phase $\alpha$. $\square$

**Remark 4.6.3 (The cost of the metric reduction).** The loss of phase information at $\gamma = 1$ is the metric-level manifestation of the general fact that a metric (real-valued) cannot encode the full structure of a complex-valued function. The complex structure is retained by $Q$ itself, not by $d_1$. This motivates the two-selector formulation of Chapter 9: to recover phase information, one maintains two value functions rather than one.

## 4.7 Summary

The $\gamma$-family interpolates between the cost-only geometry ($\gamma = 0$) and the full complex-modulus geometry ($\gamma = 1$).

**Metric equivalence (Proposition 4.2.1, Corollary 4.2.2):** For $\gamma > 0$, all $d_\gamma$ are topologically equivalent. The case $\gamma = 0$ is special: it is the pure-cost geometry and may induce a distinct topology.

**Geometric interpretation (Proposition 4.3.2):** The $\gamma$-ball is an ellipse with semi-axes $r$ and $r/\gamma$. As $\gamma$ increases, the ball expands in the debt direction and is unchanged in the cost direction.

**Sensitivity interpretation (Remark 4.4.3):** $\gamma$ is the system's sensitivity to its own epistemic debt. It is a property of the system, not a design parameter.

**Contraction threshold (Proposition 4.5.2):** $\gamma < 1/\sqrt{2}$ is a sufficient condition for the Bellman operator under the naive proof. It is not sharp and may be extendable.

**The $\gamma = 1$ case (Proposition 4.6.1):** At $\gamma = 1$, the metric is the modulus of the complex cost, and phase information is lost at the metric level. The complex structure is retained by $Q$ itself, not by $d_1$.

This chapter establishes the framework's parameter family and its basic properties. The next chapter turns to the framework's distinctive feature: the asymmetry of the complex quasi-metric and the bitopological structure it generates.

## Exercises

**Exercise 4.1.** For a two-state system with $c(b_1, b_2) = 3$, $d(b_1, b_2) = 4$, compute $d_\gamma(b_1, b_2)$ for $\gamma = 0$, $\gamma = 0.5$, and $\gamma = 1$. Verify the monotonicity of $d_\gamma$ in $\gamma$.

**Exercise 4.2.** For the same system, compute the $\gamma$-balls $B_\gamma(b_1, 1)$ for $\gamma = 0, 0.5, 1$. Describe the shape of each ball in the $(c, d)$-plane.

**Exercise 4.3.** Verify Proposition 4.2.1(i) for $\gamma_1 = 0.5$, $\gamma_2 = 1$, and the transition from Exercise 4.1.

**Exercise 4.4.** Prove that for $\gamma_1 = 0$ and any $\gamma_2 > 0$, the bound $d_{\gamma_2}(b, b') \le c(b, b') + \gamma_2 |d(b, b')|$ is tight. Find a transition where equality holds.

**Exercise 4.5.** Give an explicit example of a system where the $\gamma = 0$ topology differs from the $\gamma = 1$ topology. (Hint: consider a state space where $|d|$ is unbounded relative to $c$.)

**Exercise 4.6 (Discussion).** The interpretation of $\gamma$ as "debt sensitivity" (Remark 4.4.3) is a modeling choice, not a theorem. Is this interpretation reasonable? Give an example of a system where $\gamma$ has a natural architectural meaning.

**Exercise 4.7.** Consider two paths from $b$ to $b'$: $P_1$ has total cost $1$ and total debt $10$; $P_2$ has total cost $5$ and total debt $1$. For what values of $\gamma$ is $P_1$ preferred? For what values is $P_2$ preferred? Compute the threshold $\gamma^*$.

**Exercise 4.8.** Verify the modulus-sup bound (Proposition 4.5.1) for $z = 3 + 4i$. Compute $|z|$ and $\sqrt{2} \max(|c|, |d|)$, and verify the inequality.

**Exercise 4.9.** Prove that the bound in Proposition 4.5.1 is tight by finding a $z \in \mathbb{C}$ where $|z| = \sqrt{2} \max(|c|, |d|)$.

**Exercise 4.10.** For the Bellman operator with $d_\gamma$-modulus, compute the contraction modulus explicitly for $\gamma = 0.5$ and $\gamma = 0.9$. Show that the modulus is less than $1$ for both, but the contraction is weaker for larger $\gamma$.

**Exercise 4.11.** Show that the phase loss at $\gamma = 1$ (Proposition 4.6.2) does not occur at $\gamma = 0$. That is, at $\gamma = 0$, the metric $d_0 = c$ distinguishes between transitions with different costs, regardless of their phases.

**Exercise 4.12 (Discussion).** The framework emphasizes $\gamma = 1$ as the canonical case. But the metric topology is the same for all $\gamma > 0$ (Corollary 4.2.2). What is the point of the $\gamma$-family, if the topology is the same? Discuss.

**Exercise 4.13 (Open).** Is the contraction threshold $\gamma < 1/\sqrt{2}$ sharp? Construct a cMDP where the Bellman operator fails to contract for $\gamma = 1/\sqrt{2}$, or prove that it contracts for some $\gamma > 1/\sqrt{2}$.

**Exercise 4.14 (Open).** The $\gamma$-family interpolates between $d_0 = c$ and $d_1 = |Q|$. Are there natural intermediate values of $\gamma$ that correspond to specific system architectures? Give examples.

**Exercise 4.15 (Open).** The $\gamma$-family is parameterized by a single scalar $\gamma$. Can the framework be generalized to a multi-parameter family, e.g., with different weights for the real and imaginary axes of the complex plane? What would the resulting geometry look like?
