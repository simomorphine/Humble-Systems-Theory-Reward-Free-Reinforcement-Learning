# Part IV — Equilibrium Theory

---

# Chapter 11 — Fixed Points and Their Existence



## 11.1 The fixed-point problem

Parts II and III developed the geometry and the learning theory. This part studies the equilibrium structure: what fixed points exist, whether they are unique, and what their properties are.

**Definition 11.1.1 (Fixed point of the complex Bellman operator).** A function $Q^\* \in \mathcal{Q}$ is a *fixed point* of the Bellman optimality operator $T$ if

$$TQ^\* = Q^\*,$$

i.e. if for all $(b, a)$,

$$Q^\*(b, a) = \mathbb{E}_{b' \sim p(\cdot \mid b, a)}\left[z(b, a, b') + \lambda \, Q^\*(b', \pi_{Q^\*}(b'))\right].$$

**Definition 11.1.2 (Fixed point of the two-selector operator).** A pair $(Q^{\*+}, Q^{\*-}) \in \mathcal{Q} \times \mathcal{Q}$ is a *fixed point of* $T_{\rightarrow\leftarrow}$ if

$$T_{\rightarrow\leftarrow}(Q^{\*+}, Q^{\*-}) = (Q^{\*+}, Q^{\*-}).$$

**Definition 11.1.3 (Epistemic equilibrium).** A pair $(Q^{\*+}, Q^{\*-})$ is in *epistemic equilibrium* if it is a fixed point of $T_{\rightarrow\leftarrow}$ and $Q^{\*+} = Q^{\*-}$.

**Problem 11.1.4 (Existence).** Under what conditions does $T$ (or $T_{\rightarrow\leftarrow}$) have a fixed point in $\mathcal{Q}$ (or $\mathcal{Q} \times \mathcal{Q}$)?

**Problem 11.1.5 (Uniqueness).** If a fixed point exists, is it unique?

**Problem 11.1.6 (Structure).** What is the structure of the fixed-point set when it is not a singleton?

**Remark 11.1.7 (Dependence on OP1).** The existence and uniqueness questions are closely tied to the contraction question (OP1). If $T$ is a contraction, existence and uniqueness follow from Banach. If $T$ is not a contraction, existence may still be established by other means (Schauder, monotonicity, etc.), but uniqueness is not guaranteed.

## 11.2 Existence via Banach

The cleanest existence result uses the Banach fixed-point theorem, which requires contraction.

**Theorem 11.2.1 (Existence under contraction).** If $T$ is a $\lambda$-contraction on $(\mathcal{Q}, \|\cdot\|_\infty)$ for some $\lambda < 1$, then $T$ has a unique fixed point in $\mathcal{Q}$.

*Proof.* Banach fixed-point theorem. $\square$

**Corollary 11.2.2 (Evaluation).** The evaluation operator $T^\pi$ is a $\lambda$-contraction and has a unique fixed point $Q^\pi$ for every $\pi$.

*Proof.* Theorem 7.2.3 and Banach. $\square$

**Corollary 11.2.3 (Optimality, conditional).** If Conjecture 8.4.5 holds — that $T$ is a $\lambda$-contraction — then $T$ has a unique fixed point in $\mathcal{Q}$, and this fixed point is the optimal value function.

*Proof.* Theorem 11.2.1 applied to $T$. $\square$

**Remark 11.2.4 (The existence problem is equivalent to the contraction problem).** For the value-based optimality theory, existence of a unique fixed point follows from OP1. The framework's existence result is therefore conditional on the resolution of the contraction question. This is one of the reasons OP1 is the framework's central open problem: it is not only about convergence of value iteration, but also about existence of the optimal value function.

## 11.3 Existence via Schauder

If $T$ is not a contraction but is continuous on a compact convex set, existence can be established via Schauder's theorem without uniqueness.

**Theorem 11.3.1 (Schauder fixed-point theorem).** Let $K$ be a non-empty, compact, convex subset of a Banach space, and let $T : K \to K$ be continuous. Then $T$ has a fixed point in $K$.

