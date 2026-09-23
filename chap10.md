# Chapter 10 — The Complex Policy Gradient Theorem



## 10.1 Parameterized policies

Chapters 7–9 developed the value-based side of the complex framework. This chapter develops the policy-based alternative: the agent maintains a parameterized policy $\pi_\theta$ and adjusts $\theta$ to reduce the complex cost.

**Definition 10.1.1 (Parameterized policy).** A *parameterized policy* is a family $\{\pi_\theta : \theta \in \Theta\}$ of stochastic policies $\pi_\theta : \mathcal{B} \to \Delta(\mathcal{A})$, where $\Theta \subseteq \mathbb{R}^n$ is a parameter space. For each $(b, a)$, the map $\theta \mapsto \pi_\theta(a \mid b)$ is assumed to be differentiable.

**Definition 10.1.2 (Complex expected return).** For an initial state $b_0$, the *complex expected return* is
$$\eta(\theta) = \mathbb{E}^{\pi_\theta}[G_0 \mid B_0 = b_0] \in \mathbb{C},$$
where $G_0$ is the complex return under $\pi_\theta$ (Definition 7.1.3).

**Definition 10.1.3 (Performance objective).** The *performance objective* is
$$J(\theta) = |\eta(\theta)|^2 = \eta(\theta) \overline{\eta(\theta)} \in \mathbb{R}_{\ge 0}.$$

**Remark 10.1.4 (Why the squared modulus).** Minimizing $|\eta|$ and minimizing $|\eta|^2$ are equivalent: both are zero at the same points and have the same directional derivatives up to sign. Working with the squared modulus avoids the non-differentiability of $|\eta|$ at zero, which occurs whenever $\eta = 0$ — a state the agent is trying to reach.

**Remark 10.1.5 (The policy gradient approach bypasses OP1).** The policy gradient method does not require the Bellman optimality operator to be a contraction. It requires only that the complex expected return $\eta(\theta)$ be differentiable in $\theta$, which holds under standard regularity conditions. The policy gradient theorem therefore provides a path to learning in the complex framework that does not depend on the resolution of OP1.

## 10.2 Regularity conditions

**Assumption 10.2.1 (Regularity).** The following hold:

- (i) *Bounded score:* $\|\nabla_\theta \log \pi_\theta(a \mid b)\| \le B < \infty$ for all $(b, a, \theta)$.
- (ii) *Bounded utility:* $|z(b, a, b')| \le Z_{\max} < \infty$ for all $(b, a, b')$.
- (iii) *Differentiability under expectation:* the map $\theta \mapsto \mathbb{E}^{\pi_\theta}[G_0]$ is differentiable, and the derivative can be taken inside the expectation (e.g. by dominated convergence).

**Proposition 10.2.2 (Bounded return).** Under Assumption 10.2.1(ii), $|G_t| \le Z_{\max}/(1-\lambda)$ almost surely.

*Proof.* Proposition 7.1.6. $\square$

## 10.3 The log-derivative identity

The central tool of the policy gradient theorem is the log-derivative identity, also known as the REINFORCE trick.

**Definition 10.3.1 (Trajectory).** A *trajectory* is $\tau = (B_0, A_0, B_1, A_1, \ldots)$. The probability of a length-$T$ prefix under $\pi_\theta$ is
$$\mathbb{P}_\theta(\tau_{0:T}) = \rho(B_0) \prod_{t=0}^{T-1} \pi_\theta(A_t \mid B_t) \, p(B_{t+1} \mid B_t, A_t),$$
where $\rho$ is the initial state distribution.

**Lemma 10.3.2 (Log-derivative identity).** For any $\theta$ and any trajectory $\tau$,
$$\nabla_\theta \log \mathbb{P}_\theta(\tau_{0:T}) = \sum_{t=0}^{T-1} \nabla_\theta \log \pi_\theta(A_t \mid B_t).$$

*Proof.* Taking the logarithm,
$$\log \mathbb{P}_\theta(\tau_{0:T}) = \log \rho(B_0) + \sum_{t=0}^{T-1} \left[\log \pi_\theta(A_t \mid B_t) + \log p(B_{t+1} \mid B_t, A_t)\right].$$
The terms $\log \rho(B_0)$ and $\log p(B_{t+1} \mid B_t, A_t)$ do not depend on $\theta$. Differentiating gives the result. $\square$

