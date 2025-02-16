## Exercise 1
Let $A, B \subseteq \mathbb{N}$. Define the notion of reducibility $A \leq_m B$. Prove whether it is true that if $A$ is recursive and $B$ is finite, non-empty then $A \leq_m B$. Analyze the case without the finiteness hypothesis for $B$.

**Solution**: 

First, let us formally define many-one reducibility: A set $A$ reduces to a set $B$ (written $A \leq_m B$) if there exists a total computable function $f: \mathbb{N} \to \mathbb{N}$ such that for all $x \in \mathbb{N}$: $x \in A \iff f(x) \in B$

For the first case, we prove that with $B$ finite and non-empty, the property does not hold by constructing a counterexample:

Let $A = \mathbb{N}\setminus{0}$ (recursive) and $B = {1}$ (finite, non-empty). Assume by contradiction that $A \leq_m B$ through some reduction function $f$. Then:

- For all $x \in A$, $f(x) = 1$ (since $B = {1}$)
- For all $x \not\in A$, $f(x) \neq 1$ This contradicts the fact that $f$ must be total, as $\overline{B}$ is infinite.

For the general case, we can restore the property by requiring $B$ to be recursive. Then for any recursive $A$, we can construct a reduction:

$f(x) = \begin{cases} \mu y.(y \in B) & \text{if }x \in A \\ \mu y.(y \not\in B) & \text{if }x \not\in A \end{cases}$

This $f$ is computable since:

1. $A$ is recursive so $\chi_A$ is computable
2. $B$ being recursive means both $B$ and $\overline{B}$ are r.e., allowing us to compute the minima

## Exercise 2
State the second recursion theorem and use it to prove that for every $k ≥ 0$ there exist two indices $x, y ∈ ℕ$ such that $x - y = k$ and $φ_x = φ_y$.

**Solution:**

The Second Recursion Theorem states that for any total computable function $h: \mathbb{N} \to \mathbb{N}$, there exists $e \in \mathbb{N}$ such that: $\phi_e = \phi_{h(e)}$

To prove the claim, let $k \geq 0$ and define: $h(x) = x - k$

This function is total and computable. By the Second Recursion Theorem, there exists $e \in \mathbb{N}$ such that: $\phi_e = \phi_{h(e)} = \phi_{e-k}$

Let $x = e$ and $y = e-k$. Then:

1. $x - y = e - (e-k) = k$
2. $\phi_x = \phi_e = \phi_{e-k} = \phi_y$

Therefore, we have found indices satisfying both required conditions.

## Exercise 3

Given two functions $f,g : \mathbb{N} \to \mathbb{N}$, with $f$ total, define the predicate $Q_{f,g}(x) \equiv \ "f(x) = g(x)"$. Show that if $f$ and $g$ are computable then $Q_{f,g}$ is semidecidable. Does the converse hold, i.e., if $Q_{f,g}$ is semidecidable can we deduce that $f$ and $g$ are computable?

**Solution**: 

Let $f$ and $g$ be computable functions. Then:

1. First part: Let's prove that $Q_{f,g}$ is semidecidable.
    - Since $f$ and $g$ are computable, there exist indices $e_1, e_2$ such that $f = \phi_{e_1}$ and $g = \phi_{e_2}$
    - The semi-characteristic function of $Q_{f,g}$ can be written as: $sc_{Q_{f,g}}(x) = \begin{cases} 1 & \text{if } f(x) = g(x) \\ \uparrow & \text{otherwise} \end{cases}$
    - This is equivalent to $sc_{Q_{f,g}}(x) = 1(\mu z.|f(x) - g(x)|)$
    - Since $f$ and $g$ are computable, this is computable by composition
    - Therefore $Q_{f,g}$ is semidecidable
2. Second part: The converse does not hold. Let's provide a counterexample:
    - Let $f(x) = x$ (which is computable)
    - Let $g(x) = \begin{cases} x & \text{if } x \in K \\ \uparrow & \text{otherwise} \end{cases}$
    - Then $Q_{f,g}$ is semidecidable as it coincides with the halting problem $K$
    - However, $g$ is not computable as it would solve the halting problem

## Exercise 4

Let $\mathbb{P} = \{2k \ | \ k \in \mathbb{N}\}$ be the set of even numbers. Study the recursiveness of the set $A = \{x \in \mathbb{N} : |W_x \cap \mathbb{P}| \geq 2\}$, i.e., determine if $A$ and $\bar{A}$ are recursive/recursively enumerable.

**Solution**: 
Let us study the recursiveness of $A = \{x \in \mathbb{N} : |W_x \cap \mathbb{P}| \geq 2\}$.

First, we'll show that $A$ is r.e. by constructing its semi-characteristic function:

$sc_A(x) = 1(\mu w. (H(x, 2(w)_1, (w)_3) \wedge H(x, 2(w)_2, (w)_4) \wedge (w)_1 \neq (w)_2))$

This function searches for two different even numbers in $W_x$ by:
1. Finding two numbers $(w)_1$ and $(w)_2$ 
2. Multiplying them by 2 to ensure they're even
3. Verifying that both are in $W_x$ (using the H predicate)
4. Checking they are different $((w)_1 \neq (w)_2)$

Since this function is computable (being composed of computable functions), $A$ is r.e.

Furthermore, $A$ is not recursive. We can prove this by showing that $K \leq_m A$. Consider the function:

