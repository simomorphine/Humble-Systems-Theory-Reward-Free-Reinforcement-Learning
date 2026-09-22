# Part III — Reinforcement Learning

---

# Chapter 7 — The Complex Bellman Equation

*(Revised with exercises)*

## 7.1 The setting

**Definition 7.1.1 (Complex Markov decision process).** A *complex Markov decision process* (cMDP) is a tuple
$$\mathcal{M} = (\mathcal{B}, \mathcal{A}, p, z, \lambda),$$
where:

- $\mathcal{B}$ is a belief space (Definition 2.1.1).
- $\mathcal{A}$ is a finite action space.
- $p : \mathcal{B} \times \mathcal{A} \to \Delta(\mathcal{B})$ is a transition kernel, written $p(b' \mid b, a)$.
- $z : \mathcal{B} \times \mathcal{A} \times \mathcal{B} \to \mathbb{C}$ is a complex utility of the form $z(b, a, b') = c(b, a, b') + i \, d(b, a, b')$.
- $\lambda \in [0, 1)$ is a discount factor.

**Assumption 7.1.2 (Bounded utility).** $|z(b, a, b')| \le Z_{\max} < \infty$ for all $(b, a, b')$.

**Definition 7.1.3 (Complex return).** For a policy $\pi$ and initial state-action $(b, a)$, the *complex return* is

$$G_t = \sum_{k=0}^\infty \lambda^k \, z(B_{t+k}, A_{t+k}, B_{t+k+1}), \qquad A_{t+k} \sim \pi(\cdot \mid B_{t+k}).$$

**Definition 7.1.4 (Complex action-value function).** The *complex action-value function* under $\pi$ is

$$Q^\pi(b, a) = \mathbb{E}^\pi[G_t \mid B_t = b, A_t = a].$$

**Definition 7.1.5 (Complex state-value function).** The *complex state-value function* under $\pi$ is

$$V^\pi(b) = \mathbb{E}^\pi[G_t \mid B_t = b].$$

**Proposition 7.1.6 (Absolute convergence).** Under Assumption 7.1.2, the complex return converges absolutely:

$$\mathbb{E}^\pi[|G_t| \mid B_t = b, A_t = a] \le \frac{Z_{\max}}{1 - \lambda}.$$

*Proof.* $|G_t| \le \sum_k \lambda^k |z(B_{t+k}, A_{t+k}, B_{t+k+1})| \le Z_{\max} \sum_k \lambda^k = Z_{\max}/(1-\lambda)$. Take expectations. $\square$

**Definition 7.1.7 (Function space).** Let $\mathcal{Q} = \mathcal{B}(\mathcal{B} \times \mathcal{A}, \mathbb{C})$ be the Banach space of bounded complex-valued functions on $\mathcal{B} \times \mathcal{A}$, equipped with the sup-norm

$$\|Q\|_\infty = \sup_{(b, a) \in \mathcal{B} \times \mathcal{A}} |Q(b, a)|.$$

**Remark 7.1.8 (Complex vs. real Banach space).** The space $\mathcal{Q}$ is a complex Banach space, but it is also a real Banach space when scalar multiplication is restricted to $\mathbb{R}$. In this book, $\mathcal{Q}$ is treated as a complex Banach space; the sup-norm is the standard one. Completeness of $\mathcal{Q}$ under the sup-norm is standard.

## 7.2 The evaluation operator

**Definition 7.2.1 (Evaluation operator).** For a deterministic policy $\pi : \mathcal{B} \to \mathcal{A}$, the *evaluation operator* $T^\pi : \mathcal{Q} \to \mathcal{Q}$ is

$$(T^\pi Q)(b, a) = \mathbb{E}_{b' \sim p(\cdot \mid b, a)}\left[z(b, a, b') + \lambda \, Q(b', \pi(b'))\right].$$

**Proposition 7.2.2 (Well-definedness).** $T^\pi$ maps $\mathcal{Q}$ into itself.

*Proof.* For $Q \in \mathcal{Q}$ with $\|Q\|_\infty < \infty$:

$$|(T^\pi Q)(b, a)| \le \mathbb{E}_{b'}[|z(b, a, b')| + \lambda |Q(b', \pi(b'))|] \le Z_{\max} + \lambda \|Q\|_\infty < \infty. \qquad \square$$