**Lemma 10.3.3 (Score function identity).** For any $(b, a)$,
$$\mathbb{E}_{A \sim \pi_\theta(\cdot \mid b)}\left[\nabla_\theta \log \pi_\theta(A \mid b)\right] = 0.$$

*Proof.*
$$\int \nabla_\theta \log \pi_\theta(a \mid b) \, \pi_\theta(a \mid b) \, da = \int \nabla_\theta \pi_\theta(a \mid b) \, da = \nabla_\theta \int \pi_\theta(a \mid b) \, da = \nabla_\theta 1 = 0. \qquad \square$$

**Remark 10.3.4 (Both lemmas are measure-theoretic).** The log-derivative identity and the score function identity depend only on the probability measure, not on the integrand. They apply to complex-valued integrands without modification. This is why the complex policy gradient theorem goes through as smoothly as in the real case.

## 10.4 The complex policy gradient theorem

**Theorem 10.4.1 (Complex policy gradient).** Under Assumption 10.2.1,
$$\nabla_\theta \eta(\theta) = \mathbb{E}^{\pi_\theta}\left[\sum_{t=0}^\infty \lambda^t \, G_t \, \nabla_\theta \log \pi_\theta(A_t \mid B_t) \,\middle|\, B_0 = b_0\right] \in \mathbb{C}^n,$$
where $G_t = \sum_{k=t}^\infty \lambda^{k-t} z(B_k, A_k, B_{k+1})$ is the complex return from time $t$.

*Proof.* Write $\eta(\theta) = \int G_0(\tau) \, d\mathbb{P}_\theta(\tau)$ as an integral over trajectories. Differentiating under the integral (Assumption 10.2.1(iii)):
$$\nabla_\theta \eta(\theta) = \int G_0(\tau) \, \nabla_\theta \log d\mathbb{P}_\theta(\tau) \, d\mathbb{P}_\theta(\tau).$$
By Lemma 10.3.2, $\nabla_\theta \log d\mathbb{P}_\theta(\tau) = \sum_{t=0}^\infty \nabla_\theta \log \pi_\theta(A_t \mid B_t)$. Hence
$$\nabla_\theta \eta(\theta) = \mathbb{E}^{\pi_\theta}\left[G_0(\tau) \sum_{t=0}^\infty \nabla_\theta \log \pi_\theta(A_t \mid B_t)\right].$$
Expand $G_0 = \sum_{k=0}^\infty \lambda^k z_k$. Group terms by $t \leq k$:
$$\nabla_\theta \eta = \sum_{t=0}^\infty \sum_{k \geq t} \lambda^k \mathbb{E}\left[z_k \nabla_\theta \log \pi_\theta(A_t \mid B_t)\right].$$
For fixed $t$, condition on $(B_t, A_t)$. Then $\nabla_\theta \log \pi_\theta(A_t \mid B_t)$ is $(B_t, A_t)$-measurable, and
$$\mathbb{E}\left[\sum_{k \geq t} \lambda^k z_k \,\middle|\, B_t, A_t\right] = \lambda^t G_t(B_t, A_t).$$
Summing over $t$ gives the stated result. $\square$

**Remark 10.4.2 (Comparison to the scalar case).** The proof is formally identical to the classical policy gradient theorem. The complex structure enters only through the integrand $G_t \in \mathbb{C}$. The measure $\mathbb{P}_\theta$ is real, and the log-derivative trick is measure-theoretic. This is the same observation as in Chapter 7 for the evaluation contraction: the complex framework inherits the classical machinery, and the complex structure does not introduce new difficulties at this level.

**Corollary 10.4.3 (Component form).** Writing $\eta = \eta_R + i \eta_I$ and $G_t = G_t^R + i G_t^I$,
$$\nabla_\theta \eta_R = \mathbb{E}^{\pi_\theta}\left[\sum_t \lambda^t G_t^R \nabla_\theta \log \pi_\theta(A_t \mid B_t)\right],$$
$$\nabla_\theta \eta_I = \mathbb{E}^{\pi_\theta}\left[\sum_t \lambda^t G_t^I \nabla_\theta \log \pi_\theta(A_t \mid B_t)\right].$$

