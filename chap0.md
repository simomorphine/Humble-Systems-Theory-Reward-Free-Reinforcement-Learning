Chapter 0: The Problem of Two Burdens

0.1 The Two Burdens of an Adaptive Agent

Every adaptive agent navigating an uncertain world faces two qualitatively distinct burdens simultaneously. These burdens are not merely different in degree — they are different in kind. They have different mathematical properties, different physical interpretations, and different implications for decision-making. Yet classical reinforcement learning treats them as if they were the same.

The first burden is real cost ($c$) — the measurable, immediate price of action. This is the tangible currency of physical and computational systems: joules of energy consumed, seconds of time elapsed, dollars spent, bits processed, errors made. Real cost is additive and cumulative: costs sum along a trajectory, and the total cost of a path is the sum of its parts. It is path-dependent: the cost of going from $A$ to $C$ via $B$ is generally greater than going directly. It is irreversible: once energy is spent or time elapsed, it cannot be recovered. And it is non-negative: $c \geq 0$ for all transitions.

The second burden is information debt ($d$) — the epistemic burden of operating with incomplete or miscalibrated models. As established in prior work, debt is conservative: it behaves like a potential difference, depending only on the endpoints of a transition, not the path taken. For any states $s_i, s_j, s_k$, we have $d(s_i, s_k) = d(s_i, s_j) + d(s_j, s_k)$. It is reversible: debt can be paid down by gaining information. And it is sign-unrestricted: debt can be positive when uncertainty increases, or negative when knowledge is gained.

Property Real Cost ($c$) Information Debt ($d$)
Additivity Additive Conservative
Path-dependence Path-dependent Path-independent
Sign $c \geq 0$ $d \in \mathbb{R}$
Reversibility Irreversible Reversible

These are not two dimensions of the same quantity. They are two fundamentally different types of burden. A decision-making framework that cannot distinguish between them is missing something essential.

0.2 The Classical Reinforcement Learning Paradigm

0.2.1 The Markov Decision Process

The mathematical foundation of reinforcement learning is the Markov Decision Process. An MDP provides a formal framework for modeling sequential decision-making under uncertainty.

Definition 0.1 (Markov Decision Process). A finite Markov Decision Process is a tuple $(\mathcal{S}, \mathcal{A}, p, r, \lambda)$ where $\mathcal{S}$ is a finite set of states, $\mathcal{A}$ is a finite set of actions, $p(s' \mid s, a)$ is the transition probability satisfying $\sum_{s'} p(s' \mid s, a) = 1$, $r(s, a, s')$ is a scalar reward function, and $\lambda \in [0,1)$ is a discount factor.

The Markov property asserts that the future depends only on the current state and action:

p(s_{t+1} \mid s_t, a_t, s_{t-1}, a_{t-1}, \ldots) = p(s_{t+1} \mid s_t, a_t).

This makes the framework mathematically tractable and enables dynamic programming.

0.2.2 Policies, Returns, and Value Functions

Definition 0.2 (Policy). A policy $\pi$ maps each state to either a single action (deterministic) or a probability distribution over actions (stochastic), with $\sum_{a} \pi(a \mid s) = 1$.

Definition 0.3 (Return). The discounted return from time $t$ is:

G_t = \sum_{k=0}^{\infty} \lambda^k R_{t+k+1}.

Definition 0.4 (State-Value Function). The value of a state under policy $\pi$ is:

V^\pi(s) = \mathbb{E}^\pi[G_t \mid S_t = s].

Definition 0.5 (Action-Value Function). The value of taking action $a$ in state $s$ under policy $\pi$ is:

Q^\pi(s,a) = \mathbb{E}^\pi[G_t \mid S_t = s, A_t = a].

These are related by $V^\pi(s) = \sum_{a} \pi(a \mid s) Q^\pi(s, a)$.

0.2.3 Bellman Equations and Optimality

The Bellman equations express value functions recursively:

V^\pi(s) = \sum_{a} \pi(a \mid s) \sum_{s'} p(s' \mid s, a)\left[r(s,a,s') + \lambda V^\pi(s')\right],

