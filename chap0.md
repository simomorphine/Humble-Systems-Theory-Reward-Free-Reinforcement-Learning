Here is Chapter 0 rewritten — no drawings, no references, no exercises, no bandit example.

---

# Chapter 0: The Problem of Two Burdens

## 0.1 The Two Burdens of an Adaptive Agent

Every adaptive agent navigating an uncertain world faces two qualitatively distinct burdens simultaneously. These burdens are not merely different in degree — they are different in kind. They have different mathematical properties, different physical interpretations, and different implications for decision-making. Yet classical reinforcement learning treats them as if they were the same.

The first burden is **real cost** ($c$) — the measurable, immediate price of action. This is the tangible currency of physical and computational systems: joules of energy consumed, seconds of time elapsed, dollars spent, bits processed, errors made. Real cost is additive and cumulative: costs sum along a trajectory, and the total cost of a path is the sum of its parts. It is path-dependent: the cost of going from $A$ to $C$ via $B$ is generally greater than going directly. It is irreversible: once energy is spent or time elapsed, it cannot be recovered. And it is non-negative: $c \geq 0$ for all transitions.

The second burden is **information debt** ($d$) — the epistemic burden of operating with incomplete or miscalibrated models. As established in prior work, debt is conservative: it behaves like a potential difference, depending only on the endpoints of a transition, not the path taken. For any states $s_i, s_j, s_k$, we have $d(s_i, s_k) = d(s_i, s_j) + d(s_j, s_k)$. It is reversible: debt can be paid down by gaining information. And it is sign-unrestricted: debt can be positive when uncertainty increases, or negative when knowledge is gained.

| Property | Real Cost ($c$) | Information Debt ($d$) |
|----------|----------------|----------------------|
| Additivity | Additive | Conservative |
| Path-dependence | Path-dependent | Path-independent |
| Sign | $c \geq 0$ | $d \in \mathbb{R}$ |
| Reversibility | Irreversible | Reversible |

These are not two dimensions of the same quantity. They are two fundamentally different types of burden. A decision-making framework that cannot distinguish between them is missing something essential.

## 0.2 The Classical Reinforcement Learning Paradigm

### 0.2.1 The Markov Decision Process

The mathematical foundation of reinforcement learning is the Markov Decision Process. An MDP provides a formal framework for modeling sequential decision-making under uncertainty.

**Definition 0.1 (Markov Decision Process).** A finite Markov Decision Process is a tuple $(\mathcal{S}, \mathcal{A}, p, r, \lambda)$ where $\mathcal{S}$ is a finite set of states, $\mathcal{A}$ is a finite set of actions, $p(s' \mid s, a)$ is the transition probability satisfying $\sum_{s'} p(s' \mid s, a) = 1$, $r(s, a, s')$ is a scalar reward function, and $\lambda \in [0,1)$ is a discount factor.

The Markov property asserts that the future depends only on the current state and action:

$$p(s_{t+1} \mid s_t, a_t, s_{t-1}, a_{t-1}, \ldots) = p(s_{t+1} \mid s_t, a_t).$$

This makes the framework mathematically tractable and enables dynamic programming.

### 0.2.2 Policies, Returns, and Value Functions

**Definition 0.2 (Policy).** A policy $\pi$ maps each state to either a single action (deterministic) or a probability distribution over actions (stochastic), with $\sum_{a} \pi(a \mid s) = 1$.

**Definition 0.3 (Return).** The discounted return from time $t$ is:

$$G_t = \sum_{k=0}^{\infty} \lambda^k R_{t+k+1}.$$

**Definition 0.4 (State-Value Function).** The value of a state under policy $\pi$ is:

$$V^\pi(s) = \mathbb{E}^\pi[G_t \mid S_t = s].$$

**Definition 0.5 (Action-Value Function).** The value of taking action $a$ in state $s$ under policy $\pi$ is:

$$Q^\pi(s,a) = \mathbb{E}^\pi[G_t \mid S_t = s, A_t = a].$$

These are related by $V^\pi(s) = \sum_{a} \pi(a \mid s) Q^\pi(s, a)$.

### 0.2.3 Bellman Equations and Optimality

The Bellman equations express value functions recursively:

$$V^\pi(s) = \sum_{a} \pi(a \mid s) \sum_{s'} p(s' \mid s, a)\left[r(s,a,s') + \lambda V^\pi(s')\right],$$