$g(x,y) = \begin{cases} 0 & \text{if } x \in K \text{ and } y = 0 \\ 2 & \text{if } x \in K \text{ and } y = 1 \\ \uparrow & \text{otherwise} \end{cases}$

This function is computable since $g(x,y) = (2y + 2) \cdot sc_K(x)$. By the s-m-n theorem, there exists a total computable function $s$ such that $\phi_{s(x)}(y) = g(x,y)$ for all $x,y \in \mathbb{N}$.

Then $s$ is a reduction function for $K \leq_m A$ because:
- If $x \in K$, then $W_{s(x)} = \{0,2\}$, so $|W_{s(x)} \cap \mathbb{P}| = 2$, hence $s(x) \in A$
- If $x \notin K$, then $W_{s(x)} = \emptyset$, so $|W_{s(x)} \cap \mathbb{P}| = 0$, hence $s(x) \notin A$

Since $A$ is r.e. but not recursive, $\bar{A}$ cannot be r.e. (otherwise $A$ would be recursive).

Therefore:
- $A$ is r.e. but not recursive
- $\bar{A}$ is not r.e.

## Exercise 5

State the second recursion theorem and use it to prove that the set $B = \{x \in \mathbb{N} : |W_x| = x + 1\}$ is not saturated.

**Solution**: 