Q^\pi(s,a) = \sum_{s'} p(s' \mid s, a)\left[r(s,a,s') + \lambda \sum_{a'} \pi(a' \mid s') Q^\pi(s', a')\right].

The Bellman evaluation operator $T^\pi$ acts on value functions by:

(T^\pi V)(s) = \sum_{a} \pi(a \mid s) \sum_{s'} p(s' \mid s, a)\left[r(s,a,s') + \lambda V(s')\right].

Theorem 0.1 (Contraction of $T^\pi$). $T^\pi$ is a $\lambda$-contraction in the sup-norm:

\|T^\pi V_1 - T^\pi V_2\|_\infty \leq \lambda \|V_1 - V_2\|_\infty.

This guarantees that iterative application of $T^\pi$ converges to the unique fixed point $V^\pi$.

The optimal value functions are:

V^*(s) = \max_\pi V^\pi(s), \qquad Q^*(s,a) = \max_\pi Q^\pi(s,a).

They satisfy the Bellman optimality equations:

V^*(s) = \max_{a} \sum_{s'} p(s' \mid s,a)\left[r(s,a,s') + \lambda V^*(s')\right],

Q^*(s,a) = \sum_{s'} p(s' \mid s,a)\left[r(s,a,s') + \lambda \max_{a'} Q^*(s',a')\right].

The Bellman optimality operator $T$ defined by:

(TQ)(s,a) = \sum_{s'} p(s' \mid s,a)\left[r(s,a,s') + \lambda \max_{a'} Q(s',a')\right]

is also a $\lambda$-contraction in the sup-norm, ensuring convergence of value iteration to $Q^*$.

0.2.4 The Central Limitation

Classical RL treats rewards as scalar quantities. The agent's objective is to maximize a single number. This framework has achieved remarkable success, but it rests on a hidden assumption: that all objectives can be meaningfully combined into a single scalar. When an agent faces both cost and debt, this assumption fails — and the failure is fundamental, not incidental.

0.3 Why Scalarisation Fails

0.3.1 Linear Scalarisation and the Free Parameter

When an agent faces multiple objectives, the standard approach is linear scalarisation: combine them into a single scalar reward:

r_{\text{total}} = c + \mu d,

where $\mu \geq 0$ is a weighting parameter. This is simple, and it uses standard RL algorithms without modification. But it introduces a free parameter whose choice is arbitrary, environment-dependent, task-dependent, and state-dependent. No single $\mu$ works across all environments, tasks, or phases of learning.

This is the Free Parameter Problem.

0.3.2 The Free Parameter Problem

Theorem 0.2 (The Free Parameter Problem). Let an environment be characterized by a set of feasible policies, each with cost $C(\pi) \geq 0$ and debt $D(\pi) \geq 0$. Consider the scalarised objective:

J_\mu(\pi) = C(\pi) + \mu D(\pi), \qquad \mu > 0.

Then:

1. Within-environment dependence. There exists an MDP for which the optimal policy changes from cost-favoring to debt-favoring as $\mu$ varies.
2. Cross-environment inconsistency. For every fixed $\mu > 0$, there exist two MDPs for which the same $\mu$ selects opposite trade-offs: cost-favoring in one and debt-favoring in the other.

Consequently, $\mu$ has no environment-independent interpretation as a universal exchange rate between cost and debt.

Proof.

Part 1. Consider an MDP with two feasible policies satisfying $(C(\pi^c), D(\pi^c)) = (0,1)$ and $(C(\pi^d), D(\pi^d)) = (1,0)$. Their scalarised objectives are $J_\mu(\pi^c) = \mu$ and $J_\mu(\pi^d) = 1$. Therefore:

\pi_\mu^* = \begin{cases} \pi^c & \mu < 1 \\ \pi^d & \mu > 1. \end{cases}

The optimal policy switches at $\mu^* = 1$. Even within a fixed environment, the effect of $\mu$ is not invariant.