**Proposition 11.3.2 (Compactness of $\mathcal{Q}$ in the weak topology).** The unit ball of $\mathcal{Q}$ is weakly compact if $\mathcal{Q}$ is reflexive. The space $\mathcal{Q} = \mathcal{B}(\mathcal{B} \times \mathcal{A}, \mathbb{C})$ is reflexive if $\mathcal{B} \times \mathcal{A}$ is a finite set.

*Proof.* Finite-dimensional complex Banach spaces are reflexive. $\square$

**Proposition 11.3.3 (Continuity of $T$ on a finite cMDP).** If $\mathcal{B}$ and $\mathcal{A}$ are finite, then $T : \mathcal{Q} \to \mathcal{Q}$ is continuous in the norm topology away from the tie set $\mathcal{T} = \lbrace Q : \exists b, a \neq a' \text{ with } |Q(b, a)| = |Q(b, a')|\rbrace$, and its restriction to the complement of $\mathcal{T}$ is Lipschitz with constant $\lambda$.

*Proof.* On the complement of the tie set, the selector $\pi_Q$ is locally constant, so $T$ is locally an evaluation operator, which is $\lambda$-Lipschitz. $\square$

**Theorem 11.3.4 (Existence for finite cMDPs).** If $\mathcal{B}$ and $\mathcal{A}$ are finite, then $T$ has at least one fixed point in $\mathcal{Q}$.

*Proof.* Consider a smoothed version $T_\tau$ of $T$ obtained by replacing the hard selector with a soft selector of temperature $\tau > 0$:

$$\pi_{\tau, Q}(a \mid b) = \frac{\exp(-|Q(b, a)| / \tau)}{\sum_{a' \in \mathcal{A}} \exp(-|Q(b, a')| / \tau)}.$$

For each $\tau > 0$, $T_\tau$ is continuous on $\mathcal{Q}$ (as a composition of continuous maps) and maps a sufficiently large closed ball $\overline{B(0, R)}$ into itself, where $R = Z_{\max}/(1-\lambda)$. By Schauder's theorem, $T_\tau$ has a fixed point $Q_\tau^\*$ in $\overline{B(0, R)}$. As $\tau \to 0$, the sequence $\lbrace Q_\tau^\*\rbrace$ is bounded and hence has a convergent subsequence (by finite-dimensionality of $\mathcal{Q}$). Any limit point $Q^\*$ of such a subsequence satisfies $TQ^\* = Q^\*$ by continuity of $T$ on the complement of the tie set and by the limiting behavior of the soft selector. $\square$

**Remark 11.3.5 (Existence but not uniqueness).** Theorem 11.3.4 establishes existence but not uniqueness. The fixed-point set may be a singleton or a manifold. For finite cMDPs, the smoothed version $T_\tau$ has a unique fixed point for each $\tau > 0$ (by Banach, since $T_\tau$ is a contraction for suitable $\tau$). If the limit as $\tau \to 0$ is independent of the choice of subsequence, the fixed point of $T$ is unique. Whether the limit is subsequence-independent is not established.

**Remark 11.3.6 (The existence result is robust).** The Schauder argument does not require the hard selector to be continuous; it requires only that a smoothed version be continuous and that the limit be a fixed point. This is a standard technique in fixed-point theory and is applicable here because the state and action spaces are finite.

## 11.4 Uniqueness

**Proposition 11.4.1 (Uniqueness in the real case).** If $d \equiv 0$, then $T$ reduces to the classical real Bellman optimality operator, which has a unique fixed point.

*Proof.* Standard. $\square$

**Proposition 11.4.2 (Uniqueness under phase-cone restriction).** If $T$ is a contraction on a phase cone $C_\theta$ (Proposition 8.6.2) and the fixed point lies in $C_\theta$, then $T$ has a unique fixed point in $C_\theta$.

*Proof.* Banach fixed-point theorem applied to $T$ restricted to $C_\theta$. $\square$

**Problem 11.4.3 (Uniqueness in general).** Does $T$ have a unique fixed point in $\mathcal{Q}$? This is open.

**Remark 11.4.4 (Why uniqueness is hard).** The smoothed-operator argument (Theorem 11.3.4) gives existence but not uniqueness. If the limit as $\tau \to 0$ depends on the choice of subsequence, uniqueness fails. Whether the limit is subsequence-independent is not established. A proof of uniqueness would need either a contraction argument (which is OP1) or a monotonicity argument, neither of which is currently available.