## 10.5 Gradient of the performance objective

**Theorem 10.5.1 (Gradient of $|\eta|^2$).** Under Assumption 10.2.1,
$$\nabla_\theta |\eta(\theta)|^2 = 2 \operatorname{Re}\left(\overline{\eta(\theta)} \cdot \nabla_\theta \eta(\theta)\right) \in \mathbb{R}^n,$$
where $\overline{\eta} \cdot \nabla_\theta \eta$ is the complex vector whose $j$-th component is $\overline{\eta(\theta)} \cdot \partial_{\theta_j} \eta(\theta)$.

*Proof.* For each $j$,
$$\partial_{\theta_j} |\eta|^2 = \partial_{\theta_j}(\eta \overline{\eta}) = (\partial_{\theta_j} \eta) \overline{\eta} + \eta \overline{\partial_{\theta_j} \eta} = 2 \operatorname{Re}(\overline{\eta} \cdot \partial_{\theta_j} \eta). \qquad \square$$

**Corollary 10.5.2 (Explicit form).** Substituting Theorem 10.4.1,
$$\nabla_\theta |\eta|^2 = 2 \operatorname{Re}\left(\overline{\eta(\theta)} \cdot \mathbb{E}^{\pi_\theta}\left[\sum_{t=0}^\infty \lambda^t G_t \nabla_\theta \log \pi_\theta(A_t \mid B_t)\right]\right).$$

**Remark 10.5.3 (Real output).** The gradient $\nabla_\theta |\eta|^2$ is a real vector in $\mathbb{R}^n$, appropriate for a descent step on $\theta \in \mathbb{R}^n$. The complex structure enters through the inner product $\overline{\eta} \cdot \nabla_\theta \eta$, which weights the gradient by the conjugate of the current performance.

**Remark 10.5.4 (Automatic step-size adaptation).** When $|\eta|$ is large — the agent is far from equilibrium — the gradient is amplified by the factor $|\eta|$. When $|\eta|$ is small — the agent is near equilibrium — the gradient is damped. This is an automatic step-size adaptation arising from the geometry of $\mathbb{C}$, without an explicit schedule.

## 10.6 Baselines and variance reduction

**Proposition 10.6.1 (Complex baseline).** For any bounded $\mathbb{C}$-valued function $b : \mathcal{B} \to \mathbb{C}$,
$$\mathbb{E}^{\pi_\theta}\left[b(B_t) \cdot \nabla_\theta \log \pi_\theta(A_t \mid B_t)\right] = 0.$$

*Proof.* By Lemma 10.3.3, $\mathbb{E}_{A_t}[\nabla_\theta \log \pi_\theta(A_t \mid B_t) \mid B_t] = 0$. Multiplying by $b(B_t)$ (which is $B_t$-measurable) and taking the full expectation gives the result. $\square$

**Corollary 10.6.2 (Advantage form).** The gradient $\nabla_\theta \eta(\theta)$ is unchanged if $G_t$ is replaced by the complex advantage
$$A^{\pi_\theta}(B_t, A_t) = Q^{\pi_\theta}(B_t, A_t) - V^{\pi_\theta}(B_t) \in \mathbb{C}.$$

**Corollary 10.6.3 (Gradient with advantage).**
$$\nabla_\theta \eta(\theta) = \mathbb{E}^{\pi_\theta}\left[\sum_t \lambda^t A^{\pi_\theta}(B_t, A_t) \nabla_\theta \log \pi_\theta(A_t \mid B_t)\right].$$

**Remark 10.6.4 (Interpretation of the advantage).** The complex advantage has:

- $\operatorname{Re} A^{\pi_\theta}(B_t, A_t)$: the excess real cost of action $A_t$ at state $B_t$, relative to the policy's average cost.
- $\operatorname{Im} A^{\pi_\theta}(B_t, A_t)$: the excess imaginary debt of the action, relative to the policy's average debt.

Under the information-theoretic reading (Assumption 3.3.1), the imaginary advantage is the excess information gain of the action. Positive imaginary advantage means the action is more informative than average; negative means less.

## 10.7 The two channels of the gradient