Part 2. Fix any $\mu > 0$. Construct $M_1$ with policies $(C(\pi_1^c), D(\pi_1^c)) = (0,1)$ and $(C(\pi_1^d), D(\pi_1^d)) = (2\mu, 0)$. Then $J_\mu(\pi_1^c) = \mu < 2\mu = J_\mu(\pi_1^d)$, so $\mu$ selects the cost-favoring policy $\pi_1^c$.

Construct $M_2$ with policies $(C(\pi_2^c), D(\pi_2^c)) = (0, 2/\mu)$ and $(C(\pi_2^d), D(\pi_2^d)) = (1,0)$. Then $J_\mu(\pi_2^c) = 2 > 1 = J_\mu(\pi_2^d)$, so $\mu$ selects the debt-favoring policy $\pi_2^d$.

Since $\mu > 0$ was arbitrary, no fixed scalarisation weight can serve as a universal exchange rate. $\blacksquare$

The general break-even threshold between any two policies $\pi^c$ and $\pi^d$ with $C(\pi^c) < C(\pi^d)$ and $D(\pi^c) > D(\pi^d)$ is:

\mu^* = \frac{C(\pi^d) - C(\pi^c)}{D(\pi^c) - D(\pi^d)}.

The preferred policy depends entirely on whether $\mu$ is above or below this threshold, and the threshold is environment-dependent.

Corollary 0.1. No fixed $\mu > 0$ is universally optimal across all environments.

0.3.3 Alternative Scalarisation Approaches

Linear scalarisation is not the only approach. Non-linear scalarisation uses $r = f(c,d)$ for some function $f$. Lexicographic ordering prioritizes objectives strictly. Pareto-based methods maintain a set of non-dominated policies. Threshold-based methods optimize the primary objective subject to constraints on the secondary.

All of these share the same defect: they require choosing parameters — weights, priorities, thresholds, or selection criteria — that are arbitrary, environment-dependent, and task-dependent. The Free Parameter Problem is not specific to linear scalarisation. It is the inherent consequence of treating cost and debt as two separate quantities to be traded off by an external designer.

The issue is not scalarisation itself. It is the assumption that a single externally chosen parameter can universally encode the correct trade-off. No such parameter exists.

0.3.4 The Geometry of Failure

Linear scalarisation $c + \mu d = \text{constant}$ defines lines of fixed slope $-1/\mu$ in the cost-debt plane. The scalarisation selects the point on the Pareto frontier where a line of this slope is tangent to the frontier. But the Pareto frontier's shape varies across environments. The same slope corresponds to different points on different frontiers. The optimal slope depends on the frontier's shape, which the agent cannot know in advance.

This is the geometry of failure: fixed-slope level sets cannot universally track a frontier whose shape changes with the environment.

0.4 A Geometric Alternative: The Complex Encoding

0.4.1 From Weighting to Geometry

The failure of scalarisation suggests a shift in perspective. Instead of asking how should we weight cost and debt, we should ask what is the natural geometry of cost and debt.

Cost and debt are not two quantities that need to be combined — they are two components of a single geometric object. The Euclidean distance from the origin in the cost-debt plane is natural, principled, and free of arbitrary weights:

\text{Distance} = \sqrt{c^2 + d^2}.

This is the modulus of the complex number $z = c + id$.

0.4.2 The Complex Utility

Definition 0.6 (Complex Utility). Let $z = c + id \in \mathbb{C}$, where $c \in \mathbb{R}_{\geq 0}$ is the real cost and $d \in \mathbb{R}$ is the information debt. The complex utility $z$ represents the total burden of an action or transition in the cost-debt plane.

The real axis represents cost; the imaginary axis represents debt. Every action corresponds to a point in this plane. A point with $d = 0$ is a pure cost action — exploitation. A point with $c = 0, d < 0$ is pure information gathering — exploration. A point with $d < 0$ is one that pays down debt at a cost.

0.4.3 The Modulus as Natural Objective

Definition 0.7 (Modulus Objective). The performance criterion is:

J(z) = |z| = \sqrt{c^2 + d^2}.