1. Second Recursion Theorem: For any total computable function $f: \mathbb{N} \to \mathbb{N}$, there exists $e_0 \in \mathbb{N}$ such that $\phi_{e_0} = \phi_{f(e_0)}$
2. To prove $B$ is not saturated:
    - Let's define a function $g(x,y) = \begin{cases} 0 & \text{if } y \leq x \ \uparrow & \text{otherwise} \end{cases}$
    - By s-m-n theorem, there exists a computable function $s$ such that $\phi_{s(x)}(y) = g(x,y)$
    - By the second recursion theorem, there exists $e$ such that $\phi_e = \phi_{s(e)}$
    - Therefore $|W_e| = e + 1$, so $e \in B$
    - However, there exists $e' \neq e$ such that $\phi_e = \phi_{e'}$ (since every computable function has infinitely many indices)
    - But $|W_{e'}| = e + 1 \neq e' + 1$, so $e' \notin B$
    - Therefore $B$ is not saturated

## Exercise 6

Let $A, B \subseteq \mathbb{N}$. Define the notion of reducibility $A \leq_m B$. Consider the set $S_4 = \{4 * n \ | \ n \in \mathbb{N}\}$, i.e., the set of multiples of 4. Prove that $A$ is recursive if $A \leq_m S_4$.

**Solution**: 

1. First, recall that $A \leq_m B$ means there exists a total computable function $f: \mathbb{N} \to \mathbb{N}$ such that $\forall x \in \mathbb{N}: x \in A \iff f(x) \in B$
2. Let's prove that if $A \leq_m S_4$ then $A$ is recursive:
    - $S_4$ is recursive since its characteristic function is: $\chi_{S_4}(x) = \begin{cases} 1 & \text{if } 4 | x \ 0 & \text{otherwise} \end{cases}$
    - Let $f$ be the reduction function $A \leq_m S_4$
    - Then $\chi_A(x) = \chi_{S_4}(f(x))$
    - Since both $f$ and $\chi_{S_4}$ are computable, $\chi_A$ is computable
    - Therefore $A$ is recursive

## Exercise 7

Study the recursiveness of the set $A = \{x \in \mathbb{N} : \exists y \in W_x.\exists z \in E_x.x = y + z\}$, i.e., determine if $A$ and $\bar{A}$ are recursive/recursively enumerable.

**Solution**: 

- First, let's prove that $K \leq_m A$, showing that $A$ is not recursive:
    - Define $g(x,y) = \begin{cases} 1 & \text{if } x \in K \\ \uparrow & \text{otherwise} \end{cases}$
    - By s-m-n theorem, there exists total computable $s$ such that $\phi_{s(x)}(y) = g(x,y)$
    - Then:
        - $x \in K \implies W_{s(x)} = \mathbb{N} \land E_{s(x)} = {1} \implies s(x) \in A$
        - $x \notin K \implies W_{s(x)} = \emptyset \implies s(x) \notin A$
    - Therefore $K \leq_m A$, so $A$ is not recursive
- $A$ is r.e. since:
    - Its semi-characteristic function is: $sc_A(x) = 1(\mu w.(H(x,(w)_1,(w)_3) \land S(x,(w)_2,(w)_1+(w)_2,(w)_3)))$
- Since $A$ is r.e. but not recursive, $\bar{A}$ cannot be r.e.

## Exercise 8

Study the recursiveness of the set $B = \{x \in \mathbb{N} : W_x \cup E_x = \mathbb{N}\}$, i.e., determine if $B$ and $\bar{B}$ are recursive/recursively enumerable.

**Solution**: 

- $B$ is saturated since $B = \{x | \phi_x \in \mathcal{B}\}$ where $\mathcal{B} = \{f \in \mathcal{C} | dom(f) \cup cod(f) = \mathbb{N}\}$
- By Rice-Shapiro theorem:
    - $B$ is not r.e. because:
        - The identity function $id \in B$ since $dom(id) = cod(id) = \mathbb{N}$
        - No finite subfunction $\theta \subseteq id$ can be in $B$ since $dom(\theta) \cup cod(\theta)$ is finite
    - $\bar{B}$ is not r.e. because:
        - $\emptyset \in \bar{B}$
        - $\emptyset \subseteq id$ but $id \in B$
- Therefore, neither $B$ nor $\bar{B}$ are recursive.

## Exercise 9

Let $A, B \subseteq \mathbb{N}$ such that $\bar{A}$ is finite and $B \neq \emptyset,\mathbb{N}$. Prove that $A \leq_m B$.

**Solution**: 

Let $\bar{A} = {a_1,...,a_n}$ be finite and let $b \in B, c \notin B$. Define:

$f(x) = \begin{cases} c & \text{if } x \in {a_1,...,a_n} \\ b & \text{otherwise} \end{cases}$

1. $f$ is computable since $\bar{A}$ is finite
2. $f$ is total by definition
3. For all $x \in \mathbb{N}$:
    - $x \in A \iff x \notin \bar{A} \iff f(x) = b \in B$
    - $x \notin A \iff x \in \bar{A} \iff f(x) = c \notin B$

Therefore $A \leq_m B$.

## Exercise 10

Consider the set $A = \{x \ | \ W_x = E_x \cup {0}\}$. We need to establish if $A$ and $\bar{A}$ are recursive/recursively enumerable.

**Solution**: 

Let's observe that $A$ is saturated since $A = \{x \ | \ \phi_x \in A\}$ where $A = \{f \ | \ dom(f) = cod(f) \cup {0}\}$.

By Rice-Shapiro's theorem, we can prove that both $A$ and $\bar{A}$ are not r.e., and thus not recursive:

1. $A$ is not r.e.:
    - Consider the identity function $id \notin A$, since $dom(id) = \mathbb{N} \neq \mathbb{N} \cup {0} = cod(id) \cup {0}$
    - However, the empty function $\emptyset \subseteq id$ belongs to $A$, since $dom(\emptyset) = \emptyset = \emptyset \cup {0} = cod(\emptyset) \cup {0}$
    - Therefore, by Rice-Shapiro's theorem, $A$ is not r.e.
2. $\bar{A}$ is not r.e.:
    - If we take $f = {(0,0)}$, we have $f \notin \bar{A}$ since $dom(f) = {0} = {0} \cup {0} = cod(f) \cup {0}$
    - However, consider $g = {(0,1)} \subseteq f$. Then $g \in \bar{A}$ since $dom(g) = {0} \neq {1} \cup {0} = cod(g) \cup {0}$
    - Therefore, by Rice-Shapiro's theorem, $\bar{A}$ is not r.e.
## Exercise 11

Consider the set $B = \{x \in \mathbb{N} \ | \ 4x + 1 \in E_x\}$. We need to establish if $B$ and $\bar{B}$ are recursive/recursively enumerable.

**Solution**: 

We will prove that $B$ is not recursive by showing $K \leq_m B$.

Let us define: $$ g(x,y) = \begin{cases} 4x + 1 & \text{if } x \in K \\ \uparrow & \text{otherwise} \end{cases} $$

$g$ is computable since $g(x,y) = (4x + 1) \cdot 1(\Psi_U(x,x))$

By the s-m-n theorem, there exists $s: \mathbb{N} \rightarrow \mathbb{N}$ computable and total such that: $$\phi_{s(x)}(y) = g(x,y)\ \forall x,y$$

Then $s$ is a reduction function for $K \leq_m B$ since:

- If $x \in K$: $\phi_{s(x)}(y) = 4x + 1$ thus $4x + 1 \in E_{s(x)}$ and therefore $s(x) \in B$
- If $x \notin K$: $\phi_{s(x)}(y) \uparrow$ for all $y$, thus $E_{s(x)} = \emptyset$ and therefore $s(x) \notin B$

$B$ is r.e. since its semi-characteristic function is computable: $$sc_B(x) = 1(\mu(y,t).S(x,y,4x+1,t))$$

Since $B$ is r.e. but not recursive, by the complementation theorem we can conclude that $\bar{B}$ is not r.e.
## Exercise 12

Show that for any $k \geq 2$, the function $sum_k: \mathbb{N}^k \rightarrow \mathbb{N}$ defined by $sum_k(x_1,\ldots,x_k) = \sum_{i=1}^k x_i$ is primitive recursive.

**Solution**: 

First recall that the class of primitive recursive functions $\mathcal{PR}$ is the smallest class containing:

1. Zero function: $z: \mathbb{N}^k \rightarrow \mathbb{N}, z(x_1,\ldots,x_k) = 0$
2. Successor function: $s: \mathbb{N} \rightarrow \mathbb{N}, s(x) = x + 1$
3. Projections: $U^k_i: \mathbb{N}^k \rightarrow \mathbb{N}, U^k_i(x_1,\ldots,x_k) = x_i$

And closed under:

- Composition
- Primitive recursion

For $k = 2$, we can define $sum_2$ by primitive recursion: $$ \begin{align*} sum_2(x_1,0) &= x_1 \\ sum_2(x_1,x_2+1) &= s(sum_2(x_1,x_2)) \end{align*} $$

For $k > 2$, we can define inductively: $$sum_k(x_1,\ldots,x_k) = sum_2(sum_{k-1}(x_1,\ldots,x_{k-1}), x_k)$$

Since composition preserves primitive recursiveness and $sum_2 \in \mathcal{PR}$, by induction we have $sum_k \in \mathcal{PR}$ for all $k \geq 2$.
## Exercise 13

Given a function $f: \mathbb{N} \rightarrow \mathbb{N}$, define: $Z(f) = {g: \mathbb{N} \rightarrow \mathbb{N} | \forall x \in \mathbb{N}. g(x) = f(x) \vee g(x) = 0}$

Show that $Z(id)$ is not enumerable, where $id$ is the identity function. Is it true for all functions $f$ that $Z(f)$ is not enumerable?

**Solution**: 

To prove $Z(id)$ is not enumerable, we proceed by contradiction. Assume $Z(id)$ is enumerable. Then there would exist a surjective function $f: \mathbb{N} \rightarrow Z(id)$.

We can construct a bijective correspondence between $\mathcal{P}(\mathbb{N})$ and $Z(id)$ by defining $h: Z(id) \rightarrow \mathcal{P}(\mathbb{N})$ as: $$h(g) = \{x \in \mathbb{N} \ | \ g(x) = 0\}$$

For any $g \in Z(id)$, $h$ uniquely constructs the set $D \subseteq \mathbb{N}$ where: $$g(x) = \begin{cases} 0 & \text{if } x \in D\ x & \text{if } x \notin D \end{cases}$$

At this point, we can define a surjective function $\bar{g}: \mathbb{N} \rightarrow \mathcal{P}(\mathbb{N})$ as: $$\bar{g} = h \circ f$$

This would imply $\mathcal{P}(\mathbb{N})$ is enumerable, which contradicts Cantor's theorem. Therefore, $Z(id)$ cannot be enumerable.

This property does not hold for all functions. For $f = 0$ (constant zero function): $$Z(0) = {0}$$ which is a finite set and thus enumerable. In general, $Z(f)$ is enumerable if and only if $f = 0$.
## Exercise 14

Consider $A = \{x \ | \ W_x \subseteq {x}\}$. We need to establish if $A$ and $\bar{A}$ are recursive/recursively enumerable.

**Solution**: 

Let's show that $K \leq_m A$. Define: $$g(x,y) = \begin{cases} x & \text{if } x \in K \\ \uparrow & \text{otherwise} \end{cases}$$

By s-m-n theorem, $\exists s: \mathbb{N} \rightarrow \mathbb{N}$ computable and total such that $\phi_{s(x)}(y) = g(x,y)$. Then:

- If $x \in K$: $W_{s(x)} = {x}$, thus $s(x) \in A$
- If $x \notin K$: $W_{s(x)} = \emptyset \subseteq {s(x)}$, thus $s(x) \notin A$

Therefore $A$ is not recursive. However, $A$ is r.e. since: $$sc_A(x) = 1(\mu w.H(x,w) \land (w = x))$$
Thus $\bar{A}$ is not r.e.
## Exercise 15

Consider the set $B = \{x \in \mathbb{N} : |W_x| > 1\}$. We need to establish if $B$ and $\bar{B}$ are recursive/recursively enumerable.

**Solution**: 

First, observe that $B$ is saturated since $B = \{x \ | \ \phi_x \in B\}$ where $B = {f \in C : |dom(f)| > 1}$. Using Rice-Shapiro's theorem, we can prove that both $B$ and $\bar{B}$ are not r.e.

For $B$ not r.e.: Consider the constant function $\textbf{1}(x) = 1$. Then $\textbf{1} \notin B$ since $|dom(\textbf{1})| = 1$. However, if we consider the finite function: $$\theta(x) = \begin{cases} 1 & \text{if } x \leq 1 \\ \uparrow & \text{otherwise} \end{cases}$$ We have that $\theta \subseteq c_1$ and $\theta \in B$ since $|dom(\theta)| = 2$. Therefore, by Rice-Shapiro's theorem, $B$ is not r.e.

For $\bar{B}$ not r.e.: Consider $\theta$ as defined above. Then $\theta \notin \bar{B}$. However, the empty function $\emptyset \subseteq \theta$ and $\emptyset \in \bar{B}$ since $|dom(\emptyset)| = 0 \leq 1$. Therefore, by Rice-Shapiro's theorem, $\bar{B}$ is not r.e.
## Exercise 16

State the s-m-n theorem and use it to prove that there exists a total computable function $s: \mathbb{N} \rightarrow \mathbb{N}$ such that $|W_{s(x)}| = 2x$ and $|E_{s(x)}| = x$.

**Solution**: 

First, let us define: $$g(x,y) = \begin{cases} y/2 & \text{if } y < 2x \\ \uparrow & \text{otherwise} \end{cases}$$

This function is computable since: $$g(x,y) = \frac{y}{2} + \mu z.\text{sg}(2x - y)$$

By the s-m-n theorem, there exists a total computable function $s: \mathbb{N} \rightarrow \mathbb{N}$ such that: $$\phi_{s(x)}(y) = g(x,y)$$

Therefore:

1. $W_{s(x)} = {y | y < 2x}$, thus $|W_{s(x)}| = 2x$
2. $E_{s(x)} = \{y/2 \ | \ y < 2x\} = \{z \ | \ z < x\}$, thus $|E_{s(x)}| = x$
## Exercise 17

State the Second Recursion Theorem and use it to show there exists some $x \in \mathbb{N}$ s.t. $\varphi_x(y)=y^x, \forall y \in \mathbb{N}$

**Solution**: 

By the Second Recursion Theorem, for any total computable function $h: \mathbb{N} \rightarrow \mathbb{N}$, there exists $e_0 \in \mathbb{N}$ such that $\phi_{e_0} = \phi_{h(e_0)}$.

Let us define: $$g(n,y) = y^n$$

By the s-m-n theorem, there exists a total computable function $s: \mathbb{N} \rightarrow \mathbb{N}$ such that: $$\phi_{s(n)}(y) = g(n,y) = y^n$$

Applying the Second Recursion Theorem to $s$, there exists $x \in \mathbb{N}$ such that: $$\phi_x = \phi_{s(x)}$$

Therefore: $$\phi_x(y) = \phi_{s(x)}(y) = y^x \text{ for all } y \in \mathbb{N}$$
## Exercise 18

Prove that $F = \{\theta \mid \theta : \mathbb{N} \to \mathbb{N} \land \text{dom}(\theta) \text{ finite}\}$ (unary functions with finite domain) set is countable.

**Solution**: 
For any finite function θ ∈ F, we can encode it uniquely as a natural number using the following encoding:

$\widetilde{\theta} = \prod_{i=1}^n p_{x_i+1}^{y_i+1}$

where:

- ${(x_1,y_1),...,(x_n,y_n)}$ represents the input-output pairs of θ
- $p_i$ represents the i-th prime number

Given an encoding z = $\widetilde{\theta}$:

- $x ∈ dom(θ)$ iff $(z)_{x+1} \neq 0$
- $θ(x) =$ $(z)_{x+1} - 1$ when $x ∈ dom(θ)$

This encoding is:

1. Injective (each finite function has a unique encoding)
2. Computable (we can effectively compute the encoding and decoding)

Therefore, we have established a one-to-one correspondence between $F$ and a subset of $\mathbb{N}$, proving that $F$ is countable.
## Exercise 19

Study the recursiveness of $B = \{x \mid \phi_x(x)\downarrow \land \ \phi_x(x) \text{ odd}\}$

**Solution**: 

We show that $K ≤_m B$ to prove B is not recursive.

Define $g(x,y)$ as: $g(x,y) = \begin{cases} 1 & \text{if } x \in K \\ \uparrow & \text{otherwise} \end{cases}$

By the s-m-n theorem, there exists $s : \mathbb{N} → \mathbb{N}$ total computable such that: $φ_s(x)(y) = g(x,y)$

Then s is a reduction function $K ≤_m B$ since:

- $x ∈ K ⇒ φ_s(x)(s(x))↓ \ = 1 (odd) ⇒ s(x) ∈ B$
- $x ∉ K ⇒ φ_s(x)(s(x))↑ \ ⇒ s(x) ∉ B$

Therefore:

1. $B$ is not recursive
2. $B$ is r.e. since $sc_B(x) = 1(φ_x(x)) · sg(mod(φ_x(x),2))$
3. $B̄$ is not r.e. (otherwise $B$ would be recursive)
## Exercise 20

State the Second Recursion Theorem and use it to show there exists some $x \in \mathbb{N}$ s.t. $|W_x|=x$

**Solution**: 

By the Second Recursion Theorem, for any total computable $f : \mathbb{N} \to \mathbb{N}$, there exists $e \in \mathbb{N}$ such that $\phi_e = \phi_{f(e)}$.

Define: $h(x,y) = \begin{cases} x & \text{if } y \leq |W_x| \\ \uparrow & \text{otherwise} \end{cases}$

By s-m-n theorem, $\exists s$ total computable such that $\phi_{s(x)}(y) = h(x,y)$.

By Second Recursion Theorem, $\exists e$ such that: $\phi_e = \phi_{s(e)}$

Therefore $|W_e| = e$, proving the existence of such $e$.
## Exercise 21

Define the class of primitive recursive functions. Using only the definition, show that the function $f : \mathbb{N} \to \mathbb{N}$ defined by $f(y) = 2y + 1$ is primitive recursive.

**Solution**: 

First, let us recall that the class $PR$ of primitive recursive functions is the smallest class containing:

Base functions:

1. Zero function: $z(x) = 0$
2. Successor function: $s(x) = x + 1$
3. Projection functions: $U^k_i(x_1,...,x_k) = x_i$

And closed under:

1. Composition
2. Primitive recursion

To show $f(y) = 2y + 1$ is primitive recursive, we can construct it using only these operations:

1. Define $double(y)$ by primitive recursion: $\begin{cases} double(0) = 0 \\ double(y+1) = double(y) + 2 = s(s(double(y))) \end{cases}$
2. Then $f(y) = s(double(y))$

Therefore, $f$ is primitive recursive as it is constructed using only composition and primitive recursion from the base functions.
## Exercise 22

Classify the following set from the point of view of recursiveness $A = \{x \mid W_x \cap E_x \supseteq {0}\}$, i.e., establish if $A$ and $\overline{A}$ are recursive/recursively enumerable.

**Solution**: 

$A$ is saturated since $A = \{x \mid \phi_x \in A\}$ where $A = \{f \mid 0 \in dom(f) \cap cod(f)\}$.

Let's prove $K \leq_m A$. Define: $g(x,y) = \begin{cases} 0 & \text{if } x \in K \\ \uparrow & \text{otherwise} \end{cases}$

By s-m-n theorem, $\exists s : \mathbb{N} \to \mathbb{N}$ total computable such that $\phi_{s(x)}(y) = g(x,y)$.

Then:

- $x \in K \implies \phi_{s(x)}(0) = 0 \implies 0 \in W_{s(x)} \cap E_{s(x)} \implies s(x) \in A$
- $x \notin K \implies \phi_{s(x)}(0)\uparrow \implies 0 \notin W_{s(x)} \cap E_{s(x)} \implies s(x) \notin A$

Therefore:

1. $A$ is not recursive
2. $A$ is r.e. since $sc_A(x) = 1(\mu y.(H(x,0,y) \land S(x,0,0,y)))$
3. $\overline{A}$ is not r.e.
## Exercise 23

Classify the following set from the point of view of recursiveness $B = \{x \in \mathbb{N} \mid \exists y. \phi_x(y) = x + 1\}$, i.e., establish if $B$ and $\overline{B}$ are recursive/recursively enumerable. Also establish if $B$ is saturated.

**Solution**: 

First, let's prove $B$ is r.e. Its semi-characteristic function is: $sc_B(x) = 1(\mu w.(S(x,(\omega)_1,x+1,(\omega)_2)))$

Now let's show $K \leq_m B$. Define: $g(x,y) = \begin{cases} s(x) & \text{if } x \in K \\ \uparrow & \text{otherwise} \end{cases}$

By s-m-n theorem, $\exists s$ total computable such that $\phi_{s(x)}(y) = g(x,y)$.

Then:

- $x \in K \implies \phi_{s(x)}(0) = x + 1 \implies s(x) \in B$
- $x \notin K \implies \phi_{s(x)}(y)\uparrow \text{ for all } y \implies s(x) \notin B$

Therefore:

1. $B$ is not recursive
2. $B$ is r.e.
3. $\overline{B}$ is not r.e.

For saturation: Define by Second Recursion Theorem an index $e$ such that: $\phi_e(y) = \begin{cases} e + 1 & \text{if } y = e \\ \uparrow & \text{otherwise} \end{cases}$

Then $e \in B$. Let $e' \neq e$ such that $\phi_{e'} = \phi_e$. Then $\phi_{e'}(e') = \phi_e(e') \uparrow$, hence $e' \notin B$. Therefore $B$ is not saturated.
## Exercise 24

State the s-m-n theorem. Use it to prove that there exists a total computable function $k : \mathbb{N} \to \mathbb{N}$ such that for all $x,y \in \mathbb{N}$ it holds that $\phi_{k(x)}(y) = lcm(x,y)$, where $lcm$ is the least common multiple of $x$ and $y$.

**Solution**: 
First, let's state the s-m-n theorem: For any $m,n \geq 1$, there exists a total computable function $s^m_n : \mathbb{N}^{m+1} \to \mathbb{N}$ such that for all $e \in \mathbb{N}, \vec{x} \in \mathbb{N}^m, \vec{y} \in \mathbb{N}^n$: $\phi^{(m+n)}_e(\vec{x},\vec{y}) = \phi^{(n)}_{s^m_n(e,\vec{x})}(\vec{y})$

To prove the existence of $k$, define: $f(x,y) = \mu z \leq x \cdot y.(x|z \land y|z)$

Then $f$ is computable since: $f(x,y) = \mu z \leq x \cdot y.(\overline{sg}(div(x,z)) \cdot \overline{sg}(div(y,z)))$

By the s-m-n theorem, there exists $k : \mathbb{N} \to \mathbb{N}$ total computable such that: $\phi_{k(x)}(y) = f(x,y) = lcm(x,y)$
## Exercise 25

Classify the following set from the point of view of recursiveness $A = {x \mid W_x \cup E_x \subseteq \mathbb{P}}$, where $\mathbb{P}$ is the set of even numbers, i.e., establish if $A$ and $\overline{A}$ are recursive/recursively enumerable.

**Solution**: $A$ is saturated since $A = \{x \mid \phi_x \in A\}$ where $A = \{f \mid dom(f) \cup cod(f) \subseteq \mathbb{P}\}$.

Let's prove $\overline{K} \leq_m A$. Define: $g(x,y) = \begin{cases} 0 & \text{if } x \in \overline{K} \\ 1 & \text{otherwise} \end{cases}$

By s-m-n theorem, $\exists s$ total computable such that $\phi_{s(x)}(y) = g(x,y)$.

Then:

- $x \in \overline{K} \implies \phi_{s(x)}(y) = 0 \implies W_{s(x)} \cup E_{s(x)} \subseteq \mathbb{P} \implies s(x) \in A$
- $x \notin \overline{K} \implies \phi_{s(x)}(y) = 1 \implies W_{s(x)} \cup E_{s(x)} \not\subseteq \mathbb{P} \implies s(x) \notin A$

Therefore:

1. $A$ is not r.e.
2. $\overline{A}$ is r.e. since $sc_{\overline{A}}(x) = 1(\mu w.(H(x,(\omega)_1,(\omega)_2) \land odd((\omega)_1) \lor S(x,(\omega)_1,(\omega)_2,(\omega)_3) \land odd((\omega)_2)))$
## Exercise 26

Classify $B = \{x \in \mathbb{N} \mid 2x + 1 \in W_x\}$ from the point of view of recursiveness, i.e., establish if $B$ and $\overline{B}$ are recursive/recursively enumerable. Also establish if $B$ is saturated.

**Solution**: 

First, $B$ is r.e. since: $sc_B(x) = 1(\mu w.H(x,2x+1,w))$

Let's prove $K \leq_m B$. Define: $g(x,y) = \begin{cases} 1 & \text{if } y = 2s(x)+1 \land x \in K \ \uparrow & \text{otherwise} \end{cases}$

By s-m-n theorem, $\exists s$ total computable such that $\phi_{s(x)}(y) = g(x,y)$.

Then:

- $x \in K \implies 2s(x)+1 \in W_{s(x)} \implies s(x) \in B$
- $x \notin K \implies W_{s(x)} = \emptyset \implies 2s(x)+1 \notin W_{s(x)} \implies s(x) \notin B$

Therefore:

1. $B$ is not recursive
2. $B$ is r.e.
3. $\overline{B}$ is not r.e.

For saturation: Define by Second Recursion Theorem an index $e$ such that: $\phi_e(y) = \begin{cases} 1 & \text{if } y = 2e+1 \\ \uparrow & \text{otherwise} \end{cases}$

Then $e \in B$. Let $e' \neq e$ such that $\phi_{e'} = \phi_e$. Then $2e'+1 \notin W_{e'} = {2e+1}$, hence $e' \notin B$. Therefore $B$ is not saturated.
## Exercise 27

