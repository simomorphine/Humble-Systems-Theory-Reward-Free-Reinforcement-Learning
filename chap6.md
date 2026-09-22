# Chapter 6 — Equilibrium Structure

*(Revised with exercises)*

## 6.1 Fixed points revisited

**Definition 6.1.1 (Fixed point of a state).** A state $b^\* \in \mathcal{B}$ is a *fixed point* if

$$Q(b^\*, b^\*) = 0.$$

**Remark 6.1.2 (Local nature of the definition).** The definition is local: it says that a transition from $b^\*$ to $b^\*$ has zero complex cost. It does not say that the state is absorbing, or that the system remains there. It says that, with respect to itself, the state has no cost and no debt.

**Proposition 6.1.3 (Fixed points satisfy the equilibrium condition).** If $b^\*$ is a fixed point and the quasi-metric is continuous at $b^\*$ in $\tau_{\text{avg}}$, then $b^\* \in E_\tau$ for every $\tau \in \{\tau_+, \tau_-, \tau_{\text{avg}}, \tau_+ \vee \tau_-, \tau_+ \wedge \tau_-\}$.

*Proof.* By continuity, for any $\epsilon > 0$ there exists $\delta > 0$ such that $d_{\text{avg}}(b^\*, b') < \delta$ implies $b' \in B_{\text{avg}}(b^\*, \epsilon)$. Since $b^\* \in B_{\text{avg}}(b^\*, \delta)$ for all $\delta > 0$ (as $d_{\text{avg}}(b^\*, b^\*) = 0$), we have $b^* \in U_{\text{pre}}$ and hence $b^* \in \overline{U_{\text{pre}}}^\tau$ for every $\tau$. $\square$

**Remark 6.1.4 (Sufficient conditions for continuity).** The quasi-metric is continuous at $b^\*$ if the cost and debt functions are continuous at $b^\*$ in the relevant topology. This holds in all standard settings (finite state spaces, smooth state spaces with continuous cost functions).

## 6.2 Conditions on the potential

The equilibrium structure depends on the potential $\phi$ through the debt. This section collects the conditions that will be used throughout.

**Definition 6.2.1 (Submartingale condition).** $\phi$ satisfies the *submartingale condition* under the system's dynamics if
$$\mathbb{E}[\phi(B_{t+1}) \mid B_t = b, A_t = a] \ge \phi(b)$$
for all $(b, a)$ and all policies.

**Definition 6.2.2 (Bounded potential).** $\phi$ is *bounded* if $\sup_{b} |\phi(b)| < \infty$.

**Definition 6.2.3 (Lipschitz potential).** $\phi$ is $L$-*Lipschitz* with respect to $d_{\text{avg}}$ if
$$|\phi(b) - \phi(b')| \le L \, d_{\text{avg}}(b, b')$$
for all $b, b'$.

**Proposition 6.2.4 (Submartingale implies non-negative imaginary part).** If $\phi$ satisfies the submartingale condition, then for any policy $\pi$ and any $(b, a)$,
$$Q_I^\pi(b, a) \ge 0.$$

*Proof.* Proposition 3.2.2. $\square$

**Proposition 6.2.5 (Bounded potential gives bounded imaginary part).** If $\phi$ is bounded with $|\phi| \le M$, then
$$|Q_I^\pi(b, a)| \le \frac{2M}{1 - \lambda}$$
for all $(b, a)$.

*Proof.* $Q_I^\pi(b, a) = \bar{\phi}^\pi(b, a) - \phi(b)$, where $\bar{\phi}^\pi$ is the discounted future average (Corollary 3.1.5). Since $|\phi| \le M$, $|\bar{\phi}^\pi| \le M$. Hence $|Q_I^\pi| \le 2M$. For the discounted version: $|Q_I^\pi| = |\sum_{k=0}^\infty \lambda^k d(B_{t+k}, B_{t+k+1})| \le \sum_{k=0}^\infty \lambda^k \cdot 2M = 2M/(1-\lambda)$. $\square$

**Remark 6.2.6 (The bound is conservative).** The bound $2M/(1-\lambda)$ is the same as the bound on $Q_R^\pi$ when $c$ is bounded by $M$. It is conservative in the sense that it is the worst case; in practice the imaginary part may be much smaller.

**Definition 6.2.7 (Phase constraint).** A fixed point $Q^\*$ satisfies the *phase constraint* if $\mathrm{Arg} Q^\*(b, a) \in [0, \pi/2]$ for all $(b, a)$.

**Proposition 6.2.8 (Submartingale implies phase constraint).** Under the submartingale condition, every fixed point $Q^\*$ satisfies the phase constraint.

*Proof.* $Q_I^\*(b, a) \ge 0$ by Proposition 3.2.2. Since $c \ge 0$, the real part $Q_R^\*$ is also non-negative (as the discounted cumulative cost of non-negative costs). Hence $\mathrm{Arg} Q^* \in [0, \pi/2]$. $\square$

## 6.3 Closure properties of equilibrium sets

**Proposition 6.3.1 ($E_\tau$ is closed in $\tau$).** For each topology $\tau$, the equilibrium set $E_\tau$ is closed in $\tau$.

*Proof.* $E_\tau = \overline{U_{\text{pre}}}^{\tau}$ is the closure of a set, hence closed by definition. $\square$

**Proposition 6.3.2 (Monotonicity).** If $\tau_1 \subseteq \tau_2$, then $E_{\tau_2} \subseteq E_{\tau_1}$.

*Proof.* Closure is monotone in the opposite direction: finer topology, smaller closure. $\square$

**Corollary 6.3.3 (Hierarchy restated).** From $\tau_+ \wedge \tau_- \subseteq \tau_{\text{avg}} \subseteq \tau_+ \vee \tau_-$:
$$E_\vee \subseteq E_{\text{avg}} \subseteq E_\wedge.$$

**Proposition 6.3.4 (Non-empty under mild conditions).** If $\mathcal{B}$ is compact in $\tau_+ \vee \tau_-$ and $U_{\text{pre}}$ is non-empty, then $E_\vee$ is non-empty and compact.

*Proof.* $E_\vee = \overline{U_{\text{pre}}}^{\tau_+ \vee \tau_-}$ is a closed subset of a compact space, hence compact and non-empty. $\square$

**Proposition 6.3.5 (Equality conditions).** $E_\vee = E_{\text{avg}}$ if and only if the closure of $U_{\text{pre}}$ in $\tau_+ \vee \tau_-$ equals its closure in $\tau_{\text{avg}}$. This holds, in particular, if $\tau_{\text{avg}} = \tau_+ \vee \tau_-$ on $U_{\text{pre}}$.

*Proof.* Immediate from the definition of $E_\tau$. $\square$

**Remark 6.3.6 (When the hierarchy collapses).** The inclusions $E_\vee \subseteq E_{\text{avg}} \subseteq E_\wedge$ are strict in general. The hierarchy collapses (all three sets equal) when the topologies agree on $U_{\text{pre}}$, which happens when the asymmetry is small enough that the average topology coincides with the join and meet topologies. In the symmetric case ($d_\gamma(b, b') = d_\gamma(b', b)$ for all $b, b'$), the hierarchy collapses to a single equilibrium set. Whether it collapses in the asymmetric case depends on the specifics of the asymmetry; this is an open problem.

## 6.4 Symmetric points and their relationship to equilibrium

**Definition 6.4.1 (Locally symmetric point).** $b \in \mathcal{B}$ is *locally symmetric* if
$$\liminf_{b' \to_{\tau_{\text{avg}}} b} \frac{|d_\gamma(b, b') - d_\gamma(b', b)|}{d_{\text{avg}}(b, b')} = 0.$$
The set of all locally symmetric points is $\operatorname{Sym}_\gamma(\mathcal{B})$.

**Proposition 6.4.2 (Locally symmetric points are in $E_{\text{avg}}$).** If $b \in Sym_\gamma(\mathcal{B})$ and $b$ is a fixed point, then $b \in E_{\text{avg}}$.

*Proof.* Fixed points are in all equilibrium sets (Proposition 6.1.3). $\square$

**Remark 6.4.3 (The converse is open).** The proposition is conditional on being a fixed point. Whether local symmetry implies being a fixed point, or implies membership in some $E_\tau$ without fixed-point structure, is open.

**Proposition 6.4.4 (Global symmetry collapses the hierarchy).** If $d_\gamma$ is globally symmetric, then $\tau_+ = \tau_- = \tau_{\text{avg}} = \tau_+ \vee \tau_- = \tau_+ \wedge \tau_-$, and
$$E_\vee = E_{\text{avg}} = E_\wedge = E_\rightarrow = E_\leftarrow.$$

*Proof.* If $d_\gamma$ is symmetric, forward and backward balls coincide, so $\tau_+ = \tau_-$. All derived topologies coincide. The equilibrium sets are all closures in the same topology, hence equal. $\square$

**Remark 6.4.5 (Symmetry as a special case).** The symmetric case is the special case in which the framework reduces to a single topology and a single equilibrium concept. The framework's distinctive structure (the bitopological hierarchy) is entirely due to asymmetry. This is the framework's central structural claim: that asymmetry is the generic case, and symmetry is the degenerate special case.

## 6.5 Local structure of $E_\tau$

**Definition 6.5.1 (Neighborhood of $E_\tau$).** For $b \in E_\tau$ and $\epsilon > 0$, the *$\epsilon$-neighborhood of $E_\tau$ in $\tau$* is
$$N_\tau(E_\tau, \epsilon) = \{b' \in \mathcal{B} : \exists b \in E_\tau, \, d_\tau(b, b') < \epsilon\},$$
where $d_\tau$ is the metric generating $\tau$ (or, for the join and meet topologies, the appropriate quasi-metric).