**Proposition 10.7.1 (Decomposition of the gradient).** The policy gradient decomposes as
$$\nabla_\theta |\eta|^2 = 2 \operatorname{Re}(\overline{\eta}) \cdot \mathbb{E}\left[\sum_t \lambda^t \operatorname{Re} A_t \, \nabla_\theta \log \pi_\theta\right] - 2 \operatorname{Im}(\overline{\eta}) \cdot \mathbb{E}\left[\sum_t \lambda^t \operatorname{Im} A_t \, \nabla_\theta \log \pi_\theta\right].$$

*Proof.* Expand $\operatorname{Re}(\overline{\eta} \cdot A_t) = \operatorname{Re}(\overline{\eta}) \operatorname{Re}(A_t) - \operatorname{Im}(\overline{\eta}) \operatorname{Im}(A_t)$, then distribute the expectation. $\square$

**Corollary 10.7.2 (Two channels).** The gradient has:

- A *cost channel*, weighted by $\operatorname{Re}(\overline{\eta})$, acting on the real part of the advantage.
- A *debt channel*, weighted by $-\operatorname{Im}(\overline{\eta})$, acting on the imaginary part of the advantage.

**Remark 10.7.3 (The debt channel vanishes near equilibrium).** Near equilibrium, $\operatorname{Im}(\overline{\eta}) \to 0$, and the debt channel becomes inactive. The system transitions from a two-channel update (cost and debt) to a single-channel update (cost only). This is the framework's account of the exploration-exploitation transition at the gradient level.

## 10.8 Exploration signal as variance

**Definition 10.8.1 (Exploration signal).** For a policy $\pi_\theta$ and state $b$, the *exploration signal* at $b$ is
$$\mathcal{E}(b) = \operatorname{Var}_{A \sim \pi_\theta(\cdot \mid b)}\left[\operatorname{Im} A^{\pi_\theta}(b, A)\right].$$

**Remark 10.8.2 (The exploration signal is the variance, not the mean).** The imaginary advantage is not non-negative in general. What drives exploration is the *variation* of the imaginary advantage across actions: actions with above-average debt and actions with below-average debt. The variance captures this variation.

**Proposition 10.8.3 (Bounded exploration signal).** $\mathcal{E}(b) \le \left(Z_{\max}/(1-\lambda)\right)^2$ for all $b$.

*Proof.* $\operatorname{Im} A^{\pi_\theta}(b, a) \in [-Z_{\max}/(1-\lambda), Z_{\max}/(1-\lambda)]$. The variance of a random variable bounded by $M$ is at most $M^2$. $\square$

**Proposition 10.8.4 (Exploration signal decays at equilibrium).** If the system converges to equilibrium in the sense that $\operatorname{Im} Q_t^*(b, a) \to 0$ for all $(b, a)$, then $\mathcal{E}(b) \to 0$ for all $b$.

*Proof.* If $\operatorname{Im} Q_t^* \to 0$, then $\operatorname{Im} A_t^* \to 0$, hence $\mathcal{E}_t(b) \to 0$. $\square$

**Remark 10.8.5 (Automatic exploration-exploitation transition).** The exploration signal is bounded and decays to zero at equilibrium. It does not require a schedule; the decay is a consequence of the convergence of the imaginary component of the fixed point. This is the framework's formal account of automatic exploration-exploitation transition.

## 10.9 Natural gradient

**Definition 10.9.1 (Fisher information matrix).** The *Fisher information matrix* of the policy family $\{\pi_\theta\}$ is
$$F(\theta) = \mathbb{E}^{\pi_\theta}\left[\nabla_\theta \log \pi_\theta(A \mid B) \, \nabla_\theta \log \pi_\theta(A \mid B)^\top\right] \in \mathbb{R}^{n \times n}.$$

**Proposition 10.9.2 (Properties of $F$).** $F(\theta)$ is symmetric and positive semi-definite. If the policy family is identifiable, it is positive definite.

*Proof.* Symmetry is immediate. Positive semi-definiteness: for any $v \in \mathbb{R}^n$, $v^\top F v = \mathbb{E}[(v^\top \nabla_\theta \log \pi_\theta)^2] \ge 0$. Strict positivity under identifiability is standard. $\square$

**Remark 10.9.3 (The Fisher matrix is real, not Hermitian).** The parameter $\theta$ is real, so the gradient $\nabla_\theta \log \pi_\theta$ is real, and $F(\theta)$ is a real symmetric matrix. It is not Hermitian in any nontrivial sense. The framework uses real parameters; the Hermitian language would be genuinely complex only for complex parameters, which the framework does not employ.