Minimizing $|z|$ is principled because Euclidean distance is the natural metric on the cost-debt plane. It is parameter-free: no $\mu$, no $\epsilon$, no schedule. It is scale-aware: when cost dominates, the agent focuses on reducing cost; when debt dominates, the agent focuses on gathering information. The level sets of the modulus are circles $c^2 + d^2 = R^2$, and minimizing $|z|$ means moving toward the origin — the point of zero cost and zero debt.

The contrast with scalarisation is complete:

| Aspect | Scalarisation $c + \mu d$ | Complex $|z|$ |

|--------|--------------------------|---------------|

| Weighting | $\mu$ is arbitrary | No weights |

| Level sets | Lines | Circles |

| Trade-off | Determined by $\mu$ | Determined by geometry |

| Parameters | One ($\mu$) | Zero |

0.4.4 The Phase as Exploration-Exploitation Angle

Definition 0.8 (Phase). The phase of the complex utility is:

\theta = \arg(z) = \arctan\left(\frac{d}{c}\right).

The phase measures the instantaneous balance between cost and debt. When $\theta = 0$, debt is zero and the agent is in pure exploitation mode. When $\theta$ is large, debt dominates and the agent is in exploration mode. When $\theta < 0$, the agent is actively paying down debt — gaining information at a cost.

As the agent learns, debt decreases and $\theta$ decreases from exploration toward exploitation. This transition is automatic. No external schedule is required. No annealing is needed. The geometry drives it.

0.4.5 The HST Equilibrium Axiom

This book is grounded in Humble Systems Theory (HST), which provides the overarching framework for the complex approach.

Axiom 0.1 (HST Equilibrium Axiom). Every Information Processing System evolves toward epistemic equilibrium — a state of minimum computational cost subject to informational constraints.

At epistemic equilibrium, the system has no remaining epistemic debt: $d = 0$ for all relevant quantities. It acts as a pure cost minimizer. It has achieved the minimum possible computational cost given its environment.

The Equilibrium Axiom implies that the transition from exploration to exploitation is not something that must be engineered — it is the natural trajectory of any information processing system. The modulus-greedy policy:

\pi_Q(s) = \arg\min_{a \in \mathcal{A}} |Q(s,a)|

automatically shifts from exploring when debt is large to exploiting when debt is small. The geometry of $\mathbb{C}$ does the work.

0.4.6 The Complex MDP

The geometric insight leads to a complete framework. The Complex MDP is:

\mathcal{M} = (\mathcal{S}, \mathcal{A}, p, z, \lambda),

where $z = c + id$ replaces the scalar reward. The complex return is:

G_t = \sum_{k=0}^{\infty} \lambda^k z(S_{t+k}, A_{t+k}, S_{t+k+1}) \in \mathbb{C}.

The complex value functions are:

V^\pi(s) = \mathbb{E}^\pi[G_t \mid S_t = s] \in \mathbb{C}, \qquad Q^\pi(s,a) = \mathbb{E}^\pi[G_t \mid S_t = s, A_t = a] \in \mathbb{C}.

The performance criterion is $J^\pi(s) = |V^\pi(s)|$. The agent seeks to minimize this for all states — to reach the origin of the cost-debt plane.

0.5 Why Complex Numbers Are Not Arbitrary

0.5.1 The Uniqueness of $\mathbb{C}$

A natural question arises: why complex numbers? Why not vectors, quaternions, or some other structure? The answer is that $\mathbb{C}$ is the unique two-dimensional structure satisfying the properties we need.

Theorem 0.3 (Frobenius, 1877). Any two-dimensional real algebra that is a field is isomorphic to $\mathbb{C}$.

The alternatives fail:

· Split-complex numbers $a + bj$ with $j^2 = 1$ have zero divisors: $(1+j)(1-j) = 0$. They are not a field and admit no compatible norm.
· Dual numbers $a + b\epsilon$ with $\epsilon^2 = 0$ also have zero divisors and are not a field.
· Quaternions are four-dimensional and non-commutative, making them unsuitable for a two-burden framework.