**Conjecture 11.4.5 (Uniqueness conjecture).** If $T$ has a fixed point $Q^\*$ with $\mathrm{Re} Q^\* \ge 0$ and $\mathrm{Im} Q^\* \ge 0$ (first quadrant), then $Q^\*$ is unique in $\mathcal{Q}$.

**Remark 11.4.6 (Motivation for the conjecture).** The first-quadrant restriction holds at any fixed point under the submartingale condition (Corollary 8.5.3). The conjecture is that this restriction, combined with the structure of the Bellman equation, forces uniqueness. The intuition is that the phase-loss obstruction (Chapter 8) is what allows multiple fixed points, and if the phase is constrained to the first quadrant, the obstruction weakens.

## 11.5 The fixed-point set

When the fixed point is not unique, its structure is of interest.

**Definition 11.5.1 (Fixed-point set).** The *fixed-point set* of $T$ is

$$\mathcal{F} = \lbrace Q \in \mathcal{Q} : TQ = Q\rbrace$$

**Proposition 11.5.2 (Closedness).** If $T$ is continuous, then $\mathcal{F}$ is closed in $(\mathcal{Q}, \|\cdot\|_\infty)$.

*Proof.* $\mathcal{F} = (T - I)^{-1}(\{0\})$, and the preimage of a closed set under a continuous map is closed. $\square$

**Proposition 11.5.3 (Convexity in the real case).** If $d \equiv 0$ and $T$ is the classical real Bellman operator, then $\mathcal{F}$ is a singleton.

*Proof.* Uniqueness in the classical case. $\square$

**Proposition 11.5.4 (Structure in the complex case).** In general, $\mathcal{F}$ may be a singleton, a finite set, a manifold, or a more complicated set. The structure depends on the specific cMDP.

**Problem 11.5.5 (Structure of the fixed-point set).** Characterize $\mathcal{F}$ for cMDPs with potential-difference debt. Under what conditions is $\mathcal{F}$ a singleton? A manifold? Discrete?

**Remark 11.5.6 (Connection to OP1).** If $T$ is a contraction, $\mathcal{F}$ is a singleton (Banach). If $T$ is not a contraction but has a fixed point, $\mathcal{F}$ may have more structure. The structure of $\mathcal{F}$ is therefore a finer question than uniqueness alone, and it may be more tractable in some cases.

## 11.6 The Lyapunov candidate at the fixed point

The Lyapunov candidate $\mathcal{L}(b, a) = |Q^*(b, a)|^2$ has properties that depend on the fixed-point structure.

**Proposition 11.6.1 (Non-negativity).** $\mathcal{L}(b, a) \ge 0$ for all $(b, a)$.

*Proof.* The squared modulus is non-negative. $\square$

**Proposition 11.6.2 (Decomposition).** $\mathcal{L}(b, a) = Q_R^*(b, a)^2 + Q_I^*(b, a)^2$.

*Proof.* $|z|^2 = (\operatorname{Re} z)^2 + (\operatorname{Im} z)^2$. $\square$

**Proposition 11.6.3 (Upper bound).** $\mathcal{L}(b, a) \le \left(Z_{\max}/(1-\lambda)\right)^2$.

*Proof.* $|Q^*(b, a)| \le Z_{\max}/(1-\lambda)$ by Corollary 7.2.5. $\square$

**Proposition 11.6.4 (Epistemic component).** Under the submartingale condition, $\mathcal{L}_I(b, a) = Q_I^*(b, a)^2 \ge 0$.

*Proof.* $Q_I^* \ge 0$ by Proposition 8.5.1. $\square$

**Remark 11.6.5 (The Lyapunov candidate is not automatically a Lyapunov function).** The properties above establish that $\mathcal{L}$ is non-negative, bounded, and decomposes into cost and epistemic components. Whether it *decreases* along trajectories is a separate question, addressed in Chapter 12.

## 11.7 Summary

Fixed-point existence and uniqueness for the complex Bellman optimality operator $T$ are open problems in general.