**Definition 10.9.4 (Natural gradient).** The *natural gradient* of $|\eta|^2$ is
$$\widetilde{\nabla}_\theta |\eta|^2 = F(\theta)^{-1} \nabla_\theta |\eta|^2,$$
with $F(\theta)^{-1}$ replaced by $(F(\theta) + \epsilon I)^{-1}$ for a regularizer $\epsilon > 0$ when $F$ is not invertible.

**Proposition 10.9.5 (Reparameterization invariance).** The natural gradient is invariant to smooth reparameterizations of $\theta$. If $\theta = \phi(\xi)$ for a smooth bijection $\phi$, then the natural gradient with respect to $\xi$ equals the pullback of the natural gradient with respect to $\theta$ under $\phi$.

*Proof.* Standard, using the chain rule and the transformation property of the Fisher information. $\square$

## 10.10 The Complex Natural Actor-Critic

**Algorithm 10.10.1 (CNAC).**

```
Initialize θ ∈ ℝⁿ, ψ, F̂ ← Iₙ, α_θ, α_ψ, ε > 0, β ∈ (0, 1)
for each episode do
    Sample trajectory τ = (b_0, a_0, z_0, b_1, a_1, z_1, …) under π_θ
    for each t do
        G_t ← Σ_{k≥t} λ^{k-t} z_k
        Y_t ← z_t + λ Q_ψ(b_{t+1}, π_θ(b_{t+1}))
    end for
    ψ ← ψ - α_ψ Σ_t ∇_ψ |Q_ψ(b_t, a_t) - Y_t|²
    for each t do
        Â_t ← G_t - Q_ψ(b_t, a_t)
    end for
    η̂ ← Σ_t λ^t z_t
    g ← 2 Re( η̂ · Σ_t λ^t Â_t ∇_θ log π_θ(a_t | b_t) )
    F̂ ← (1 - β) F̂ + β Σ_t ∇_θ log π_θ(a_t | b_t) ∇_θ log π_θ(a_t | b_t)^T
    θ ← θ - α_θ (F̂ + εI)⁻¹ g
end for
```

**Proposition 10.10.2 (Well-definedness).** Under Assumption 10.2.1, each step of the algorithm is well-defined and bounded.

*Proof.* The critic update uses a squared-modulus loss, differentiable under a differentiable critic family. The policy gradient uses the complex advantage, bounded by $2 Z_{\max}/(1-\lambda)$. The Fisher estimate is a convex combination of positive semi-definite matrices. The regularizer ensures invertibility. $\square$

**Remark 10.10.3 (Choice of critic loss).** The critic loss is $|Q_\psi(b, a) - Y|^2$, the squared modulus of the complex TD error. This is the natural loss under the modulus criterion. Alternatives include separate losses for real and imaginary parts, or a Huber loss; the choice affects convergence rate but not the asymptotic properties.

**Remark 10.10.4 (The algorithm is well-defined regardless of OP1).** The CNAC algorithm does not require the Bellman optimality operator to be a contraction. It requires only the evaluation contraction (Chapter 7) for the critic and the policy gradient theorem (this chapter) for the actor. Both are proven. The policy gradient approach therefore provides a path to learning in the complex framework that does not depend on the resolution of OP1.

## 10.11 Summary

**The complex policy gradient theorem (Theorem 10.4.1):** the gradient of the complex expected return is a REINFORCE-style identity with complex returns. The proof is measure-theoretic and does not require complex differentiation.

**The gradient of the squared modulus (Theorem 10.5.1):** $\nabla_\theta |\eta|^2 = 2 \operatorname{Re}(\overline{\eta} \cdot \nabla_\theta \eta)$. The result is a real vector, appropriate for descent on real parameters.

**The complex advantage (Corollary 10.6.3):** the gradient can be written in advantage form. The advantage decomposes into a real part (excess cost) and an imaginary part (excess debt). The imaginary part's variance is the exploration signal.

**The two channels (Proposition 10.7.1):** the gradient decomposes into a cost channel and a debt channel, weighted by the real and imaginary parts of the return. The debt channel vanishes as the return becomes real near equilibrium.