If we require a two-dimensional structure with addition, multiplication, and a compatible norm, $\mathbb{C}$ is the only choice. It is not arbitrary — it is mathematically forced.

0.5.2 Comparison with Other Representations

We now compare complex numbers with the principal alternatives for encoding cost and debt. The comparison is organized around the structural properties that the framework requires: a natural multiplication, a compatible norm, an intrinsic phase, and a rich analytic theory.

1. Two-dimensional vectors $(c, d) \in \mathbb{R}^2$:

Aspect Vector Representation Complex Representation
Addition Component-wise Component-wise
Multiplication No natural multiplication Natural multiplication
Distance Ad hoc (Euclidean norm) Modulus (natural)
Phase No phase concept Phase has algebraic meaning
Algebraic structure Vector space only Field
Analytic functions Not applicable Rich theory

Advantages of vectors: Simple and intuitive; component-wise operations are straightforward.

Disadvantages of vectors: No natural multiplication (the dot product produces a scalar, not a vector; the cross product is undefined in two dimensions). The Euclidean norm is one of many possible norms — its selection requires justification. No phase or angle concept with algebraic meaning. No analytic function theory.

2. Complex numbers $c + id$:

Aspect Complex Representation
Addition Component-wise
Multiplication $(a+ib)(c+id) = (ac-bd) + i(ad+bc)$
Distance Modulus $\|z\| = \sqrt{c^2 + d^2}$ (natural)
Phase $\theta = \arg(z)$ (meaningful)
Algebraic structure Field
Analytic functions Rich theory (holomorphic functions, conformal maps)

Advantages of complex numbers: Natural multiplication that interacts with the geometry. Modulus is the unique compatible norm. Phase has a clear interpretation (exploration-exploitation angle). Rich mathematical theory (complex analysis, conformal mappings, contour integration).

Disadvantages of complex numbers: Requires familiarity with complex analysis. Multiplication may not have an intuitive physical interpretation in all contexts.

3. Split-complex numbers $a + bj$, $j^2 = 1$:

These have zero divisors: $(1+j)(1-j) = 0$. They are not a field, admit no compatible norm, and have no natural phase. They are unsuitable.

4. Dual numbers $a + b\epsilon$, $\epsilon^2 = 0$:

These also have zero divisors and are not a field. They are unsuitable.

5. Quaternions $q = a + bi + cj + dk$:

Aspect Quaternion Representation
Dimension Four-dimensional
Multiplication Non-commutative
Distance Norm (Euclidean)
Phase Ambiguous (multiple angles)

Advantages: Can represent rotations in 3D; rich algebraic structure.

Disadvantages: Overkill for two burdens. Non-commutativity complicates operations. Phase ambiguity (multiple angles). Not a field (non-commutative division algebra).

6. Matrices:

Aspect Matrix Representation
Dimension Any (including 2×2)
Multiplication Matrix multiplication
Distance Various matrix norms
Phase Not naturally defined

Advantages: Very general; can represent many operations.

Disadvantages: Too general — loses the specific structure we need. No natural phase interpretation. Many matrix norms to choose from (ad hoc).

7. Tensors:

Aspect Tensor Representation
Dimension Multi-dimensional
Multiplication Various tensor products
Distance Various norms
Phase Not naturally defined

Advantages: Can represent high-dimensional structures; flexible.

Disadvantages: Too complex for our purposes. No natural metric or phase. Computationally expensive.

Summary Comparison:

Representation Dimension Field? Norm Phase Natural
Vector 2 No Ad hoc No No
Complex 2 Yes Natural Yes Yes
Split-complex 2 No No No No
Dual 2 No No No No
Quaternion 4 No (non-commutative) Natural Ambiguous No
Matrix Variable No Ad hoc No No
Tensor Variable No Ad hoc No No

Conclusion. The complex numbers are the unique two-dimensional algebra that is a field with a compatible norm and a natural phase interpretation. They are the only representation that satisfies all our requirements.