Let us study the recursiveness of the set

$B = \{x \mid k \cdot (x+1) \in W_x \cap E_x \text{ for all } k \in \mathbb{N}\}$

In other words, determine if $B$ and $\bar{B}$ are recursive/recursively enumerable.

**Solution:**

Let us prove that set $B$ is not recursive by showing that $K \leq_m B$. We will then prove that $B$ is recursively enumerable, which will imply that $\bar{B}$ is not recursively enumerable.

We show that $K \leq_m B$ by constructing a computable reduction function. Let us define:

$g(x,y) = \begin{cases} 1 & \text{if } x \in K \\ \uparrow & \text{otherwise} \end{cases}$

This function is computable since $g(x,y) = sc_K(x)$. By the smn theorem, there exists a total computable function $s: \mathbb{N} \rightarrow \mathbb{N}$ such that $\phi_{s(x)}(y) = g(x,y)$ for all $x,y \in \mathbb{N}$.

We shall prove that $s$ is a reduction function for $K \leq_m B$:

1. If $x \in K$, then:
    - $\phi_{s(x)}(y) = 1$ for all $y \in \mathbb{N}$
    - Therefore $W_{s(x)} = E_{s(x)} = \mathbb{N}$
    - Thus for all $k$, $k(s(x)+1) \in W_{s(x)} \cap E_{s(x)}$
    - Hence $s(x) \in B$
