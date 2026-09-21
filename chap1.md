# Chapter 1 — Why Scalar Cost Is Inadequate

*(Revised with exercises)*

## 1.1 The collapse

Consider a system that must choose among actions. Each action carries a cost. In the classical formulation, the cost is a real number, and the system minimizes it.

This is a complete description of the system's objective, under one condition: that the cost is the only thing the system cares about. If the system cares about a second quantity as well — say, the amount of information it acquires, or the tension between its current model and its world — then the classical formulation must combine the two into a single scalar before minimization can proceed.

The combination is a weighted sum:
$$\text{total cost} = c + \mu \, d,$$
where $c$ is the energetic cost, $d$ is the second quantity, and $\mu > 0$ is a weight.

The weight $\mu$ is not given by the system. It is chosen. It is chosen by the designer, or by a schedule, or by a meta-learning procedure. The choice of $\mu$ determines the system's behavior: a small $\mu$ means the system cares mostly about $c$; a large $\mu$ means it cares mostly about $d$. Different values of $\mu$ select different points on the Pareto frontier between the two objectives.

## 1.2 What the collapse loses

The weighted sum $c + \mu\, d$ is a real number. It is a point on a line. The system's choice, under this objective, is determined by the position of that point.

But the two quantities $c$ and $d$ are geometrically distinct. The cost $c$ is non-negative: doing anything costs something, and doing nothing costs zero. The debt $d$ is signed: the system can move toward or away from a state of lower tension, and the sign of $d$ matters.

A system with low cost and rising debt is in a different situation from a system with high cost and falling debt. The scalar $c + \mu\, d$ cannot distinguish them if the numbers happen to coincide. The information about *direction* — the sign of $d$, the relationship between $c$ and $d$ — is lost.

Formally, the scalar objective is a map from the two-dimensional space of $(c, d)$ to the real line. Such a map cannot be injective. The image is one-dimensional; the preimage of a generic point is a line. Information is destroyed.

## 1.3 A better objective

A natural alternative is to keep the two components separate and minimize a function of both. The Euclidean norm is the canonical choice:
$$|z| = \sqrt{c^2 + d^2}, \qquad z = c + i\, d.$$

The modulus is a map from $\mathbb{C}$ to $\mathbb{R}_{\ge 0}$. It is not injective either — it loses the argument — but it loses less. In particular, it preserves the distinction between transitions with different magnitudes, and it preserves the distinction between transitions with the same cost but different debts, up to a sign.

The modulus has a geometric interpretation: it is the distance from the origin in the complex plane. The system's objective is to be as close to the origin as possible in the $(c, d)$-plane. This is a two-dimensional minimization problem, and it selects a specific point on the Pareto frontier — the point closest to the origin in the Euclidean sense.

## 1.4 The trade-off is not eliminated

It must be stated clearly: the modulus does not eliminate the trade-off between $c$ and $d$. The trade-off is real. A system can pay more cost to reduce debt, or accept more debt to save cost. The set of achievable $(c, d)$ pairs is a curve, and moving along it involves trading one for the other.

What the modulus does is select a specific point on this curve. The point is canonical: it is the point closest to the origin. It is determined by the shape of the curve, which is a property of the environment and the system's capabilities, not by an external parameter.

This is the correct statement of the framework's claim. It is not "the trade-off is eliminated." It is "the trade-off is resolved by geometry, without a free parameter."

## 1.5 What the framework requires

The framework requires three things.

**A configuration space.** A set $\mathcal{B}$ of states, with a notion of transition between them. The states may be physical configurations, or belief states, or any other representation of the system's situation.

**A cost function.** A real, non-negative function $c : \mathcal{B} \times \mathcal{B} \to \mathbb{R}_{\ge 0}$ assigning an energetic cost to each transition.

**A potential.** A real function $\phi : \mathcal{B} \to \mathbb{R}$ on state space. The debt of a transition is the potential difference:
$$d(b, b') = \phi(b') - \phi(b).$$

The complex utility of a transition is $z = c + i\, d$. The system minimizes $|z|$.

The framework does not specify what the potential means. That is a semantic choice, made by the user. Three readings are available:

- **Physical:** $\phi$ is a physical potential (energy, height). The debt is mechanical energy difference.
- **Information-theoretic:** $\phi = -H(\Theta \mid \cdot)$, negative conditional entropy of a latent variable. The debt is expected information gain.
- **Epistemic:** $\phi$ is a general measure of the system's tension. The debt is the direction of the system's approach to or departure from a state of better fit.

The algebra is the same for all three. The interpretations differ.

## 1.6 What the framework is not

Three negatives, for clarity.