0.5.3 Why Complex Numbers Are Better Than Vectors

The difference between complex numbers and vectors is not merely semantic — it is structural.

1. Multiplication.

Vectors do not have a natural multiplication. The dot product $c_1 c_2 + d_1 d_2$ produces a scalar, not another vector. The cross product is not defined in two dimensions.

Complex numbers have natural multiplication:

(c_1 + id_1)(c_2 + id_2) = (c_1 c_2 - d_1 d_2) + i(c_1 d_2 + d_1 c_2).

This multiplication has geometric meaning: it rotates and scales in the complex plane. If $z_1 = r_1 e^{i\theta_1}$ and $z_2 = r_2 e^{i\theta_2}$, then $z_1 z_2 = r_1 r_2 e^{i(\theta_1 + \theta_2)}$.

2. The norm.

For vectors, the Euclidean norm $\sqrt{c^2 + d^2}$ is one of many possible norms (Manhattan, supremum, etc.). Why choose Euclidean?

For complex numbers, the modulus $|z| = \sqrt{c^2 + d^2}$ is the unique norm that satisfies:

· Multiplicativity: $|z_1 z_2| = |z_1||z_2|$.
· Triangle inequality: $|z_1 + z_2| \leq |z_1| + |z_2|$.
· Compatibility with the field structure.

The modulus is not arbitrary — it is the natural norm on the complex numbers.

3. The phase.

Vectors can have an angle, but it is defined using trigonometric functions: $\theta = \arctan(d/c)$. This is an external definition.

Complex numbers have an intrinsic phase: $z = |z| e^{i\theta}$. The phase is part of the algebraic structure, not an external addition.

4. Analytic functions.

Vectors do not support a theory of analytic functions. Complex numbers support holomorphic functions, conformal mappings, contour integration, and the rich theory of complex analysis.

5. Algebraic closure.

The complex numbers are algebraically closed — every polynomial has a root in $\mathbb{C}$. Vectors do not have this property.

Complex numbers are not just vectors with a special notation. They are a different kind of structure — a field with a compatible norm, a natural phase, and a rich analytic theory. The complex plane is not the same as $\mathbb{R}^2$ with a dot product.

0.5.4 The Role of the Modulus in a Field

The modulus plays a special role because it is compatible with the field structure of $\mathbb{C}$:

· Multiplicativity: $|z_1 z_2| = |z_1||z_2|$.
· Triangle inequality: $|z_1 + z_2| \leq |z_1| + |z_2|$.
· Positive definiteness: $|z| \geq 0$, with equality if and only if $z = 0$.

These properties are not available for an arbitrary choice of norm on $\mathbb{R}^2$. They follow from the field structure of $\mathbb{C}$ and underpin the contraction properties of the complex Bellman operators developed in subsequent chapters.

0.5.5 The Geometric Meaning of Complex Operations

Every operation on complex numbers has a direct interpretation in the cost-debt plane:

Operation Formula Meaning
Addition $(c_1 + c_2) + i(d_1 + d_2)$ Combining burdens
Conjugation $c - id$ Reflection across the real axis
Modulus $\sqrt{c^2 + d^2}$ Total burden
Phase $\arctan(d/c)$ Exploration angle
Multiplication Rotation and scaling Composing utilities

This correspondence is not imposed on the complex numbers — it emerges from their structure. The algebra and the geometry are the same thing.

0.6 The Landscape of Related Work

0.6.1 Multi-Objective Reinforcement Learning

Multi-Objective Reinforcement Learning (MORL) extends classical RL to problems with vector-valued rewards $\mathbf{r}: \mathcal{S} \times \mathcal{A} \to \mathbb{R}^n$. The main approaches — linear scalarisation, lexicographic ordering, Pareto-based methods, and threshold-based methods — all require choosing parameters. The complex framework eliminates these parameters by recognizing that cost and debt are not two objectives to be weighted but two components of a single geometric object.

The key distinction is that MORL treats the trade-off as a design choice made by the system's designer. The complex framework treats it as a geometric fact determined by the structure of the problem.