**Theorem 7.2.3 (Evaluation contraction).** $T^\pi$ is a $\lambda$-contraction on $(\mathcal{Q}, \|\cdot\|_\infty)$.

*Proof.* For $Q_1, Q_2 \in \mathcal{Q}$ and any $(b, a)$:

$$|(T^\pi Q_1)(b, a) - (T^\pi Q_2)(b, a)| = \left|\mathbb{E}_{b'}\left[\lambda Q_1(b', \pi(b')) - \lambda Q_2(b', \pi(b'))\right]\right| \le \lambda \, \mathbb{E}_{b'}\left[|Q_1(b', \pi(b')) - Q_2(b', \pi(b'))|\right] \le \lambda \, \|Q_1 - Q_2\|_\infty.$$

The first inequality uses the modulus of expectation (Proposition 2.3.2); the second uses the definition of the sup-norm. Taking the supremum over $(b, a)$ gives the contraction. $\square$

**Corollary 7.2.4 (Existence and uniqueness).** For any deterministic policy $\pi$, there exists a unique $Q^\pi \in \mathcal{Q}$ satisfying $T^\pi Q^\pi = Q^\pi$, and $Q^\pi = \lim_{n \to \infty} (T^\pi)^n Q_0$ for any $Q_0 \in \mathcal{Q}$.

*Proof.* Banach fixed-point theorem applied to $T^\pi$ on the complete space $(\mathcal{Q}, \|\cdot\|_\infty)$. $\square$

**Corollary 7.2.5 (Bound on the fixed point).** $\mid Q^\pi \mid_\infty \le Z_{\max}/(1-\lambda)$.

*Proof.* $|Q^\pi(b, a)| = |T^\pi Q^\pi(b, a)| \le Z_{\max} + \lambda \|Q^\pi\|_\infty$. Rearranging gives the bound. $\square$

**Remark 7.2.6 (Evaluation is not where the difficulty lies).** The proof of Theorem 7.2.3 is identical to the proof of the classical real-valued evaluation contraction. The complex structure does not complicate the proof; it uses only the triangle inequality for the modulus and the fact that the transition kernel is a probability measure. The difficulty of the complex framework is entirely in the optimality problem (Chapter 8), where the policy depends on the complex value and the absence of a total order on $\mathbb{C}$ becomes relevant.

## 7.3 Component decomposition

The evaluation equation decouples in the real and imaginary parts.

**Proposition 7.3.1 (Component Bellman equations).** $Q^\pi = Q_R^\pi + i \, Q_I^\pi$, where
$$Q_R^\pi(b, a) = \mathbb{E}_{b'}[c(b, a, b') + \lambda \, Q_R^\pi(b', \pi(b'))],$$
$$Q_I^\pi(b, a) = \mathbb{E}_{b'}[d(b, a, b') + \lambda \, Q_I^\pi(b', \pi(b'))].$$

*Proof.* Taking real and imaginary parts of the complex Bellman equation. The transition kernel $p$ is real, so the real and imaginary parts do not mix. $\square$

**Corollary 7.3.2 (Independent evaluation).** $Q_R^\pi$ and $Q_I^\pi$ can be computed independently. The evaluation problem decomposes into two real-valued Bellman equations.

**Corollary 7.3.3 (Closed form for $Q_I^\pi$).** If $d$ takes the potential-difference form $d(b, a, b') = \phi(b') - \phi(b)$, then $Q_I^\pi$ has the closed form
$$Q_I^\pi(b, a) = -\phi(b) + (1 - \lambda) \, \mathbb{E}^\pi\left[\sum_{k=0}^\infty \lambda^k \, \phi(B_{t+k+1}) \,\middle|\, B_t = b, A_t = a\right],$$
by Theorem 3.1.3.

*Proof.* Theorem 3.1.3 applies directly to the imaginary component. $\square$

**Remark 7.3.4 (Evaluation is decoupled; optimization is not).** In the evaluation of a fixed policy, the real and imaginary components decouple. In the optimization problem (Chapter 8), they couple through the modulus-greedy selector: the choice of action depends on the modulus $\sqrt{Q_R^2 + Q_I^2}$, which mixes the two components. This coupling is the source of every technical difficulty in the optimality analysis.

## 7.4 Relationship to the classical case

**Proposition 7.4.1 (Real case is a special case).** If $d \equiv 0$, then $Q^\pi = Q_R^\pi$ is real and the complex Bellman equation reduces to the classical real-valued Bellman equation.

