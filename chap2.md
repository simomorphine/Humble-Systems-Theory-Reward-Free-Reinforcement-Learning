# Chapter 2 — The Complex Quasi-Metric


## 2.1 Belief space and complex cost

**Definition 2.1.1 (Belief space).** A *belief space* is a set $\mathcal{B}$ equipped with a $\sigma$-algebra $\Sigma$. Elements of $\mathcal{B}$ are called *states* or *beliefs*.

**Remark 2.1.2.** The term "belief space" is used throughout, but the framework does not require $\mathcal{B}$ to consist of probability distributions. A belief space is any set of configurations, and the framework applies to physical state spaces, epistemic state spaces, and more abstract configuration spaces equally.

**Definition 2.1.3 (Complex cost function).** A *complex cost function* on $\mathcal{B}$ is a function
$$Q : \mathcal{B} \times \mathcal{B} \to \mathbb{C}$$
of the form
$$Q(b, b') = c(b, b') + i\, d(b, b'),$$
where $c : \mathcal{B} \times \mathcal{B} \to \mathbb{R}_{\ge 0}$ is a *real cost* and $d : \mathcal{B} \times \mathcal{B} \to \mathbb{R}$ is a *real debt*.

**Remark 2.1.5 (Asymmetry is permitted).** Symmetry is not required. In general $Q(b, b') \neq Q(b', b)$, and both the modulus and the argument may differ. The asymmetry is the central structural feature of the framework (Chapter 5).

**Remark 2.1.6 (The triangle inequality is for the modulus).** Condition (Q3) is the triangle inequality for the modulus $|Q|$. It is weaker than the triangle inequality for the complex-valued function $Q$ itself, which would require $Q(b, b'') = Q(b, b') + Q(b', b'')$ and is not generally true. Throughout the book, "triangle inequality" refers to (Q3) unless stated otherwise.

**Proposition 2.1.7.** The modulus $|Q|$ is a quasi-metric in the classical sense: it satisfies identity, non-negativity, and the triangle inequality. If $Q$ is symmetric ($Q(b, b') = Q(b', b)$ for all $b, b'$), then $|Q|$ is a metric, provided $|Q(b, b')| = 0$ implies $b = b'$.

*Proof.* Identity: $|Q(b, b)| = |0| = 0$. Non-negativity: $|Q(b, b')| \ge 0$. Triangle inequality: (Q3). The symmetry statement is immediate. $\square$

**Remark 2.1.8.** The modulus $|Q|$ loses the argument of $Q$. Two transitions with the same modulus but different arguments are indistinguishable at the level of $|Q|$. This loss is a recurring theme: it is the source of the optimality obstruction in Chapter 8, and it motivates the two-selector formulation of Chapter 9.

## 2.2 The potential-difference form

**Definition 2.2.1 (Epistemic potential).** A function $\phi : \mathcal{B} \to \mathbb{R}$ is an *epistemic potential* on $\mathcal{B}$.

**Definition 2.2.2 (Potential-difference debt).** The debt $d$ takes the *potential-difference form* if there exists a potential $\phi$ such that
$$d(b, b') = \phi(b') - \phi(b)$$
for all $b, b' \in \mathcal{B}$.

**Proposition 2.2.3 (Basic properties).** If $d$ takes the potential-difference form, then:

- (i) *Identity:* $d(b, b) = 0$.
- (ii) *Antisymmetry:* $d(b, b') = -d(b', b)$.
- (iii) *Additivity (telescoping):* $d(b, b'') = d(b, b') + d(b', b'')$ for all $b, b', b''$.
- (iv) *Cycle invariance:* for any $b_1, \ldots, b_n$ with $b_{n+1} = b_1$,
$$\sum_{k=1}^n d(b_k, b_{k+1}) = 0.$$
- (v) *Gauge invariance:* under $\phi \mapsto \phi + c$ for any constant $c \in \mathbb{R}$, $d$ is unchanged.

*Proof.* All follow directly from $d = \phi(b') - \phi(b)$. $\square$

**Proposition 2.2.4 (Characterization).** A function $d : \mathcal{B} \times \mathcal{B} \to \mathbb{R}$ takes the potential-difference form if and only if it satisfies additivity and $d(b, b) = 0$. In that case, the potential is unique up to an additive constant.

*Proof.* ($\Rightarrow$) Proposition 2.2.3. ($\Leftarrow$) Fix $b_0 \in \mathcal{B}$ and define $\phi(b) = d(b_0, b)$. Then
$$\phi(b') - \phi(b) = d(b_0, b') - d(b_0, b) = d(b, b')$$
by additivity and antisymmetry. Uniqueness up to constant follows from gauge invariance. $\square$

**Remark 2.2.5 (The debt is a conservative quantity).** The potential-difference form makes the debt *path-independent*: the total debt incurred along any path depends only on the endpoints. This is the structural distinction between the debt (imaginary part) and the cost (real part). Cost is irreversible and path-dependent; debt is reversible and path-independent.

## 2.3 Metric properties of the modulus

**Proposition 2.3.1 (Reverse triangle inequality).** For any $z_1, z_2 \in \mathbb{C}$,
$$\left| |z_1| - |z_2| \right| \le |z_1 - z_2|.$$

*Proof.* By the triangle inequality, $|z_1| = |z_1 - z_2 + z_2| \le |z_1 - z_2| + |z_2|$, hence $|z_1| - |z_2| \le |z_1 - z_2|$. Interchanging $z_1$ and $z_2$ gives the reverse inequality, and combining yields the stated bound. $\square$

**Proposition 2.3.2 (Modulus of expectation).** For any $\mathbb{C}$-valued random variable $Z$ with $\mathbb{E}[|Z|] < \infty$,
$$|\mathbb{E}[Z]| \le \mathbb{E}[|Z|].$$

*Proof.* This is Jensen's inequality applied to the convex function $|\cdot| : \mathbb{C} \to \mathbb{R}_{\ge 0}$. $\square$

**Remark 2.3.3 (Equality condition).** The inequality in Proposition 2.3.2 is strict unless $Z$ has constant argument almost surely (i.e. $Z$ is a.s. a positive real multiple of its expectation). This condition appears repeatedly in the book, notably in the Lyapunov analysis of Chapter 12.

**Proposition 2.3.4 (Continuity of the modulus).** The map $z \mapsto |z|$ is Lipschitz with constant $1$: for any $z_1, z_2 \in \mathbb{C}$, $||z_1| - |z_2|| \le |z_1 - z_2|$.

*Proof.* Proposition 2.3.1. $\square$

## 2.4 The $\gamma$-distance family

**Definition 2.4.1 ($\gamma$-distance).** For $\gamma \in [0, 1]$, the $\gamma$-*distance* is

$$d_\gamma(b, b') = \sqrt{c(b, b')^2 + \gamma^2 \, d(b, b')^2}.$$

**Proposition 2.4.2 (Basic properties).** For every $\gamma \in [0, 1]$:

- (i) $d_\gamma(b, b) = 0$ for all $b$.
- (ii) $d_\gamma(b, b') \ge 0$ for all $b, b'$.
- (iii) $d_\gamma$ satisfies the triangle inequality.

*Proof.* (i) and (ii) are immediate from the definition. For (iii), see Proposition 2.4.3 below. $\square$

**Proposition 2.4.3 (Triangle inequality for $d_\gamma$).** For every $\gamma \in [0, 1]$,
$$d_\gamma(b, b'') \le d_\gamma(b, b') + d_\gamma(b', b'').$$

*Proof.* By definition, $d_\gamma(b, b'') = \|(c(b, b''), \gamma\, d(b, b''))\|_2$, where $\|\cdot\|_2$ is the Euclidean norm on $\mathbb{R}^2$.

By the triangle inequality for $c$ and for $|d|$ (which follow from the generalized triangle inequality (Q3) with $\gamma = 1$),
$$c(b, b'') \le c(b, b') + c(b', b''),$$
$$|d(b, b'')| \le |d(b, b')| + |d(b', b'')|.$$

Apply Minkowski's inequality to the vectors

$$u = (c(b, b'), \gamma\, d(b, b')), \qquad v = (c(b', b''), \gamma\, d(b', b'')).$$

Minkowski's inequality gives $\|u + v\|_2 \le \|u\|_2 + \|v\|_2$. The first component of $u + v$ is $c(b, b') + c(b', b'') \ge c(b, b'')$, and the second component is $\gamma(d(b, b') + d(b', b''))$, whose absolute value dominates $\gamma |d(b, b'')|$. Hence

$$\|(c(b, b''), \gamma\, d(b, b''))\|_2 \le \|u + v\|_2 \le \|u\|_2 + \|v\|_2 = d_\gamma(b, b') + d_\gamma(b', b''). \qquad \square$$

**Corollary 2.4.4 (Endpoints).** $d_0(b, b') = c(b, b')$ (pure cost) and $d_1(b, b') = |Q(b, b')|$ (full modulus).

**Remark 2.4.5 (The $\gamma$-family interpolates).** As $\gamma$ increases from $0$ to $1$, the $\gamma$-distance interpolates continuously between the cost-only geometry and the full complex-modulus geometry. The interpolation is not linear: it is a continuous deformation of the metric on state space.

## 2.5 Summary

The complex quasi-metric $Q = c + i\,d$ is a two-component object: a non-negative real part and a signed imaginary part. Its modulus $|Q|$ is a classical quasi-metric. The debt takes the potential-difference form when it is the difference of a real-valued potential; this gives conservativity, antisymmetry, and gauge invariance. The $\gamma$-family interpolates between the cost-only geometry ($\gamma = 0$) and the full complex geometry ($\gamma = 1$), with each $d_\gamma$ a quasi-metric.

The metric properties established in this chapter are the foundation for everything that follows. The triangle inequality for $d_\gamma$ (Proposition 2.4.3) will be used in the evaluation contraction (Chapter 7) and the policy gradient theorem (Chapter 10). The reverse triangle inequality (Proposition 2.3.1) will be used in the optimality analysis (Chapter 8). The modulus of expectation (Proposition 2.3.2) is used throughout.

## Exercises

**Exercise 2.1.** Verify that $Q(b, b') = |b' - b| + i(b' - b)$ is a complex quasi-metric on $\mathcal{B} = \mathbb{R}$. Check each of the axioms (Q1), (Q2), (Q3). Is it symmetric?

**Exercise 2.2.** For the same $Q$, compute $Q(0, 1)$ and $Q(1, 0)$. Verify that $Q(0, 1) \neq Q(1, 0)$. Compute $|Q(0, 1)|$ and $|Q(1, 0)|$. Are they equal?

**Exercise 2.3.** Let $\phi(b) = b^2$ and $c(b, b') = |b' - b|$. Verify that $d(b, b') = \phi(b') - \phi(b)$ takes the potential-difference form. Check properties (i)–(v) of Proposition 2.2.3 for this specific $d$.

**Exercise 2.4.** Prove that the potential-difference form is *not* symmetric in general. Give an explicit example where $d(b, b') \neq d(b', b)$.

**Exercise 2.5.** Let $Q(b, b') = c(b, b') + i\, d(b, b')$ with $c(b, b') = |b' - b|$ and $d(b, b') = b' - b$. Compute $d_\gamma(0, 2)$ for $\gamma = 0$, $\gamma = 1/2$, and $\gamma = 1$.

**Exercise 2.6.** For the same $Q$, verify the triangle inequality (Q3) for the triple $(b, b', b'') = (0, 1, 2)$. Compute $|Q(0, 2)|$, $|Q(0, 1)| + |Q(1, 2)|$, and verify the inequality.

**Exercise 2.7.** Consider the potential $\phi(b) = b^3$ on $\mathcal{B} = \mathbb{R}$. Compute the debt $d(b, b')$ for a transition from $0$ to $1$. Is the debt positive, negative, or zero? What about the reverse transition?

**Exercise 2.8.** Prove the following strengthened version of the reverse triangle inequality: for any $z_1, z_2 \in \mathbb{C}$,
$$|z_1 + z_2| \ge ||z_1| - |z_2||.$$
This is the "other" reverse triangle inequality, used in the proofs of later chapters.

**Exercise 2.9.** Show that Jensen's inequality for the modulus is strict unless the random variable has constant argument. Give an explicit example of a random variable with non-constant argument where the inequality is strict.

**Exercise 2.10.** Let $\phi$ be a bounded potential with $|\phi(b)| \le M$ for all $b$. Compute the bound on $|Q_I^\pi(b, a)|$ in terms of $M$ and $\lambda$. (You may use the telescoping identity from Chapter 3, or derive the bound directly.)

**Exercise 2.11.** Show that if $Q$ is symmetric ($Q(b, b') = Q(b', b)$ for all $b, b'$), then $d_\gamma$ is symmetric for every $\gamma \in [0, 1]$.

**Exercise 2.12.** Show that the converse is false: give an example where $d_\gamma$ is symmetric but $Q$ is not.

**Exercise 2.13 (Discussion).** The $\gamma$-distance interpolates between $d_0 = c$ and $d_1 = |Q|$. What does it mean for a system to have $\gamma = 0.5$? Is there a natural interpretation of intermediate $\gamma$ in terms of the system's behavior? Argue for or against the interpretation of $\gamma$ as "debt sensitivity" (Section 4.4).

**Exercise 2.14 (Open).** The triangle inequality for $d_\gamma$ is proven for all $\gamma \in [0, 1]$. What happens for $\gamma > 1$? Does the triangle inequality still hold? Compute a counterexample or prove the inequality for $\gamma > 1$.

**Exercise 2.15 (Open).** Can the complex quasi-metric framework be generalized to higher dimensions — e.g., quaternions or $n$-dimensional vectors? What would be the analogue of the potential-difference form, and would the telescoping identity (Chapter 3) still hold?