$$Q^\pi(s,a) = \sum_{s'} p(s' \mid s, a)\left[r(s,a,s') + \lambda \sum_{a'} \pi(a' \mid s') Q^\pi(s', a')\right].$$

The Bellman evaluation operator $T^\pi$ acts on value functions by:

$$(T^\pi V)(s) = \sum_{a} \pi(a \mid s) \sum_{s'} p(s' \mid s, a)\left[r(s,a,s') + \lambda V(s')\right].$$

**Theorem 0.1 (Contraction of $T^\pi$).** $T^\pi$ is a $\lambda$-contraction in the sup-norm:

$$\|T^\pi V_1 - T^\pi V_2\|_\infty \leq \lambda \|V_1 - V_2\|_\infty.$$

This guarantees that iterative application of $T^\pi$ converges to the unique fixed point $V^\pi$.

The optimal value functions are:

$$V^*(s) = \max_\pi V^\pi(s), \qquad Q^*(s,a) = \max_\pi Q^\pi(s,a).$$

They satisfy the Bellman optimality equations:

$$V^*(s) = \max_{a} \sum_{s'} p(s' \mid s,a)\left[r(s,a,s') + \lambda V^*(s')\right],$$

$$Q^*(s,a) = \sum_{s'} p(s' \mid s,a)\left[r(s,a,s') + \lambda \max_{a'} Q^*(s',a')\right].$$

The Bellman optimality operator $T$ defined by:

$$(TQ)(s,a) = \sum_{s'} p(s' \mid s,a)\left[r(s,a,s') + \lambda \max_{a'} Q(s',a')\right]$$

is also a $\lambda$-contraction in the sup-norm, ensuring convergence of value iteration to $Q^*$.

### 0.2.4 The Central Limitation

Classical RL treats rewards as scalar quantities. The agent's objective is to maximize a single number. This framework has achieved remarkable success, but it rests on a hidden assumption: that all objectives can be meaningfully combined into a single scalar. When an agent faces both cost and debt, this assumption fails — and the failure is fundamental, not incidental.

## 0.3 Why Scalarisation Fails

### 0.3.1 Linear Scalarisation and the Free Parameter

When an agent faces multiple objectives, the standard approach is linear scalarisation: combine them into a single scalar reward:

$$r_{\text{total}} = c + \mu d,$$

where $\mu \geq 0$ is a weighting parameter. This is simple, and it uses standard RL algorithms without modification. But it introduces a free parameter whose choice is arbitrary, environment-dependent, task-dependent, and state-dependent. No single $\mu$ works across all environments, tasks, or phases of learning.

This is the **Free Parameter Problem**.

### 0.3.2 The Free Parameter Problem

**Theorem 0.2 (The Free Parameter Problem).** Let an environment be characterized by a set of feasible policies, each with cost $C(\pi) \geq 0$ and debt $D(\pi) \geq 0$. Consider the scalarised objective:

$$J_\mu(\pi) = C(\pi) + \mu D(\pi), \qquad \mu > 0.$$

Then:

1. **Within-environment dependence.** There exists an MDP for which the optimal policy changes from cost-favoring to debt-favoring as $\mu$ varies.

2. **Cross-environment inconsistency.** For every fixed $\mu > 0$, there exist two MDPs for which the same $\mu$ selects opposite trade-offs: cost-favoring in one and debt-favoring in the other.

Consequently, $\mu$ has no environment-independent interpretation as a universal exchange rate between cost and debt.

**Proof.**

*Part 1.* Consider an MDP with two feasible policies satisfying $(C(\pi^c), D(\pi^c)) = (0,1)$ and $(C(\pi^d), D(\pi^d)) = (1,0)$. Their scalarised objectives are $J_\mu(\pi^c) = \mu$ and $J_\mu(\pi^d) = 1$. Therefore:

$$\pi_\mu^* = \begin{cases} \pi^c & \mu < 1 \\ \pi^d & \mu > 1. \end{cases}$$

The optimal policy switches at $\mu^* = 1$. Even within a fixed environment, the effect of $\mu$ is not invariant.

*Part 2.* Fix any $\mu > 0$. Construct $M_1$ with policies $(C(\pi_1^c), D(\pi_1^c)) = (0,1)$ and $(C(\pi_1^d), D(\pi_1^d)) = (2\mu, 0)$. Then $J_\mu(\pi_1^c) = \mu < 2\mu = J_\mu(\pi_1^d)$, so $\mu$ selects the cost-favoring policy $\pi_1^c$.