**Proposition 6.5.2 (Density of $U_{\text{pre}}$ in $E_\tau$).** $U_{\text{pre}}$ is dense in $E_\tau$ with respect to $\tau$.

*Proof.* $E_\tau = \overline{U_{\text{pre}}}^\tau$. $\square$

**Proposition 6.5.3 (Interior of $E_\tau$).** If $U_{\text{pre}}$ is open in $\tau$, then $E_\tau$ contains $U_{\text{pre}}$ as an open subset.

*Proof.* Immediate. $\square$

**Proposition 6.5.4 (Boundary of $E_\tau$).** The boundary $\partial E_\tau = E_\tau \setminus \operatorname{int}(E_\tau)$ is contained in $E_\tau$ and may be non-empty.

*Proof.* Standard topological fact. The boundary is non-empty if $U_{\text{pre}}$ is not closed. $\square$

**Remark 6.5.5 (Dependence on $\epsilon$).** The local structure of $E_\tau$ depends on the threshold function $\epsilon$ through $U_{\text{pre}}$. Different choices of $\epsilon$ give different equilibrium sets. The framework does not specify $\epsilon$ uniquely; it is a design choice, or a parameter determined by the system's architecture.

## 6.6 Convergence to equilibrium

**Definition 6.6.1 (Convergence).** A trajectory $\{b_t\}_{t \ge 0}$ *converges to $E_\tau$* if, for every $\tau$-open neighborhood $U$ of $E_\tau$, there exists $T$ such that $b_t \in U$ for all $t \ge T$.