**The exploration signal (Definition 10.8.1):** the variance of the imaginary advantage. Bounded by the return bound and decaying to zero at equilibrium.

**The natural gradient (Definition 10.9.4):** reparameterization-invariant. For real parameters, the Fisher matrix is real symmetric; the Hermitian language is vacuous.

**The CNAC algorithm (Algorithm 10.10.1):** natural gradient actor-critic with automatic exploration. Well-defined regardless of OP1.

The policy gradient theorem and its consequences provide an alternative path to learning in the complex framework that bypasses the optimality problem entirely. This is the framework's practical contribution to reinforcement learning.

## Exercises

**Exercise 10.1.** Verify the log-derivative identity (Lemma 10.3.2) for a specific trajectory in a two-state cMDP with a softmax policy.

**Exercise 10.2.** Verify the score function identity (Lemma 10.3.3) for a softmax policy over two actions. Compute the expected value of $\nabla_\theta \log \pi_\theta(A \mid b)$ over $A \sim \pi_\theta(\cdot \mid b)$.

**Exercise 10.3.** Compute the complex policy gradient (Theorem 10.4.1) for a specific one-step trajectory with a specific policy and utility. Verify the formula by direct computation.

**Exercise 10.4.** Prove the component form (Corollary 10.4.3) by expanding the complex gradient into real and imaginary parts.

**Exercise 10.5.** Verify Theorem 10.5.1 (gradient of $|\eta|^2$) for a specific complex $\eta$ and $\nabla_\theta \eta$. Compute both sides of the identity.

**Exercise 10.6.** Prove the complex baseline proposition (10.6.1) by direct computation.

**Exercise 10.7.** For a specific cMDP, verify that the gradient with advantage (Corollary 10.6.3) equals the gradient without advantage (Theorem 10.4.1). Use a specific baseline $b(b) = V^\pi(b)$ and compute both expressions.

**Exercise 10.8.** Verify the two-channel decomposition (Proposition 10.7.1) for a specific cMDP. Compute both channels and check that they sum to the full gradient.

**Exercise 10.9.** For a policy $\pi_\theta$ and utility $z$, compute the exploration signal $\mathcal{E}(b)$ at a specific state. Verify the bound in Proposition 10.8.3.

**Exercise 10.10.** Show that if the utility is purely real ($d \equiv 0$), the debt channel of the gradient is zero. Verify this for a specific cMDP.

**Exercise 10.11.** Prove that the Fisher information matrix (Definition 10.9.1) is positive semi-definite. Give an example where it is singular.

**Exercise 10.12.** Verify the reparameterization invariance (Proposition 10.9.5) for a specific change of coordinates. Choose two parameterizations $\theta$ and $\xi$ of the same policy family and verify that the natural gradient update is invariant.

**Exercise 10.13.** Implement the CNAC algorithm for a small cMDP. Run a few episodes and verify that the policy gradient is computed correctly.

**Exercise 10.14 (Discussion).** The CNAC algorithm does not require OP1 to be resolved. Is this a virtue or a limitation? Discuss.

**Exercise 10.15 (Discussion).** The exploration signal is the variance of the imaginary advantage, not its mean. Is this intuitive? Give an example where the mean is zero but the variance is non-zero.

**Exercise 10.16 (Open).** Does the CNAC algorithm converge to a local minimum of $|\eta|^2$? Under what conditions on the policy family and the cMDP? (This is Open Problem OP9 in Part V.)

**Exercise 10.17 (Open).** The Fisher matrix is real for real parameters. If the parameters were complex, would the framework change? What would the complex Fisher matrix look like?

**Exercise 10.18 (Open).** The policy gradient theorem uses a single discount factor $\lambda$ for both real and imaginary components. What happens if the two components have different discount factors? Does the policy gradient theorem generalize?

**Exercise 10.19 (Open).** The exploration signal decays to zero at equilibrium (Proposition 10.8.4). Is this the optimal behavior for exploration-exploitation trade-off? Compare with classical methods like entropy regularization or count-based bonuses.

**Exercise 10.20 (Open).** The CNAC algorithm uses a smoothed Fisher estimate with parameter $\beta$. How sensitive is the algorithm to the choice of $\beta$? Is there a principled way to choose it?
