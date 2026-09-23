# Chapter 15 — Cost Geometry and Reward-Free Reinforcement Learning



## 15.1 The two regimes

The framework developed in Chapters 1–14 has been presented as a theory of *cost* — a system that pays an energetic price and an epistemic price, and that minimizes the modulus of their complex combination. Reward, in this presentation, has been either absent or reduced to a subtraction from cost. This chapter makes the two regimes explicit and develops them separately.

**Regime A (Cost geometry, reward-free).** The agent minimizes a complex cost

$$z = c + i\,d,$$

with $c \ge 0$ an energetic cost and $d = \phi(b') - \phi(b)$ an epistemic debt. There is no reward signal. The agent's objective is to reduce its total burden.

**Regime B (Cost–reward geometry).** The agent combines a cost with a reward signal $r$, encoding the net burden as

$$z = \max(0, c - r) + i\,d.$$

The real part is the *net cost after reward*, clipped at zero; the imaginary part remains the epistemic debt.

The two regimes are not competitors. They describe different classes of systems:

- Regime A applies to systems where there is no external reward: biological homeostasis, certain self-supervised learning agents, some classes of RL where the reward is the cost reduction itself.
- Regime B applies to systems where a reward signal is available but should not be the sole objective: standard RL environments where the reward is informative but the epistemic and energetic costs are also relevant.

The framework is honest about the relationship. Regime A is the framework's core; Regime B is an extension that reintroduces reward as a subtractive term. Neither is "the framework" — the framework is the geometry, and the two regimes are two ways of populating it.

## 15.2 Regime A: Cost geometry without reward

### 15.2.1 The objective

The agent minimizes the complex cost $z = c + i\,d$ along the trajectory. The objective is

$$\eta(\theta) = \mathbb{E}^{\pi_\theta}\left[\sum_{k=0}^\infty \lambda^k z(B_k, A_k, B_{k+1})\right] \in \mathbb{C},$$

and the performance is $J(\theta) = |\eta(\theta)|^2$.

There is no reward. The agent does not pursue anything; it reduces tension.

### 15.2.2 Why reward-free matters

**First, it eliminates the reward-shaping problem.** In classical RL, designing a reward signal that leads to the desired behavior is a substantial engineering task, and the resulting agent often optimizes the reward rather than the underlying task. In Regime A, there is no reward to design; the agent minimizes cost, and the cost is determined by the environment and the potential.

**Second, it makes the cost structure explicit.** The cost $c$ and the potential $\phi$ are the framework's inputs. The agent's behavior is determined by these, not by a reward function that may or may not align with them. This makes the framework's predictions clearer: given $c$ and $\phi$, the optimal policy is determined (up to the resolution of OP1).

**Third, it provides a natural account of intrinsic motivation.** If the potential is chosen as negative entropy ( $\phi = -H(\Theta \mid \cdot)$ ), the imaginary component measures information gain, and the agent's behavior is driven by the desire to reduce its own uncertainty — a form of intrinsic motivation that does not require external reward. This is the framework's bridge to the literature on curiosity-driven learning.

### 15.2.3 The cost and potential functions

The framework requires two functions:

- The cost $c(b, a, b')$, which measures the energetic price of a transition.
- The potential $\phi(b)$, whose differences give the debt.

In Regime A, these are the agent's *entire* specification. The choice of $c$ and $\phi$ determines the agent's behavior. This is a strength (the specification is parsimonious) and a limitation (the choice is not always obvious).

The framework does not specify how to choose $c$ and $\phi$. This is Open Problem OP11 in the inventory: the derivation of the cost and potential functions for a given system is an open problem. In practice, they are either given by the environment (physical cost, physical potential) or chosen heuristically (see the CartPole and Pendulum examples in the repository).

### 15.2.4 The evaluation and optimality problems

In Regime A, the evaluation problem is the same as in Chapter 7: the evaluation operator $T^\pi$ is a $\lambda$-contraction, and its fixed point $Q^\pi$ exists and is unique. The optimality problem is the same as in Chapter 8: the Bellman optimality operator $T$ is not obviously a contraction (OP1), and the fixed-point existence is established for finite cMDPs via Schauder.

The policy gradient theorem (Chapter 10) applies in Regime A without modification: the agent's policy can be parameterized, and the gradient of $|\eta|^2$ is computed by the complex policy gradient theorem. The CNAC algorithm (Chapter 10) is the practical instantiation.

## 15.3 Regime B: Cost–reward geometry

### 15.3.1 The objective

In Regime B, a reward signal $r(b, a, b') \in \mathbb{R}$ is available. The agent encodes the net burden as

$$z = \max(0, c - r) + i\,d,$$

where $c$ is the energetic cost and $d$ is the epistemic debt.

The real part $\max(0, c - r)$ is the *net cost after reward*. It is:

- Zero when the reward exceeds or equals the cost ($c \le r$).
- Positive when the cost exceeds the reward ($c > r$).
- Never negative.

The clipping at zero is deliberate: it says that reward can *offset* cost but cannot make the net cost negative. A system that receives more reward than its cost does not accumulate negative cost; it simply has zero net cost.

The imaginary part $d$ is unchanged from Regime A. It is the epistemic debt, independent of the reward.

### 15.3.2 Why reintroduce reward

**First, it connects the framework to standard RL.** In most RL environments, a reward signal is available and informative. Regime B allows the framework to use this signal without abandoning the cost–debt geometry.

**Second, it separates reward from cost.** In classical RL, reward is the objective and cost is a constraint. In Regime B, reward is a *reduction* of cost, and the objective remains the modulus of the complex cost. Reward is informative but not privileged.

**Third, it provides a natural way to incorporate safety constraints.** If the cost $c$ represents a safety violation (e.g. energy expenditure, physical damage), and the reward $r$ is the task reward, then the net cost $\max(0, c - r)$ is zero when the task reward outweighs the safety cost, and positive otherwise. The agent avoids safety violations unless they are well-rewarded.

### 15.3.3 The clipping function

The function $\max(0, \cdot)$ is the *hinge* or *ReLU* clipping. It is not differentiable at $c = r$, and this has consequences for the framework's analysis.

**Why clip at zero?**

- **Loss framing.** The real part of $z$ is a *loss* rather than a *return*. Reward offsets the loss up to a floor of zero. This is the natural interpretation if the agent is minimizing rather than maximizing.
- **Asymmetry of reward and cost.** In many applications, cost is more "costly" than reward is "rewarding." A safety violation, for example, is not offset by a reward of equal numerical magnitude — the violation has effects that persist. The clipping captures the asymmetric relationship.

**Consequences of clipping:**

- The real part of the Bellman operator is no longer linear in $c$ and $r$. The evaluation contraction proof (Theorem 7.2.3) does not apply directly.
- However, the hinge $\max(0, \cdot)$ is 1-Lipschitz. This suggests the contraction may still hold, with a modified modulus bound.
- The differentiability issue at $c = r$ can be handled by subgradient methods in practice.

### 15.3.4 Contraction for Regime B

**Theorem 15.3.1 (Evaluation contraction for Regime B, sketch).** Let $z(b, a, b') = \max(0, c(b, a, b') - r(b, a, b')) + i\,d(b, a, b')$. Define the evaluation operator $T^\pi$ as in Chapter 7. Then $T^\pi$ is a $\lambda$-contraction on $(\mathcal{Q}, \|\cdot\|_\infty)$, with contraction modulus $\lambda$.

*Sketch.* The imaginary part of $T^\pi$ is unchanged from Regime A, so the imaginary component contracts as before. For the real part, the hinge is 1-Lipschitz:

$$|\max(0, c_1 - r) - \max(0, c_2 - r)| \le |c_1 - c_2|.$$

So the real component satisfies

$$|(T^\pi Q_1)_R(b, a) - (T^\pi Q_2)_R(b, a)| \le \lambda \, \mathbb{E}_{b'}\left[|(Q_1)_R(b', \pi(b')) - (Q_2)_R(b', \pi(b'))|\right] \le \lambda \|Q_1 - Q_2\|_\infty.$$

Combining the real and imaginary bounds gives the contraction. $\square$

**Remark 15.3.2 (Status of the theorem).** The sketch establishes the contraction for the evaluation operator. Whether the *optimality* operator contracts in Regime B is open — it depends on the same phase-cancellation obstruction as in Regime A (OP1), plus the additional complication of the hinge.

**Remark 15.3.3 (The hinge as a shaping function).** The hinge $\max(0, c - r)$ can be viewed as a *shaping* of the cost signal. If $r = 0$, the hinge reduces to $c$, and Regime B reduces to Regime A. If $r$ is constant, the hinge is a translation of $c$ with clipping at zero. In general, the hinge allows the reward to *mask* cost up to a threshold, but not to make the net cost negative.

## 15.4 Relationship between the regimes

### 15.4.1 Regime A is a special case of Regime B

**Proposition 15.4.1 (Regime A as a special case).** If $r \equiv 0$ in Regime B, then $z = \max(0, c) + i\,d = c + i\,d$ (since $c \ge 0$), and Regime B reduces to Regime A.

*Proof.* Since $c \ge 0$, $\max(0, c) = c$. $\square$

**Remark 15.4.2 (The reward-free regime is the base case).** Regime A is not a degenerate case of Regime B; it is the *base case*. Regime B is what you get when a reward signal is added. The framework's structure — complex cost, modulus criterion, potential-difference debt — is the same in both. The reward is an addendum.

### 15.4.2 The framework does not commit to a regime

The framework's geometry — complex quasi-metric, γ-family, bitopological structure, equilibrium hierarchy — is independent of whether a reward is present. The choice between Regime A and Regime B is a modeling choice, made by the user based on the system being described.

This is an important structural point. The framework is not "a reward-free RL method" or "a reward-based RL method." It is a geometry, and the two regimes are two ways of populating the geometry with a real part. The choice is external to the framework.

### 15.4.3 Implications for the HST Equilibrium Axiom

The HST Equilibrium Axiom (Chapter 13) states that every information processing system converges to epistemic equilibrium ( $Q_I^\* \to 0$ ). Does the axiom depend on the regime?

**Proposition 15.4.3 (Axiom is regime-independent).** The HST Equilibrium Axiom is stated in terms of the imaginary component of the value function. Since the imaginary component is unchanged between Regimes A and B (both have $d = \phi(b') - \phi(b)$ ), the axiom's statement is the same in both regimes.

*Proof.* The imaginary Bellman equation is the same in both regimes (the hinge affects only the real part). Hence the imaginary component of the fixed point is the same. $\square$

**Remark 15.4.4 (The real part differs).** While the axiom is regime-independent, the real part of the fixed point differs between the regimes. In Regime A, the real part is the discounted cumulative cost. In Regime B, it is the discounted cumulative *net* cost after reward. The two can be very different: a well-rewarded policy has small net cost in Regime B but potentially large cost in Regime A.

### 15.4.4 Implications for the CNAC algorithm

The CNAC algorithm (Chapter 10) can be run in either regime. The only difference is the critic's target $Y_t$:

- **Regime A:** $Y_t = z_t + \lambda Q_\psi(b_{t+1}, \pi_\theta(b_{t+1}))$, where $z_t = c_t + i\,d_t$.
- **Regime B:** $Y_t = z_t + \lambda Q_\psi(b_{t+1}, \pi_\theta(b_{t+1}))$, where $z_t = \max(0, c_t - r_t) + i\,d_t$.

The imaginary part of the target is the same in both cases. The real part differs: Regime B uses net cost after reward.

**Remark 15.4.5 (The critic update is well-defined in both regimes).** The critic loss is $|Q_\psi(b, a) - Y|^2$. This is differentiable in $\psi$ in both regimes. The hinge in Regime B introduces a non-differentiability at $c = r$ for the target $Y$, but this does not affect the differentiability with respect to $\psi$ (the hinge is treated as a fixed target). In practice, subgradient methods handle the non-differentiability.

## 15.5 When to use each regime

**Use Regime A when:**

- The system has no external reward signal.
- The agent's objective is to reduce cost and debt, with no notion of "pursuing" anything.
- The potential is chosen to represent an intrinsic quantity (uncertainty, free energy, Lyapunov function).
- The application is biological, physical, or self-supervised.

**Use Regime B when:**

- A reward signal is available and informative.
- The reward should offset cost up to a threshold but not make cost negative.
- The application is standard RL with safety or energy constraints.
- The cost represents a safety violation or a resource consumption that the reward can compensate.

**The choice is not always clear.** In applications where reward is available but ambiguous, both regimes may be reasonable, and the choice may depend on the specific application. The framework does not prescribe a choice; it provides the geometry for either.

## 15.6 Open problems for Regime B

**OP12. Optimality contraction for Regime B.** Does the Bellman optimality operator contract in Regime B? The hinge introduces an additional nonlinearity, on top of the modulus-greedy selector. Whether the combined operator contracts is open.

**OP13. Hinge effects on the fixed point.** How does the hinge $\max(0, c - r)$ affect the fixed point of the Bellman operator? In particular, does the fixed point differ from Regime A in a predictable way?

**OP14. Choice of clipping.** The hinge is one choice for clipping. Other possibilities include $\log(1 + \max(0, c - r))$, $(\max(0, c - r))^2$, or smooth approximations. Does the choice of clipping affect the framework's convergence and equilibrium properties?

**OP15. Reward shaping in Regime B.** The reward $r$ plays a role analogous to reward shaping in classical RL. Under what conditions does a given reward $r$ preserve the optimal policy of Regime A? This is a question about potential-based reward shaping in the complex setting.

## 15.7 Summary

The framework has two regimes:

**Regime A (cost geometry, reward-free).** The agent minimizes $z = c + i\,d$. No reward. The objective is to reduce burden.

**Regime B (cost–reward geometry).** The agent minimizes $z = \max(0, c - r) + i\,d$. Reward offsets cost up to a floor of zero. The objective is to reduce net burden.

The two regimes share the framework's geometry. The imaginary component is the same in both. The real component differs: Regime A uses raw cost, Regime B uses net cost after reward.

The choice between regimes is a modeling choice, not a commitment of the framework. Regime A is the base case; Regime B is an extension. Both are legitimate, and the choice depends on the application.

The evaluation contraction holds in Regime B (Theorem 15.3.1, sketch). The optimality contraction (OP12) is open, as it is in Regime A (OP1). The CNAC algorithm runs in either regime, with the only difference being the critic's target.

The framework's central interpretive claim (the HST Equilibrium Axiom) is regime-independent: the imaginary component of the fixed point is the same in both regimes. What differs is the real component — the discounted net cost after reward.

This chapter makes the reward-free and cost–reward regimes explicit, and clarifies that the framework is not committed to either. The geometry is the framework; the regime is a modeling choice.

## Exercises

**Exercise 15.1.** For a cMDP with cost $c = 1$, reward $r = 0.5$, and debt $d = 0.2$, compute $z$ in Regime A and in Regime B. Compare the moduli.

**Exercise 15.2.** For the same cMDP, compute $z$ when $r = 1.5$ (reward exceeds cost). What is the real part in Regime B? What is the modulus?

**Exercise 15.3.** Verify Proposition 15.4.1 (Regime A is a special case of Regime B with $r = 0$).

**Exercise 15.4.** Sketch the proof of Theorem 15.3.1 (evaluation contraction for Regime B) in full. Pay particular attention to the hinge's 1-Lipschitz property.

**Exercise 15.5.** Construct a cMDP where the optimal policy differs between Regimes A and B. Explain why.

**Exercise 15.6.** Verify Proposition 15.4.3 (the HST Equilibrium Axiom is regime-independent) for a specific cMDP.

**Exercise 15.7.** Implement the CNAC algorithm in both regimes on a simple cMDP. Compare the learning curves.

**Exercise 15.8.** Show that if $r \equiv 0$, the CNAC algorithm in Regime B reduces to the CNAC algorithm in Regime A.

**Exercise 15.9.** For a cMDP with cost $c$ and reward $r$, compute the value of $z$ in Regime B when $c < r$ and when $c > r$. Show that the real part is continuous at $c = r$ but not differentiable.

**Exercise 15.10.** Design a cost function $c$ and a reward $r$ such that the optimal policy in Regime B is to *never* receive reward (i.e., always stay in a state where $c = 0$). Is this possible? What does it mean?

**Exercise 15.11 (Discussion).** Regime A is reward-free. Is this a strength (no reward to design) or a limitation (no signal to guide learning)? Discuss.

**Exercise 15.12 (Discussion).** Regime B reintroduces reward. Is this a betrayal of the framework's "reward-free" aspirations? Or is it a natural extension?

**Exercise 15.13 (Discussion).** The hinge $\max(0, c - r)$ is one choice for clipping. What other choices might be reasonable? What properties would they need to have?

**Exercise 15.14 (Open).** Prove or disprove OP12: the Bellman optimality operator contracts in Regime B.

**Exercise 15.15 (Open).** How does the hinge affect the fixed point of the Bellman operator in Regime B? Is there a regime-B analogue of the first-quadrant result (Corollary 8.5.3)?

**Exercise 15.16 (Open).** Characterize the reward functions $r$ that preserve the optimal policy of Regime A. This is a question about reward shaping in the complex setting.

**Exercise 15.17 (Open).** The framework is presented in two regimes. Are there other natural regimes — e.g., reward-only ($z = r + i\,d$), cost-reward with different clipping, or multi-objective extensions? What would they look like?

**Exercise 15.18 (Open).** The HST Equilibrium Axiom is stated in terms of the imaginary component. Is the axiom as plausible in Regime B as in Regime A? Or does the presence of reward affect the interpretation?