2. If $x \notin K$, then:
    - $\phi_{s(x)}(y) \uparrow$ for all $y \in \mathbb{N}$
    - Therefore $W_{s(x)} = E_{s(x)} = \emptyset$
    - Thus no $k(s(x)+1)$ can be in $W_{s(x)} \cap E_{s(x)}$
    - Hence $s(x) \notin B$

$B$ is recursively enumerable since its semi-characteristic function is computable:

$sc_B(x) = 1(\mu w.(H(x,k\cdot(x+1),(\omega)_2) \wedge S(x,(\omega)_1,k\cdot(x+1),(\omega)_2)))$

where $H$ and $S$ are the standard halting and computation predicates respectively.

Therefore:

- $B$ is recursively enumerable but not recursive
- Since $B$ is not recursive but is r.e., $\bar{B}$ cannot be r.e. (otherwise $B$ would be recursive)
- Thus $\bar{B}$ is not recursively enumerable
## Exercise 28

Does there exist a total non-computable function $f: \mathbb{N} \rightarrow \mathbb{N}$ such that its image $cod(f) = \{y \mid \exists x \in \mathbb{N}. f(x) = y\}$ is finite? Provide an example or prove that such a function does not exist.

**Solution:** Yes, such a function exists. Consider the function:

$f(x) = \begin{cases} \overline{sg}(\phi_x(x)) & \text{if } x \in W_x \\ 0 & \text{if } x \notin W_x \end{cases}$