**It is not a reward-free framework.** The framework as stated uses a cost function, not a reward. But reward can be reintroduced as a subtraction from the cost: $z = \max(0, c - r) + i\,d$. This is a legitimate extension, but it changes the framework's character: the real part is no longer a pure cost but a net cost, and the convergence theory for the max operator is not yet developed. The framework's reward-free character is a simplification, not a prohibition.

**It is not a claim to derive information from geometry.** The mutual-information interpretation of the imaginary part (Chapter 3) is a *semantic assumption*, not a theorem. The algebra permits the interpretation; it does not force it. The framework is honest about this.

**It is not a solution to the exploration-exploitation problem in general.** The framework provides an automatic exploration-exploitation transition under the HST Equilibrium Axiom (Chapter 13). Whether the axiom holds for a given system is an empirical question. The framework does not guarantee the transition; it provides the structure in which the transition can occur.

## 1.7 The structure of the book

The rest of the book develops the consequences of this framework.

**Chapter 2** defines the complex quasi-metric and proves its basic properties. **Chapter 3** develops the potential-difference form and proves the telescoping identity, non-negativity, and the mutual-information interpretation. **Chapter 4** introduces the $\gamma$-family and proves the triangle inequality for all $\gamma \in [0, 1]$. **Chapter 5** develops the bitopological structure of asymmetric spaces. **Chapter 6** proves the equilibrium hierarchy.

**Part III** applies the framework to reinforcement learning. **Chapter 7** establishes the complex Bellman equation and the evaluation contraction. **Chapter 8** analyses the optimality operator and states the contraction gap. **Chapter 9** introduces the two-selector formulation and examines its status. **Chapter 10** develops the complex policy gradient theorem.

**Part IV** develops the equilibrium theory. **Chapter 11** studies fixed points. **Chapter 12** establishes the Lyapunov structure. **Chapter 13** discusses the HST Equilibrium Axiom.

**Part V** is the inventory.

Each chapter states its theorems formally, with proofs where proofs are available. Where a result is conditional, the conditions are stated. Where a result is conjectural, it is labelled as such.

## Exercises

**Exercise 1.1.** Suppose a system has three available actions, with costs $(c, d)$ given by $(1, 0)$, $(0, 2)$, and $(1, 1)$. Compute the modulus of each. Which action does the modulus criterion select?

**Exercise 1.2.** For the same system, compute the scalar objective $c + \mu d$ for $\mu = 0.5$, $\mu = 1$, and $\mu = 2$. Which action is selected in each case? Show that different values of $\mu$ select different actions.

**Exercise 1.3.** Consider two actions with costs $z_1 = 3 + 4i$ and $z_2 = 4 + 3i$. Compute the modulus of each. Does the modulus criterion distinguish them? If not, what does it lose?

**Exercise 1.4.** Prove that for any two actions with costs $(c_1, d_1)$ and $(c_2, d_2)$, if $c_1 + \mu d_1 < c_2 + \mu d_2$ for all $\mu > 0$, then $c_1 < c_2$ and $d_1 < d_2$. Conclude that the scalar objective can only rank actions consistently if one dominates the other in both components.

**Exercise 1.5.** Give an example of two actions where the modulus criterion and the scalar objective with $\mu = 1$ select different actions. Compute both and verify.

**Exercise 1.6.** Suppose the potential is $\phi(b) = b^2$ on $\mathcal{B} = \mathbb{R}$, and the cost is $c(b, b') = |b' - b|$. Compute the complex utility $z(b, b')$ for a transition from $b = 0$ to $b' = 1$. What is $|z|$?

**Exercise 1.7.** For the same potential and cost, compute the complex utility for the reverse transition, from $b = 1$ to $b' = 0$. Compare with the forward transition. Is the complex utility symmetric? Is the cost? Is the debt?

**Exercise 1.8 (Discussion).** The framework's central claim is that the modulus criterion selects a *canonical* point on the Pareto frontier, whereas the scalar objective requires choosing $\mu$. Is "canonical" the same as "correct"? Write a short paragraph arguing either side. What would it mean for the modulus criterion to be the "right" choice?

**Exercise 1.9 (Discussion).** The framework requires three inputs: a configuration space, a cost function, and a potential. Two of these (space and cost) are also required by classical RL. The potential is new. In what sense is the potential "given" by the system, and in what sense is it a modeling choice? Give an example of a system where the potential is unambiguous, and an example where it is not.

**Exercise 1.10 (Open).** The framework as presented uses a real-valued potential. Could the potential itself be complex-valued? What would that mean? Would the algebra of Chapters 2–3 still hold? (This is an open question; there is no expected answer.)