0.6.2 Information-Theoretic Reinforcement Learning

Information-theoretic approaches use entropy, mutual information, or KL divergence to guide exploration. Information-directed sampling minimizes an information ratio that implicitly requires tuning. Maximum entropy RL adds an entropy bonus $\beta \mathcal{H}(\pi)$ with a temperature parameter $\beta$ that must be chosen and is environment-dependent.

The complex framework provides a parameter-free alternative. The imaginary component $Q_I$ naturally encodes information value, and the modulus $|Q|$ automatically balances cost minimization and debt reduction. Exploration is not incentivized by a bonus — it emerges from the geometry.

0.6.3 Complex-Valued Neural Networks

Complex-valued neural networks use complex numbers as computational building blocks, with applications in signal processing and deep learning. These approaches focus on representation learning — using complex arithmetic to improve the expressiveness of neural networks.

The complex framework developed in this book is different in purpose. It uses complex numbers not for representation but for decision-making: to define the objective, the value functions, the Bellman operators, and the policy. The theoretical foundation — complex MDPs, complex Bellman equations, epistemic equilibrium — has no counterpart in the CVNN literature.

0.6.4 Humble Systems Theory

Humble Systems Theory is the overarching framework that unifies the approach developed in this book. Its central claim is that every information processing system is naturally driven toward epistemic equilibrium by the geometry of its problem space. Cost and debt are the two fundamental burdens. The complex plane is the natural setting. Exploration and exploitation are not behaviors to be engineered — they are phases of a single geometric process.

The present chapter has established the foundations of this framework: the failure of scalarisation, the geometric alternative, the uniqueness of $\mathbb{C}$, and the connection to prior work. The remaining chapters develop the theory in full.

0.7 Summary

In this chapter, we have established the core problem that motivates this book:

1. Two Fundamental Burdens. Every adaptive agent faces both real cost ($c$) and information debt ($d$). These are qualitatively different — cost is additive, path-dependent, irreversible, and non-negative; debt is conservative, path-independent, reversible, and sign-unrestricted.
2. The Failure of Scalarisation. Classical RL attempts to combine these burdens into a single scalar reward $r = c + \mu d$. This introduces a free parameter $\mu$ that must be tuned.
3. The Free Parameter Problem. No single $\mu$ works across all environments, tasks, or states (Theorem 0.2). This is a fundamental limitation, not a practical nuisance.
4. A Geometric Alternative. Encoding cost and debt as the real and imaginary parts of a complex number $z = c + id$ eliminates the free parameter. Minimizing the modulus $|z| = \sqrt{c^2 + d^2}$ is principled, parameter-free, and geometrically natural.
5. The Uniqueness of $\mathbb{C}$. Complex numbers are the unique two-dimensional real algebra that is a field with a compatible norm (Frobenius). They are not an arbitrary choice among alternatives; vectors, split-complex numbers, dual numbers, quaternions, matrices, and tensors each fail one or more of the required properties.
6. The HST Framework. The HST Equilibrium Axiom asserts that all information processors evolve toward epistemic equilibrium — a state of zero debt. The transition from exploration to exploitation is automatic, driven by geometry.

The remaining chapters develop the complex framework in full: the complex MDP, the complex Bellman equations, the telescoping identity, the mutual information interpretation, and the epistemic equilibrium results.

0.8 Exercises

Exercise 0.1 (Cost vs. Debt). Give three real-world examples of systems that face both cost and debt. For each, identify what constitutes real cost, what constitutes information debt, and how they interact.

Exercise 0.2 (The Free Parameter Problem). Consider an environment where cost is 10 times larger than debt. What weight $\mu$ would be needed to balance them? What if the environment changes and debt becomes 10 times larger? Show that no fixed $\mu$ works.

Exercise 0.3 (Break-Even Threshold). Derive the general break-even threshold $\mu^* = \frac{C(\pi^d) - C(\pi^c)}{D(\pi^c) - D(\pi^d)}$ for two policies with $C(\pi^c) < C(\pi^d)$ and $D(\pi^c) > D(\pi^d)$.