This function has the following properties:

1. It is total, as it provides a value for every input $x \in \mathbb{N}$.
2. It is not computable because for every $x \in \mathbb{N}$, $f(x) \neq \phi_x(x)$. Specifically:
    - If $\phi_x(x)\downarrow$, then $f(x) = \overline{sg}(\phi_x(x)) \neq \phi_x(x)$
    - If $\phi_x(x)\uparrow$, then $f(x) = 0 \neq \phi_x(x)$
3. By construction, $cod(f) \subseteq {0,1}$, which is clearly finite.
## Exercise 29

State the s-m-n theorem and use it to prove that there exists a total computable function $k: \mathbb{N} \rightarrow \mathbb{N}$ such that $W_{k(n)} = \{x \in \mathbb{N} \mid x \geq n\}$ and $E_{k(n)} = \{y \in \mathbb{N} \mid y \text{ is even}\}$ for all $n \in \mathbb{N}$.

**Solution:** Let us first define a computable function of two arguments $f(n,x)$ that satisfies the conditions when viewed as a function of $x$, with $n$ as a parameter:

$f(n,x) = \begin{cases} 2(x-n) & \text{if } x \geq n \\ \uparrow & \text{otherwise} \end{cases} = 2(x-n) + \mu z.(n-x)$

By the s-m-n theorem, there exists a total computable function $k: \mathbb{N} \rightarrow \mathbb{N}$ such that $\phi_{k(n)}(x) = f(n,x)$ for all $n,x \in \mathbb{N}$. Therefore:

1. $W_{k(n)} = \{x \mid f(n,x)\downarrow\} = \{x \mid x \geq n\}$
2. $E_{k(n)} = {f(n,x) \mid x \in \mathbb{N}} = {2z \mid z \in \mathbb{N}}$

## Exercise 30

State the s-m-n theorem and use it to prove that there exists a total computable function $k: \mathbb{N} \rightarrow \mathbb{N}$ such that for all $n \in \mathbb{N}$, $W_{k(n)} = \{z^n \mid z \in \mathbb{N}\}$ and $E_{k(n)}$ is the set of odd numbers.

**Solution:** Let us define a computable function of two arguments $f(n,x)$ that meets the required conditions:

$f(n,x) = \begin{cases} 2z + 1 & \text{if } x = z^n \text{ for some } z \\ \uparrow & \text{otherwise} \end{cases} = 2 \cdot \mu z.|x - z^n| + 1$

By the s-m-n theorem, there exists a total computable function $k: \mathbb{N} \rightarrow \mathbb{N}$ such that $\phi_{k(n)}(x) = f(n,x)$ for all $n,x \in \mathbb{N}$. Therefore:

1. $W_{k(n)} = \{x \mid f(n,x)\downarrow\} = \{x \mid \exists z \in \mathbb{N}. x = z^n\} = \{z^n \mid z \in \mathbb{N}\}$
2. $E_{k(n)} = \{f(n,x) \mid x \in W_{k(n)}\} = \{2z + 1 \mid z \in \mathbb{N}\}$