**Theorem 6.6.2 (Convergence under Lyapunov contraction).** Suppose there exists a continuous function $V : \mathcal{B} \to \mathbb{R}_{\ge 0}$ and a constant $\kappa \in [0, 1)$ such that
$$V(b_{t+1}) \le \kappa \, V(b_t)$$
along the system's trajectories, and $V(b) = 0$ iff $b \in E_\tau$. Then every trajectory converges to $E_\tau$.

*Proof.* $V(b_t) \le \kappa^t V(b_0) \to 0$. By continuity of $V$, for any $\tau$-neighborhood $U$ of $E_\tau$, there exists $\delta > 0$ such that $V(b) < \delta$ implies $b \in U$. Choose $T$ such that $\kappa^T V(b_0) < \delta$. $\square$

**Proposition 6.6.3 (Lyapunov function candidates).** The function $V(b, a) = |Q^*(b, a)|^2$ for a fixed point $Q^*$ is a candidate Lyapunov function. Whether it is strictly decreasing depends on the policy and the environment.

*Proof.* $V \ge 0$, $V = 0$ iff $Q^* = 0$. Strict decrease requires $\mathbb{E}[|Q^*(B_{t+1}, \cdot)|^2 \mid B_t = b] < |Q^*(b, \cdot)|^2$ for $Q^*(b, \cdot) \neq 0$, which is not automatic. $\square$

**Remark 6.6.4 (The Lyapunov picture).** The Lyapunov picture is the bridge between the static equilibrium theory of this chapter and the dynamic convergence theory of Part IV. The framework provides candidate Lyapunov functions; whether they satisfy the strict decrease condition is a substantive question addressed in Chapter 12.

## 6.7 Summary

The equilibrium structure has three layers.

**The topological layer (Chapter 5):** the five topologies on $\mathcal{B}$ organized by the chain
$$\tau_+ \wedge \tau_- \subseteq \tau_{\text{avg}} \subseteq \tau_+ \vee \tau_-.$$

**The equilibrium layer (this chapter):** the closures $E_\tau$ of the pre-equilibrium set $U_{\text{pre}}$ in each topology. The hierarchy
$$E_\vee \subseteq E_{\text{avg}} \subseteq E_\wedge, \qquad E_\vee \subseteq E_\rightarrow \cap E_\leftarrow$$
follows from the topological chain by the monotonicity of closures.