*Proof.* Immediate from the component equations. $\square$

**Proposition 7.4.2 (No order structure required for evaluation).** The proof of Theorem 7.2.3 does not use any order structure on $\mathbb{C}$; it uses only the triangle inequality and the completeness of $\mathbb{C}$ as a Banach space.

*Proof.* The proof of Theorem 7.2.3 is exactly the argument of its real-valued counterpart, with $|\cdot|$ denoting the complex modulus. No use is made of an order on $\mathbb{C}$. $\square$

**Remark 7.4.3 (Why evaluation is easy).** The evaluation operator is a *linear* operator (for fixed policy $\pi$), and the contraction proof uses only linearity and the properties of the norm. Nonlinearity enters only in the optimality operator, where the selector $\pi_Q$ is a nonlinear function of $Q$. This is why the optimality problem is harder: the selector destroys the linearity that makes evaluation tractable.

## 7.5 Policy evaluation: examples

**Example 7.5.1 (Symmetric cMDP).** Suppose the cMDP is symmetric: $c(b, b') = c(b', b)$ and $d(b, b') = -d(b', b)$ for all $b, b'$. Then $Q_R^\pi$ is the classical discounted cost, and $Q_I^\pi$ is the discounted potential difference, which telescopes to zero along closed trajectories and is bounded by the potential range along open trajectories.

**Example 7.5.2 (Asymmetric cMDP with potential-difference debt).** The real part $Q_R^\pi$ is the discounted cumulative cost under $\pi$. The imaginary part $Q_I^\pi$ is the discounted cumulative potential difference, which by Theorem 3.1.3 equals $\bar{\phi}^\pi(b, a) - \phi(b)$. Under the submartingale condition, both are non-negative.

**Example 7.5.3 (Zero-debt cMDP).** If $d \equiv 0$, the cMDP reduces to a classical MDP with cost $c$. The complex machinery is unnecessary in this case, and the framework reduces to standard value-based RL.

**Example 7.5.4 (Two-state cMDP with explicit computation).** Let $\mathcal{B} = \{b_0, b_1\}$, $\mathcal{A} = \{a_0\}$ (single action). Transitions: $p(b_1 \mid b_0, a_0) = 1$, $p(b_0 \mid b_1, a_0) = 1$. Utilities: $z(b_0, a_0, b_1) = 1 + 2i$, $z(b_1, a_0, b_0) = 1 - 2i$. Discount $\lambda = 1/2$.

Evaluate under the deterministic policy $\pi(b) = a_0$. The complex Q-values satisfy
$$Q(b_0, a_0) = (1 + 2i) + \tfrac{1}{2} Q(b_1, a_0),$$
$$Q(b_1, a_0) = (1 - 2i) + \tfrac{1}{2} Q(b_0, a_0).$$

Solving: substituting the second into the first gives
$$Q(b_0, a_0) = (1 + 2i) + \tfrac{1}{2}\left[(1 - 2i) + \tfrac{1}{2} Q(b_0, a_0)\right] = \tfrac{3}{2} + i + \tfrac{1}{4} Q(b_0, a_0).$$
Hence $Q(b_0, a_0) = \frac{3/2 + i}{3/4} = 2 + \frac{4}{3}i$. Similarly, $Q(b_1, a_0) = 2 - \frac{4}{3}i$.

The real parts are equal (both $2$), as are the moduli (both $\sqrt{4 + 16/9} = \sqrt{52}/3 \approx 2.40$). The imaginary parts are opposite. This is the framework's asymmetry at the level of the Q-values: at $b_0$, the imaginary part is positive (debt accumulated in expectation); at $b_1$, it is negative.

## 7.6 Summary

A complex Markov decision process is a classical MDP whose utility is complex-valued. The utility decomposes into a real cost $c \ge 0$ and a real debt $d$, and the debt takes the potential-difference form when there exists a potential $\phi$ with $d(b, a, b') = \phi(b') - \phi(b)$.

The evaluation operator $T^\pi$ is a $\lambda$-contraction on the Banach space of bounded complex functions with the sup-norm. Its fixed point $Q^\pi$ exists, is unique, and is the limit of value iteration. The evaluation equation decomposes into independent Bellman equations for the real and imaginary parts.