Construct $M_2$ with policies $(C(\pi_2^c), D(\pi_2^c)) = (0, 2/\mu)$ and $(C(\pi_2^d), D(\pi_2^d)) = (1,0)$. Then $J_\mu(\pi_2^c) = 2 > 1 = J_\mu(\pi_2^d)$, so $\mu$ selects the debt-favoring policy $\pi_2^d$.

Since $\mu > 0$ was arbitrary, no fixed scalarisation weight can serve as a universal exchange rate. $\blacksquare$

The general break-even threshold between any two policies $\pi^c$ and $\pi^d$ with $C(\pi^c) < C(\pi^d)$ and $D(\pi^c) > D(\pi^d)$ is:

$$\mu^* = \frac{C(\pi^d) - C(\pi^c)}{D(\pi^c) - D(\pi^d)}.$$

The preferred policy depends entirely on whether $\mu$ is above or below this threshold, and the threshold is environment-dependent.

**Corollary 0.1.** No fixed $\mu > 0$ is universally optimal across all environments.

### 0.3.3 Alternative Scalarisation Approaches

Linear scalarisation is not the only approach. Non-linear scalarisation uses $r = f(c,d)$ for some function $f$. Lexicographic ordering prioritizes objectives strictly. Pareto-based methods maintain a set of non-dominated policies. Threshold-based methods optimize the primary objective subject to constraints on the secondary.

All of these share the same defect: they require choosing parameters — weights, priorities, thresholds, or selection criteria — that are arbitrary, environment-dependent, and task-dependent. The Free Parameter Problem is not specific to linear scalarisation. It is the inherent consequence of treating cost and debt as two separate quantities to be traded off by an external designer.

The issue is not scalarisation itself. It is the assumption that a single externally chosen parameter can universally encode the correct trade-off. No such parameter exists.

### 0.3.4 The Geometry of Failure

Linear scalarisation $c + \mu d = \text{constant}$ defines lines of fixed slope $-1/\mu$ in the cost-debt plane. The scalarisation selects the point on the Pareto frontier where a line of this slope is tangent to the frontier. But the Pareto frontier's shape varies across environments. The same slope corresponds to different points on different frontiers. The optimal slope depends on the frontier's shape, which the agent cannot know in advance.

This is the geometry of failure: fixed-slope level sets cannot universally track a frontier whose shape changes with the environment.

## 0.4 A Geometric Alternative: The Complex Encoding

### 0.4.1 From Weighting to Geometry

The failure of scalarisation suggests a shift in perspective. Instead of asking *how should we weight cost and debt*, we should ask *what is the natural geometry of cost and debt*.

Cost and debt are not two quantities that need to be combined — they are two components of a single geometric object. The Euclidean distance from the origin in the cost-debt plane is natural, principled, and free of arbitrary weights:

$$\text{Distance} = \sqrt{c^2 + d^2}.$$

This is the modulus of the complex number $z = c + id$.

### 0.4.2 The Complex Utility

**Definition 0.6 (Complex Utility).** Let $z = c + id \in \mathbb{C}$, where $c \in \mathbb{R}_{\geq 0}$ is the real cost and $d \in \mathbb{R}$ is the information debt. The complex utility $z$ represents the total burden of an action or transition in the cost-debt plane.

The real axis represents cost; the imaginary axis represents debt. Every action corresponds to a point in this plane. A point with $d = 0$ is a pure cost action — exploitation. A point with $c = 0, d < 0$ is pure information gathering — exploration. A point with $d < 0$ is one that pays down debt at a cost.

### 0.4.3 The Modulus as Natural Objective

**Definition 0.7 (Modulus Objective).** The performance criterion is:

$$J(z) = |z| = \sqrt{c^2 + d^2}.$$

Minimizing $|z|$ is principled because Euclidean distance is the natural metric on the cost-debt plane. It is parameter-free: no $\mu$, no $\epsilon$, no schedule. It is scale-aware: when cost dominates, the agent focuses on reducing cost; when debt dominates, the agent focuses on gathering information. The level sets of the modulus are circles $c^2 + d^2 = R^2$, and minimizing $|z|$ means moving toward the origin — the point of zero cost and zero debt.