**The dynamical layer (Chapter 12):** convergence to equilibrium, governed by Lyapunov functions. Under a contraction condition on a Lyapunov function, trajectories converge to $E_\tau$.

Fixed points are in all equilibrium sets. Local symmetry is a weaker condition than global symmetry, and its relationship to equilibrium is subtle. The symmetric case collapses the hierarchy to a single topology and a single equilibrium concept.

This completes Part II. The geometry of complex cost is now in place: the complex quasi-metric, the potential-difference debt, the $\gamma$-family, the bitopological structure, and the equilibrium hierarchy.

## Exercises

**Exercise 6.1.** Verify that the fixed point condition $Q(b^*, b^*) = 0$ is equivalent to $c(b^*, b^*) = 0$ and $d(b^*, b^*) = 0$.

**Exercise 6.2.** Give an example of a system where $b^*$ is a fixed point but not an absorbing state. (Hint: consider a cMDP where $b^*$ has non-trivial outgoing transitions but the net cost of returning to $b^*$ is zero.)

**Exercise 6.3.** Prove that if $\phi$ is bounded with $|\phi| \le M$, then $Q_I^\pi(b, a) \le 2M$ (not $2M/(1-\lambda)$). Where does the extra factor of $1/(1-\lambda)$ come from in the discounted case?

**Exercise 6.4.** Verify Proposition 6.2.8 for a specific cMDP with a submartingale potential. Compute $Q^*$ and check that $\operatorname{Arg} Q^* \in [0, \pi/2]$.

**Exercise 6.5.** For $\mathcal{B} = \{b_1, b_2\}$ with $U_{\text{pre}} = B_{\text{avg}}(b_1, 1) \cup B_{\text{avg}}(b_2, 1)$, compute $E_\tau$ for each topology and verify the hierarchy. You may assume all balls are non-empty and the metric is discrete (each point is isolated).

**Exercise 6.6.** Prove that if $\mathcal{B}$ is finite, then every subset is closed in every topology, and the hierarchy collapses to a single set (all $E_\tau = \mathcal{B}$).

**Exercise 6.7.** Give an example of a system where the equilibrium hierarchy is strict: $E_\vee \subsetneq E_{\text{avg}} \subsetneq E_\wedge$.

**Exercise 6.8.** Verify the equality condition $E_\vee = E_{\text{avg}}$ for a specific symmetric system. Show that the hierarchy collapses.

**Exercise 6.9.** Compute the local asymmetry $\alpha_\gamma(b)$ for a specific asymmetric system and verify Proposition 5.6.2 ($\alpha_\gamma(b) \le 2$).

**Exercise 6.10.** Prove that if $b$ is a locally symmetric point and is an isolated point of $\mathcal{B}$ (under $\tau_{\text{avg}}$), then $b$ is a fixed point.

**Exercise 6.11 (Discussion).** The equilibrium hierarchy has the join topology giving the smallest set. Is this intuitive? Argue for or against the interpretation of $E_\vee$ as the "strictest" equilibrium condition.

**Exercise 6.12.** Prove that if $Q$ is symmetric, then every point is a locally symmetric point.

**Exercise 6.13.** Show that the Lyapunov function candidate $V(b, a) = |Q^*(b, a)|^2$ is bounded by $(Z_{\max}/(1-\lambda))^2$.

**Exercise 6.14.** Construct a cMDP where the Lyapunov function candidate $V = |Q^*|^2$ is strictly decreasing along all trajectories. Compute the contraction factor $\kappa$ explicitly.

**Exercise 6.15.** Construct a cMDP where $V = |Q^*|^2$ is *not* decreasing along some trajectory. Identify the mechanism (phase cancellation, selector switching, etc.).

**Exercise 6.16 (Open).** Under what conditions on the cMDP does the equilibrium hierarchy collapse to a single set? Characterize the cMDPs for which $E_\vee = E_{\text{avg}} = E_\wedge$.

**Exercise 6.17 (Open).** The equilibrium theory uses the closure of the pre-equilibrium set $U_{\text{pre}}$ in various topologies. What is the "right" choice of $U_{\text{pre}}$? Is the threshold function $\epsilon$ arbitrary, or does the framework determine it uniquely?

**Exercise 6.18 (Open).** The convergence theorem (6.6.2) requires a Lyapunov function that is strictly decreasing. Under what conditions does the candidate $V = |Q^*|^2$ satisfy this? This is essentially the same as OP1 (Chapter 8) and is the central open problem of the framework.