The evaluation problem is not where the framework's difficulty lies. The contraction proof is identical to the classical case, and the complex structure does not introduce any new obstacles. The difficulty is in the optimality problem, where the choice of policy depends on the complex value and the absence of a total order on $\mathbb{C}$ becomes relevant.

This chapter establishes the basic objects of the complex RL framework: the cMDP, the complex value functions, the evaluation operator, and the evaluation contraction. The next chapter turns to the optimality operator and the gap that remains open.

## Exercises

**Exercise 7.1.** Define a cMDP with two states, two actions, and specific utilities and transitions. Compute $Q^\pi$ for a specific deterministic policy $\pi$.

**Exercise 7.2.** Verify the evaluation contraction (Theorem 7.2.3) for the cMDP of Exercise 7.1. Choose $Q_1, Q_2 \in \mathcal{Q}$ and check the contraction inequality.

**Exercise 7.3.** Compute the bound $Z_{\max}/(1-\lambda)$ for the cMDP of Exercise 7.1 with $\lambda = 0.9$. Is the actual fixed point close to this bound? If not, why not?

**Exercise 7.4.** Verify the component decomposition (Proposition 7.3.1) for the cMDP of Exercise 7.1. Compute $Q_R^\pi$ and $Q_I^\pi$ separately and verify that $Q^\pi = Q_R^\pi + i Q_I^\pi$.

**Exercise 7.5.** For a cMDP with potential-difference debt, verify the closed form (Corollary 7.3.3) for $Q_I^\pi$ in a simple case.

**Exercise 7.6.** Prove that if $d \equiv 0$, then $Q^\pi$ is real and the evaluation problem reduces to the classical case.

**Exercise 7.7.** Let $z(b, a, b') = 1$ for all $(b, a, b')$. Compute $Q^\pi(b, a)$ for any policy $\pi$. (This is the constant-utility case.)

**Exercise 7.8.** Let $z(b, a, b') = i$ for all $(b, a, b')$. Compute $Q^\pi(b, a)$ for any policy $\pi$. What is the modulus? The argument?

**Exercise 7.9.** For the two-state cMDP of Example 7.5.4, compute the value iteration sequence $Q_0, Q_1, Q_2, \ldots$ starting from $Q_0 = 0$. Verify that it converges to $Q^\pi = (2 + 4i/3, 2 - 4i/3)$.

**Exercise 7.10.** Compute the convergence rate of the value iteration in Exercise 7.9. How many iterations are needed for $\|Q_n - Q^\pi\|_\infty < 0.01$?

**Exercise 7.11.** Prove that the evaluation operator $T^\pi$ is Lipschitz in $\lambda$: for any fixed $Q \in \mathcal{Q}$ and any $\lambda_1, \lambda_2 \in [0, 1)$,
$$\|T^\pi_{\lambda_1} Q - T^\pi_{\lambda_2} Q\|_\infty \le |\lambda_1 - \lambda_2| \cdot \|Q\|_\infty.$$

**Exercise 7.12.** Show that the component Bellman equations for $Q_R^\pi$ and $Q_I^\pi$ are independent: the solution for $Q_R^\pi$ does not depend on the debt $d$, and the solution for $Q_I^\pi$ does not depend on the cost $c$.

**Exercise 7.13.** Verify that the modulus $\|Q^\pi\|_\infty$ is bounded by $Z_{\max}/(1-\lambda)$ and that this bound is tight. Construct a cMDP where equality holds.

**Exercise 7.14 (Discussion).** The evaluation operator is linear. Does this mean the evaluation problem is "trivial"? Discuss what "easy" and "hard" mean in the context of value iteration.

**Exercise 7.15 (Open).** The evaluation contraction holds in the sup-norm. Does it hold in other norms — e.g., the $L^2$ norm (with respect to a measure on $\mathcal{B}$)? Under what conditions on the transition kernel and the measure does the contraction hold in $L^2$?

**Exercise 7.16 (Open).** The evaluation operator is a $\lambda$-contraction. Is the contraction modulus $\lambda$ optimal? Can it be improved under additional assumptions on the cMDP (e.g., ergodicity, mixing)?

**Exercise 7.17 (Open).** The evaluation problem decomposes into two independent real Bellman equations. Does the *optimality* problem admit a similar decomposition? If not, why not? (This is essentially the obstruction discussed in Chapter 8.)