The contrast with scalarisation is complete:

| Aspect | Scalarisation $c + \mu d$ | Complex $|z|$ |
|--------|--------------------------|---------------|
| Weighting | $\mu$ is arbitrary | No weights |
| Level sets | Lines | Circles |
| Trade-off | Determined by $\mu$ | Determined by geometry |
| Parameters | One ($\mu$) | Zero |

### 0.4.4 The Phase as Exploration-Exploitation Angle

**Definition 0.8 (Phase).** The phase of the complex utility is:

$$\theta = \arg(z) = \arctan\left(\frac{d}{c}\right).$$

The phase measures the instantaneous balance between cost and debt. When $\theta = 0$, debt is zero and the agent is in pure exploitation mode. When $\theta$ is large, debt dominates and the agent is in exploration mode. When $\theta < 0$, the agent is actively paying down debt — gaining information at a cost.

As the agent learns, debt decreases and $\theta$ decreases from exploration toward exploitation. This transition is automatic. No external schedule is required. No annealing is needed. The geometry drives it.

### 0.4.5 The HST Equilibrium Axiom

This book is grounded in Humble Systems Theory (HST), which provides the overarching framework for the complex approach.

**Axiom 0.1 (HST Equilibrium Axiom).** Every Information Processing System evolves toward epistemic equilibrium — a state of minimum computational cost subject to informational constraints.

At epistemic equilibrium, the system has no remaining epistemic debt: $d = 0$ for all relevant quantities. It acts as a pure cost minimizer. It has achieved the minimum possible computational cost given its environment.

The Equilibrium Axiom implies that the transition from exploration to exploitation is not something that must be engineered — it is the natural trajectory of any information processing system. The modulus-greedy policy:

$$\pi_Q(s) = \arg\min_{a \in \mathcal{A}} |Q(s,a)|$$

automatically shifts from exploring when debt is large to exploiting when debt is small. The geometry of $\mathbb{C}$ does the work.

### 0.4.6 The Complex MDP

The geometric insight leads to a complete framework. The Complex MDP is:

$$\mathcal{M} = (\mathcal{S}, \mathcal{A}, p, z, \lambda),$$

where $z = c + id$ replaces the scalar reward. The complex return is:

$$G_t = \sum_{k=0}^{\infty} \lambda^k z(S_{t+k}, A_{t+k}, S_{t+k+1}) \in \mathbb{C}.$$

The complex value functions are:

$$V^\pi(s) = \mathbb{E}^\pi[G_t \mid S_t = s] \in \mathbb{C}, \qquad Q^\pi(s,a) = \mathbb{E}^\pi[G_t \mid S_t = s, A_t = a] \in \mathbb{C}.$$

The performance criterion is $J^\pi(s) = |V^\pi(s)|$. The agent seeks to minimize this for all states — to reach the origin of the cost-debt plane.

## 0.5 Why Complex Numbers Are Not Arbitrary

### 0.5.1 The Uniqueness of $\mathbb{C}$

A natural question arises: why complex numbers? Why not vectors, quaternions, or some other structure? The answer is that $\mathbb{C}$ is the unique two-dimensional structure satisfying the properties we need.

**Theorem 0.3 (Frobenius, 1877).** Any two-dimensional real algebra that is a field is isomorphic to $\mathbb{C}$.

The alternatives fail:

- **Split-complex numbers** $a + bj$ with $j^2 = 1$ have zero divisors: $(1+j)(1-j) = 0$. They are not a field and admit no compatible norm.
- **Dual numbers** $a + b\epsilon$ with $\epsilon^2 = 0$ also have zero divisors and are not a field.
- **Quaternions** are four-dimensional and non-commutative, making them unsuitable for a two-burden framework.

If we require a two-dimensional structure with addition, multiplication, and a compatible norm, $\mathbb{C}$ is the only choice. It is not arbitrary — it is mathematically forced.

### 0.5.2 Why Complex Numbers Are Better Than Vectors

The difference between complex numbers and two-dimensional vectors is structural, not notational.

Vectors have no natural multiplication. The dot product produces a scalar; the cross product is undefined in two dimensions. The Euclidean norm $\sqrt{c^2 + d^2}$ is one of many possible norms — its selection requires justification.