Exercise 0.4 (Complex Utility). For each of the following actions, compute the complex utility $z$, the modulus $|z|$, and the phase $\theta$: (a) $c = 3, d = 4$; (b) $c = 4, d = -3$; (c) $c = 5, d = 0$; (d) $c = 0, d = -5$. Plot these points in the cost-debt plane. Which action has the smallest modulus?

Exercise 0.5 (Level Sets). Draw the level sets of the modulus $|z| = R$ for $R = 1, 2, 3$ in the cost-debt plane. Draw the level sets of the scalarisation $c + \mu d = \text{constant}$ for $\mu = 0.5, 1, 2$. Compare the shapes. Why does the geometry of the modulus avoid the free parameter problem?

Exercise 0.6 (The Phase). For the complex utility $z = c + id$, explain in your own words what $\theta = 0$ means, what $\theta = \pi/2$ means, what $\theta < 0$ means, and how $\theta$ changes as an agent learns.

Exercise 0.7 (Why Not Vectors?). Explain why two-dimensional vectors $(c, d)$ are insufficient for our purposes. What operations are missing? What aspects of the complex framework cannot be reproduced with vectors?

Exercise 0.8 (Split-Complex and Dual Numbers). Split-complex numbers are of the form $a + bj$ with $j^2 = 1$; dual numbers are of the form $a + b\epsilon$ with $\epsilon^2 = 0$. Show that both have zero divisors. Why does this make them unsuitable for our framework?

Exercise 0.9 (Modulus Multiplicativity). Prove that $|z_1 z_2| = |z_1||z_2|$ for complex numbers. Why is this property important for the contraction properties of the Bellman evaluation operator?

Exercise 0.10 (Modulus-Greedy Policy). Consider four actions with $Q$-values: $Q_1 = 5 + 0i$, $Q_2 = 4 + 3i$, $Q_3 = 3 + 4i$, $Q_4 = 0 + 5i$. Which action does the modulus-greedy policy select? Which action would scalarisation with $\mu = 1$ select? Which action would be selected for different $\mu$ values?

Exercise 0.11 (Why Not Quaternions?). Quaternions are a four-dimensional division algebra. Why would quaternions be overkill for encoding cost and debt? What problems arise from non-commutativity?

0.9 Further Reading

· Sutton, R. S. & Barto, A. G. (2018). Reinforcement Learning: An Introduction, 2nd ed. MIT Press. — The standard textbook on RL, covering the scalar reward assumption and its limitations.
· Roijers, D. M., Vamplew, P., Whiteson, S., & Dazeley, R. (2013). "A Survey of Multi-Objective Sequential Decision-Making." Journal of Artificial Intelligence Research, 48:67–113. — A comprehensive survey of multi-objective RL and its parameter dependence.
· Russo, D. & Van Roy, B. (2018). "Learning to Optimize with Information-Directed Sampling." Operations Research, 66(1):230–252. — Information-directed sampling and the exploration-exploitation trade-off with explicit parameters.
· Landauer, R. (1961). "Irreversibility and Heat Generation in the Computing Process." IBM Journal of Research and Development, 5(3):183–191. — The physical cost of computation, relevant to real cost $c$.
· Needham, T. (1997). Visual Complex Analysis. Oxford University Press. — An accessible and visually-oriented introduction to complex analysis.
· Ahlfors, L. V. (1979). Complex Analysis, 3rd ed. McGraw-Hill. — The classic textbook on complex analysis.
· Baez, J. C. (2002). "The Octonions." Bulletin of the American Mathematical Society, 39(2):145–205. — A comprehensive treatment of division algebras, including the classification theorem.
· Amari, S. (2016). Information Geometry and Its Applications. Springer. — The standard reference on information geometry, relevant to the natural-gradient interpretation of the complex framework.
· Hirose, A. (2012). Complex-Valued Neural Networks, 2nd ed. Springer. — Comprehensive treatment of complex-valued neural networks, relevant background for the representation side of the framework.