**Two positive results are available:**

- Under contraction (Conjecture 8.4.5), existence and uniqueness follow from Banach (Theorem 11.2.1). The contraction conjecture is open.
- For finite cMDPs, existence follows from Schauder applied to a smoothed version of $T$ and taking a limit (Theorem 11.3.4). Uniqueness is not established by this argument.

**The fixed-point set $\mathcal{F}$** is closed under continuity of $T$. Its structure — singleton, manifold, or more complicated — depends on the specific cMDP and is not characterized in general (Problem 11.5.5).

**The Lyapunov candidate** $|Q^*|^2$ is non-negative, decomposes into real and imaginary parts, and is bounded by $(Z_{\max}/(1-\lambda))^2$. Whether it decreases along trajectories is the subject of Chapter 12.

**The first-quadrant restriction** (Corollary 8.5.3) holds at any fixed point under the submartingale condition. It is the structural fact that may lead to a uniqueness proof (Conjecture 11.4.5) or a contraction proof (Conjecture 8.6.5).

## Exercises

**Exercise 11.1.** For a finite cMDP with two states and two actions, compute the fixed point of $T$ directly (by solving the Bellman equation). Verify that it satisfies $TQ^* = Q^*$.

**Exercise 11.2.** Verify the Schauder existence argument (Theorem 11.3.4) for a specific finite cMDP. Compute the smoothed operator $T_\tau$ for $\tau = 1$ and $\tau = 0.1$, and check that the fixed points converge as $\tau \to 0$.

**Exercise 11.3.** Prove that for a finite cMDP, the fixed-point set $\mathcal{F}$ is compact. (Hint: $\mathcal{F}$ is a closed subset of the bounded set $\overline{B(0, Z_{\max}/(1-\lambda))}$.)

**Exercise 11.4.** For a symmetric cMDP ($d \equiv 0$), verify that $T$ has a unique fixed point (the classical case).

**Exercise 11.5.** Verify that for a cMDP with potential-difference debt and a submartingale potential, the fixed point lies in the first quadrant.

**Exercise 11.6.** Consider a cMDP with two fixed points. Construct it explicitly, and compute the Lyapunov candidate $\mathcal{L} = |Q^*|^2$ for both fixed points.

**Exercise 11.7.** Verify Proposition 11.6.3 (upper bound on the Lyapunov candidate) for a specific cMDP.

**Exercise 11.8.** Show that if the Bellman operator has a unique fixed point, then the Lyapunov candidate is the same for all initial conditions.

**Exercise 11.9.** Prove that if the potential is bounded with $|\phi| \le M$, then $\mathcal{L}_I(b, a) \le (2M/(1-\lambda))^2$.

**Exercise 11.10.** For a cMDP with no fixed point (if one exists), compute the value iteration sequence and show that it does not converge.

**Exercise 11.11 (Discussion).** The Schauder existence argument gives existence but not uniqueness. Is uniqueness essential for the framework? What would be lost if the fixed point were not unique?

**Exercise 11.12 (Discussion).** The uniqueness conjecture (11.4.5) restricts the fixed point to the first quadrant. Is this reasonable? Give an example where the first-quadrant restriction might fail.

**Exercise 11.13 (Open).** Prove or disprove the uniqueness conjecture (11.4.5). If the conjecture is true, prove it. If false, construct a counterexample.

**Exercise 11.14 (Open).** Characterize the structure of the fixed-point set $\mathcal{F}$ for a general cMDP. Under what conditions is $\mathcal{F}$ a singleton? A manifold? Discrete?

**Exercise 11.15 (Open).** The Schauder existence argument uses a smoothed version of $T$. Does the limit as $\tau \to 0$ depend on the choice of the smoothing family? If so, does this imply non-uniqueness of the fixed point?

**Exercise 11.16 (Open).** For a cMDP with potential-difference debt, does the fixed point depend on the potential $\phi$? If so, how? If not, why?

**Exercise 11.17 (Open).** The Lyapunov candidate $\mathcal{L} = |Q^*|^2$ is bounded and non-negative. Is it strictly positive away from the fixed point? (This is a necessary condition for $\mathcal{L}$ to be a Lyapunov function.)