Complex numbers have natural multiplication with direct geometric meaning: $(c_1 + id_1)(c_2 + id_2)$ rotates and scales in the complex plane. The modulus $|z| = \sqrt{c^2 + d^2}$ is the unique norm satisfying multiplicativity $|z_1 z_2| = |z_1||z_2|$ and compatibility with the field structure. It is not chosen from among alternatives — it is forced by the algebra.

The phase $\theta = \arg(z)$ is intrinsic to the algebraic structure via $z = |z|e^{i\theta}$. For vectors, the angle between components must be defined externally. For complex numbers, it is part of what the number is.

Finally, complex numbers support the full theory of complex analysis — holomorphic functions, conformal mappings, contour integration — which will be used throughout this book. Vectors support none of this.

### 0.5.3 The Role of the Modulus in a Field

The modulus plays a special role because it is compatible with the field structure of $\mathbb{C}$:

- **Multiplicativity:** $|z_1 z_2| = |z_1||z_2|$.
- **Triangle inequality:** $|z_1 + z_2| \leq |z_1| + |z_2|$.
- **Positive definiteness:** $|z| \geq 0$, with equality if and only if $z = 0$.

These properties are not available for an arbitrary choice of norm on $\mathbb{R}^2$. They follow from the field structure of $\mathbb{C}$ and underpin the contraction properties of the complex Bellman operators developed in subsequent chapters.

### 0.5.4 The Geometric Meaning of Complex Operations

Every operation on complex numbers has a direct interpretation in the cost-debt plane:

| Operation | Formula | Meaning |
|-----------|---------|---------|
| Addition | $(c_1 + c_2) + i(d_1 + d_2)$ | Combining burdens |
| Conjugation | $c - id$ | Debt reversal |
| Modulus | $\sqrt{c^2 + d^2}$ | Total burden |
| Phase | $\arctan(d/c)$ | Exploration angle |
| Multiplication | Rotation and scaling | Composing utilities |

This correspondence is not imposed on the complex numbers — it emerges from their structure. The algebra and the geometry are the same thing.

## 0.6 The Landscape of Related Work

### 0.6.1 Multi-Objective Reinforcement Learning

Multi-Objective Reinforcement Learning (MORL) extends classical RL to problems with vector-valued rewards $\mathbf{r}: \mathcal{S} \times \mathcal{A} \to \mathbb{R}^n$. The main approaches — linear scalarisation, lexicographic ordering, Pareto-based methods, and threshold-based methods — all require choosing parameters. The complex framework eliminates these parameters by recognizing that cost and debt are not two objectives to be weighted but two components of a single geometric object.

The key distinction is that MORL treats the trade-off as a design choice made by the system's designer. The complex framework treats it as a geometric fact determined by the structure of the problem.

### 0.6.2 Information-Theoretic Reinforcement Learning

Information-theoretic approaches use entropy, mutual information, or KL divergence to guide exploration. Information-directed sampling minimizes an information ratio that implicitly requires tuning. Maximum entropy RL adds an entropy bonus $\beta \mathcal{H}(\pi)$ with a temperature parameter $\beta$ that must be chosen and is environment-dependent.

The complex framework provides a parameter-free alternative. The imaginary component $Q_I$ naturally encodes information value, and the modulus $|Q|$ automatically balances cost minimization and debt reduction. Exploration is not incentivized by a bonus — it emerges from the geometry.

### 0.6.3 Complex-Valued Neural Networks

Complex-valued neural networks use complex numbers as computational building blocks, with applications in signal processing and deep learning. These approaches focus on representation learning — using complex arithmetic to improve the expressiveness of neural networks.

The complex framework developed in this book is different in purpose. It uses complex numbers not for representation but for decision-making: to define the objective, the value functions, the Bellman operators, and the policy. The theoretical foundation — complex MDPs, complex Bellman equations, epistemic equilibrium — has no counterpart in the CVNN literature.

### 0.6.4 Humble Systems Theory

Humble Systems Theory is the overarching framework that unifies the approach developed in this book. Its central claim is that every information processing system is naturally driven toward epistemic equilibrium by the geometry of its problem space. Cost and debt are the two fundamental burdens. The complex plane is the natural setting. Exploration and exploitation are not behaviors to be engineered — they are phases of a single geometric process.

The present chapter has established the foundations of this framework: the failure of scalarisation, the geometric alternative, the uniqueness of $\mathbb{C}$, and the connection to prior work. The remaining chapters develop the theory in full.

---