## Exercise 31

Do there exist an index $e \in \mathbb{N}$ and a non-computable function $f: \mathbb{N} \rightarrow \mathbb{N}$ such that, denoting by $dom(f)$ and $cod(f)$ the domain and codomain of $f$ respectively (where $dom(f) = {x \mid f(x)\downarrow}$ and $cod(f) = {y \mid \exists x. f(x) = y}$), it holds that $dom(f) = W_e$ and $cod(f) = E_e$? Provide an example or prove non-existence.

Additionally, can such a function $f$ with $dom(f) = W_e$ and $cod(f) = E_e$ be found for every $e \in \mathbb{N}$?

**Solution:** For the first part, consider an index $e \in \mathbb{N}$ of the identity function, where $W_e = E_e = \mathbb{N}$. Define $f: \mathbb{N} \rightarrow \mathbb{N}$ as:

$f(x) = \begin{cases} \phi_x(x) + 1 & \text{if } x \in W_x \\ 0 & \text{otherwise} \end{cases}$

The function $f$ is total, therefore $dom(f) = \mathbb{N} = W_e$. Furthermore, $dom(f) = \mathbb{N} = E_e$. Indeed, for any $n \in \mathbb{N}$:

- If $n = 0$, consider an index $x$ of the always undefined function, then $f(x) = 0$
- If $n > 0$, consider any index $x$ of the constant function $n-1$, then $f(x) = (n-1) + 1 = n$

For the second question, the answer is no. For example, if we consider $e \in \mathbb{N}$ such that $\phi_e$ is the always undefined function, any $f$ such that $dom(f) = W_e = \emptyset$ must coincide with $\phi_e$ and thus would be computable.

## Exercise 32

Provide the definition of the set $\mathcal{PR}$ of primitive recursive functions and prove that the function $cpr: \mathbb{N}^2 \rightarrow \mathbb{N}$ defined as

$cpr(x,y) = |\{p \mid x \leq p < y \wedge p \text{ prime}\}|$

is primitive recursive, where $cpr(x,y)$ counts the number of primes in the interval $[x,y]$.

**Solution:** Let us first define $cpr': \mathbb{N}^2 \rightarrow \mathbb{N}$ such that $cpr'(x,k) = |{p \mid x \leq p < x+k \wedge p \text{ prime}}|$ by primitive recursion:

$cpr'(x,0) = 0$ 
$cpr'(x,k+1) = cpr'(x,k) + \chi_{Pr}(x + k)$

Then $cpr(x,y) = cpr'(x,y-x)$, which as composition of primitive recursive functions is itself primitive recursive.
## Exercise 33

State the s-m-n theorem and use it to prove that there exists a total computable function $s: \mathbb{N} \rightarrow \mathbb{N}$ such that for all $x \in \mathbb{N}$, $W_{s(x)} = \{(k+x)^2 \mid k \in \mathbb{N}\}$.

**Solution:** Define a function $g: \mathbb{N}^2 \rightarrow \mathbb{N}$ such that when viewed as a function of $y$ it has the desired properties:

$g(x,y) = \begin{cases} k & \text{if } \exists k., y = (x+k)^2 \\ \uparrow & \text{otherwise} \end{cases}$

This can be written as $g(x,y) = \mu k.|(x+k)^2 - y|$. This function is computable, therefore by the s-m-n theorem there exists a total computable function $s: \mathbb{N} \rightarrow \mathbb{N}$ such that $\phi_{s(x)}(y) = g(x,y)$ for all $x,y \in \mathbb{N}$.




