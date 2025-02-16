
# 1. URM machines
## Exercise 1.7
![[Pasted image 20250103135546.png]]
![[Pasted image 20250104082059.png]]
# 3. Smn-theorem

## Exercise 3.1
![[Pasted image 20250104090814.png]]
![[Pasted image 20250104090931.png]]
![[Pasted image 20250104090952.png]]
![[Pasted image 20250104091000.png]]
![[Pasted image 20250104091015.png]]
![[Pasted image 20250104091028.png]]
## Exercise 3.3
![[Pasted image 20250103135508.png]]

Proof:
The smn theorem states that given computable functions $g:\mathbb{N}^{m+n} \rightarrow \mathbb{N}$ and $h:\mathbb{N}^m \rightarrow \mathbb{N}$, there exists a total computable function $s:\mathbb{N}^{m+1} \rightarrow \mathbb{N}$ such that
$$
\phi_{s(e,\vec{x})}^{(n)}(\vec{y}) = \phi_{e}^{(m+n)}(\vec{x},\vec{y}) = g(h(\vec{x}),\vec{y})
$$
for all $e \in \mathbb{N}$, $\vec{x} \in \mathbb{N}^m$, and $\vec{y} \in \mathbb{N}^n$.

To prove the theorem, we start by defining the function $f:\mathbb{N}^3 \rightarrow \mathbb{N}$ as follows:
$$
f(x,y,z) = \begin{cases} 
      0 & \text{if } x*z=y \\
      \uparrow & \text{otherwise}
   \end{cases}
$$
which can be written in terms of the computable functions product, equality and minimization:
$$f(x,y,z) = \mu w . |x*z - y|$$
Therefore, $f$ is a computable function.

Now, by the smn theorem, there exists a total computable function $s:\mathbb{N}^2 \rightarrow \mathbb{N}$ such that for all $x,y,z \in \mathbb{N}$:
$$\phi_{s(x,y)}(z) = f(x,y,z)$$

We can then conclude that for any $x,y \in \mathbb{N}$:
$$
\begin{align*}
W_{s(x,y)} &= \{z \in \mathbb{N} : \phi_{s(x,y)}(z)\downarrow\} \\
           &= \{z \in \mathbb{N} : f(x,y,z) = 0\} \\
           &= \{z \in \mathbb{N} : x*z=y\}
\end{align*}
$$
which proves the theorem. $\square$
# 6. Functions and Computability
## Exercise 6.13

![[Pasted image 20250103135210.png]]

To prove there exists a total non-computable function $f : \mathbb{N} \rightarrow \mathbb{N}$ such that $f(x) \neq \phi_x(x)$ only on a single argument $x \in \mathbb{N}$, consider the following function:

$$
f(x) = \begin{cases}
\phi_x(x) + 1 & \text{if } \phi_x(x)\downarrow \\
0 & \text{if } \phi_x(x)\uparrow
\end{cases}
$$

This function $f$ is total by definition. Moreover, $f$ differs from every computable function $\phi_x$ on the argument $x$:

- If $\phi_x(x)\downarrow$, then $f(x) = \phi_x(x) + 1 \neq \phi_x(x)$
- If $\phi_x(x)\uparrow$, then $f(x) = 0 \neq \phi_x(x)$

Therefore, $f$ is a total non-computable function that differs from each computable function $\phi_x$ only on the single argument $x$.
## Exercise 6.14

![[Pasted image 20250103135219.png]]
To show that there is no non-computable function $f : \mathbb{N} \rightarrow \mathbb{N}$ such that $f(x) \neq \phi_x(x)$ only on a single $x \in \mathbb{N}$, suppose for contradiction that such an $f$ exists. 

Let $x_0 \in \mathbb{N}$ be the unique value where $f(x_0) \neq \phi_{x_0}(x_0)$. Define a new function $g : \mathbb{N} \rightarrow \mathbb{N}$ as follows:

$$
g(x) = \begin{cases}
f(x) & \text{if } x \neq x_0 \\
\phi_{x_0}(x_0) & \text{if } x = x_0
\end{cases}
$$

Observe that $g$ is computable, since it differs from the non-computable function $f$ only at the single argument $x_0$, where it takes on the computable value $\phi_{x_0}(x_0)$.

However, by construction, $g(x_0) = \phi_{x_0}(x_0)$ and for all $x \neq x_0$, $g(x) = f(x) = \phi_x(x)$. Therefore, $g = \phi_{x_0}$, contradicting the assumption that $f$ differs from every computable function on some argument.

Hence, our initial assumption must be false, and there cannot exist a non-computable function that differs from every computable function on only a single argument.
## Exercise 6.16
![[Pasted image 20250103140446.png]]

To show that there cannot exist a non-computable function $f: \mathbb{N} \to \mathbb{N}$ such that the set $D = \{x \in \mathbb{N} | f(x) \neq \phi_x(x)\}$ is finite, we will prove that the existence of such a function leads to a contradiction.

Suppose for the sake of argument that such a function $f$ exists. Then we can define a new function $g: \mathbb{N} \to \mathbb{N}$ as follows:
$$
g(x) = 
\begin{cases}
f(x) & \text{if } x \notin D \\
f(x)+1 & \text{if } x \in D
\end{cases}
$$

Since $D$ is finite by assumption, $g$ differs from $f$ only on a finite number of inputs. This implies that $g$ is also non-computable, as a finite change to a non-computable function cannot make it computable.

However, by construction, for all $x \in \mathbb{N}$ we have:
- If $x \notin D$, then $g(x) = f(x) \neq \phi_x(x)$, and thus $g \neq \phi_x$
- If $x \in D$, then $g(x) = f(x)+1 \neq f(x) = \phi_x(x)$, and thus $g \neq \phi_x$

Therefore, $g$ differs from every computable function $\phi_x$ on input $x$. By the diagonalization theorem, this implies that $g$ is in fact computable, contradicting our earlier observation that $g$ is non-computable.

We conclude that our initial assumption must be false, i.e., there cannot exist a non-computable function $f: \mathbb{N} \to \mathbb{N}$ such that the set $D = \{x \in \mathbb{N} | f(x) \neq \phi_x(x)\}$ is finite. The function $f$ simply cannot exist under these constraints, as its existence would lead to a logical contradiction.
## Exercise 6.20

![[Pasted image 20250103135256.png]]
Let's analyze the function $f : \mathbb{N} \rightarrow \mathbb{N}$ defined as:

$$
f(x) = \begin{cases}
x + 2 & \text{if } \varphi_x(x)\downarrow \\
x - 1 & \text{otherwise}
\end{cases}
$$

To determine if $f$ is computable, we can express it using the computable functions and operations we know.

First, note that the predicate "$\varphi_x(x)\downarrow$" is equivalent to "$x \in K$", where $K = \{x \mid x \in W_x\}$ is the halting set. We know that $K$ is recursively enumerable (r.e.) but not recursive.

Let's denote the characteristic function of $K$ as $\chi_K$, which is defined as:

$$
\chi_K(x) = \begin{cases}
1 & \text{if } x \in K \\
0 & \text{otherwise}
\end{cases}
$$

Although $\chi_K$ is not computable, we can use it to express $f$:

$$
\begin{align*}
f(x) & = (x + 2) \cdot \chi_K(x) + (x - 1) \cdot (1 - \chi_K(x)) \\
     & = (x + 2) \cdot \chi_K(x) + (x - 1) - (x - 1) \cdot \chi_K(x) \\
     & = x + 2 \cdot \chi_K(x) - 1 + \chi_K(x) \\
     & = x + 3 \cdot \chi_K(x) - 1
\end{align*}
$$

If $\chi_K$ were computable, then $f$ would also be computable as a composition of computable functions. However, since $\chi_K$ is not computable, we cannot conclude that $f$ is computable.

In fact, if $f$ were computable, then we could compute $\chi_K$ using:

$$
\chi_K(x) = \frac{f(x) - x + 1}{3}
$$

But this contradicts the fact that $\chi_K$ is not computable.

Therefore, the function $f$ is not computable.

Similarly, it was solved by an old tutor the following way:
![[Pasted image 20250104082424.png]]
![[Pasted image 20250104082434.png]]

## Exercise 6.21
![[Pasted image 20250103135319.png]]
![[Pasted image 20250103135337.png]]
Assume by contradiction that $f$ is computable. Then there exists an index $e$ such that $f = \phi_e$.

Therefore, for any $x \in \mathbb{N}$:

$$ \phi_e(x) = \begin{cases} \phi_x(x+1) + 1 & \text{if } \phi_x(x+1) \downarrow \\ \uparrow & \text{otherwise} \end{cases} $$

In particular, for $x = e$:

$$ \phi_e(e) = \begin{cases} \phi_e(e+1) + 1 & \text{if } \phi_e(e+1) \downarrow \\ \uparrow & \text{otherwise} \end{cases} $$

Now consider two cases:

1. If $\phi_e(e+1) \downarrow$, then $\phi_e(e) = \phi_e(e+1) + 1 > \phi_e(e+1)$
2. If $\phi_e(e+1) \uparrow$, then $\phi_e(e) \uparrow$

In either case, we cannot have $f = \phi_e$.

**Conclusion:** $f$ is not computable.
## Exercise 6.22
![[Pasted image 20250103135405.png]]
Assume by contradiction that $f$ is computable. Then there exists an index $e$ such that $f = \phi_e$.

Let's consider $x = e$. Then:

1. If $\phi_y(y) \downarrow$ for all $y \leq e$, then: $\phi_e(e) = f(e) = \phi_e(e) + 1$ This is a contradiction as no natural number equals its successor.
2. If there exists some $y \leq e$ such that $\phi_y(y) \uparrow$, then: $\phi_e(e) = f(e) = 0$ This means $\phi_e(e) \downarrow$, contradicting the fact that $\phi_y(y) \uparrow$ for some $y \leq e$.

Therefore, we cannot have $f = \phi_e$ for any $e$.

**Conclusion:** $f$ is not computable.
## 7. Reduction, Recursiveness and Recursive Enumerability

## Exercise 7.11
![[Pasted image 20250104091141.png]]

($\Rightarrow$) First, let's prove if $f$ is computable then $A_f$ is r.e.

If $f$ is computable, then there exists an index $e$ such that $f = \phi_e$. Define:

$$
sc_{A_f}(z) = \mu w.(S(e, (\pi_1(z)), \pi_2(z), (w)_1))
$$

where $\pi_1, \pi_2$ are the projection functions for the pair encoding.

This function is computable because:
- $S$ is decidable (step counting predicate)
- $\pi_1, \pi_2$ are computable
- The minimal search $\mu$ preserves computability

Therefore $A_f$ is r.e.

($\Leftarrow$) Now let's prove if $A_f$ is r.e. then $f$ is computable.

If $A_f$ is r.e., then there exists an index $e$ such that:

$$
A_f = W_e = \{\pi(x, f(x)) | x \in \mathbb{N}\}
$$

We can define $f$ as:

$$
f(x) = \pi_2(\mu z.(z \in W_e \land \pi_1(z) = x))
$$

This function is computable because:
- $W_e$ is r.e.
- $\pi_1, \pi_2$ are computable
- The minimal search $\mu$ is over a semi-decidable predicate
- The equality $\pi_1(z) = x$ is decidable

Therefore $f$ is computable.

**Conclusion:** $f$ is computable if and only if $A_f$ is recursively enumerable.
## Exercise 7.12
![[Pasted image 20250103135637.png]]
($\Rightarrow$) Assume $A$ is recursive. Then its characteristic function $\chi_A$ is computable. Define the reduction function $f : \mathbb{N} \rightarrow \mathbb{N}$ as $f(x) = 1 - \chi_A(x)$. Clearly, $f$ is computable, and $x \in A \Leftrightarrow f(x) = 0 \Leftrightarrow f(x) \in {0}$. Thus, $A \leq_m {0}$.

($\Leftarrow$) Assume $A \leq_m {0}$ via a computable function $f$. Then $x \in A \Leftrightarrow f(x) = 0$. Define $\chi_A(x) = 1 - \operatorname{sg}(f(x))$, where $\operatorname{sg}$ is the signum function. Since $f$ and $\operatorname{sg}$ are computable, $\chi_A$ is computable, and thus $A$ is recursive.
## Exercise 7.13
![[Pasted image 20250103135648.png]]
($\Rightarrow$) Assume $A$ is recursively enumerable. Then there exists a computable function $g : \mathbb{N} \rightarrow \mathbb{N}$ such that $\operatorname{img}(g) = A$. Let $p_i$ denote the $i$-th prime number. Define $f : \mathbb{N} \rightarrow \mathbb{N}$ as $f(p_i) = g(i)$ for all $i \in \mathbb{N}$. Clearly, $\operatorname{dom}(f)$ is the set of prime numbers and $\operatorname{img}(f) = \operatorname{img}(g) = A$.

($\Leftarrow$) Assume there exists a function $f : \mathbb{N} \rightarrow \mathbb{N}$ such that $\operatorname{dom}(f)$ is the set of prime numbers and $\operatorname{img}(f) = A$. Define $g : \mathbb{N} \rightarrow \mathbb{N}$ as $g(i) = f(p_i)$ for all $i \in \mathbb{N}$, where $p_i$ is the $i$-th prime number. Since the sequence of prime numbers is computable, $g$ is computable, and $\operatorname{img}(g) = \operatorname{img}(f) = A$. Thus, $A$ is recursively enumerable.
## Exercise 7.19
![[Pasted image 20250103135703.png]]
($\Rightarrow$) Assume $A$ is recursive. Then its characteristic function $\chi_A$ is computable. Define the semi-characteristic functions $\operatorname{sc}_A(x) = \chi_A(x)$ and $\operatorname{sc}_{\overline{A}}(x) = 1 - \chi_A(x)$. Both are computable, so $A$ and $\overline{A}$ are r.e.

($\Leftarrow$) Assume $A$ and $\overline{A}$ are r.e. Then there exist computable semi-characteristic functions $\operatorname{sc}_A$ and $\operatorname{sc}_{\overline{A}}$. Define the characteristic function $\chi_A(x) = \mu y . [\operatorname{sc}_A(x) = 1 \vee \operatorname{sc}_{\overline{A}}(x) = 1]$. Since $x \in A \cup \overline{A}$ for all $x \in \mathbb{N}$, the minimalization always terminates, and $\chi_A$ is computable. Thus, $A$ is recursive.
## Exercise 7.20
![[Pasted image 20250103135713.png]]
Rice's theorem states that for any non-trivial property of partial computable functions, the set of indices of functions with that property is undecidable.

Formally, let $C$ be the set of all partial computable unary functions and $A \subseteq C$ such that:

1. $A \neq \emptyset$
2. $A \neq C$
3. $A$ is extensional, i.e., if $f, g \in C$ and $f =^* g$ then $f \in A \Leftrightarrow g \in A$, where $f =^* g$ means $f(x) = g(x)$ whenever $f(x)$ and $g(x)$ are both defined.

Then the index set $I_A = {e \in \mathbb{N} \mid \varphi_e \in A}$ is not recursive (i.e., not decidable).
![[Pasted image 20250104082754.png]]
## Exercise 7.21
![[Pasted image 20250103135725.png]]
A set $A \subseteq \mathbb{N}$ is saturated if for all $x, y \in \mathbb{N}$, $\varphi_x = \varphi_y$ implies $x \in A \Leftrightarrow y \in A$.

To prove that $K$ is not saturated, we show there exist $e_1, e_2 \in \mathbb{N}$ such that $\varphi_{e_1} = \varphi_{e_2}$ but $e_1 \in K$ and $e_2 \notin K$.

Consider the computable function $g(x, y) = 1$ if $x = y$, and undefined otherwise. By the $s$-$m$-$n$ theorem, there exists a computable function $s : \mathbb{N} \rightarrow \mathbb{N}$ such that $\varphi_{s(x)}(y) = g(x, y)$ for all $x, y \in \mathbb{N}$.

By the Recursion Theorem, there exists $e$ such that $\varphi_e = \varphi_{s(e)}$. Thus, $\varphi_e(y) = 1$ if $y = e$, and undefined otherwise.

Now, $e \in K$ as $\varphi_e(e) = 1$. Choose any $e' \neq e$ such that $\varphi_{e'} = \varphi_e$. Then $\varphi_{e'}(e') \uparrow$, so $e' \notin K$. Therefore, $K$ is not saturated.
![[Pasted image 20250104082941.png]]
## Exercise 7.22
![[Pasted image 20250103135735.png]]
Proof by contradiction. Assume $I_A$ is r.e. Choose $e_0 \in \mathbb{N}$ such that $\varphi_{e_0}$ is the everywhere undefined function.

Define $g : \mathbb{N}^2 \rightarrow \mathbb{N}$ as:

$$ g(x, y) = \begin{cases} \varphi_{e_0}(y) & \text{if } x \notin K \\ f(y) & \text{if } x \in K \end{cases} $$

Clearly, $g$ is computable. By the $s$-$m$-$n$ theorem, there exists a computable function $s : \mathbb{N} \rightarrow \mathbb{N}$ such that $\varphi_{s(x)}(y) = g(x, y)$ for all $x, y \in \mathbb{N}$.

Now, for any $x \in \mathbb{N}$:

- If $x \notin K$, then $\varphi_{s(x)} = \varphi_{e_0} \notin A$, so $s(x) \notin I_A$.
- If $x \in K$, then $\varphi_{s(x)} = f \in A$, so $s(x) \in I_A$.

Therefore, $x \in K \Leftrightarrow s(x) \in I_A$. Since $K$ is not r.e., this contradicts the assumption that $I_A$ is r.e.
# 8. Characterization of sets
## Exercise 8.1
![[Pasted image 20250103135756.png]]

We will prove that neither $A$ nor $\bar{A}$ are recursively enumerable (r.e.).

1. First, observe that $A$ is saturated since $A = {x | \phi_x \in \mathcal{A}}$ where $\mathcal{A} = {f \in \mathcal{C} : |dom(f)| \geq 2}$.
2. Let's prove $A$ is not r.e. using Rice-Shapiro theorem:
    - Let $id$ be the identity function. Note that $id \notin A$ since $|dom(id)| = \infty \not\geq 2$
    - Define $\theta \subset id$ as: $$\theta(x) = \begin{cases} x & \text{if } x \leq 1 \\ \uparrow & \text{otherwise} \end{cases}$$
    - Then $\theta \subset id$ and $\theta \in A$ since $|dom(\theta)| = 2$
    - By Rice-Shapiro theorem, $A$ is not r.e.
3. Let's prove $\bar{A}$ is not r.e.:
    - Consider $\theta$ as defined above. Clearly $\theta \notin \bar{A}$
    - Let $\emptyset$ be the empty function. Then $\emptyset \subset \theta$ and $\emptyset \in \bar{A}$ since $|dom(\emptyset)| = 0 < 2$
    - By Rice-Shapiro theorem, $\bar{A}$ is not r.e.

Therefore, since neither $A$ nor $\bar{A}$ are r.e., $A$ is not recursive.
## Exercise 8.2

![[Pasted image 20250103135806.png]]
We will prove that $A$ is r.e. but not recursive.

1. First, let's prove $A$ is r.e.:
    - Define the semi-characteristic function: $$sc_A(x) = \begin{cases} 1 & \text{if } x \in W_x \cap E_x \\ \uparrow & \text{otherwise} \end{cases}$$
    - This is computable since: $$sc_A(x) = 1(\mu w.(H(x,x,w) \land S(x,x,x,w)))$$
2. To prove $A$ is not recursive, we show $K \leq_m A$:
    - Define: $$g(x,y) = \begin{cases} x & \text{if } x \in K \\ \uparrow & \text{otherwise} \end{cases}$$
    - By s-m-n theorem, $\exists s$ total computable such that $\forall x,y: \phi_{s(x)}(y) = g(x,y)$
    - Then $s$ is a reduction function because:
        - If $x \in K$: $\phi_{s(x)}(s(x)) = x$ thus $s(x) \in W_{s(x)} \cap E_{s(x)}$, so $s(x) \in A$
        - If $x \notin K$: $\phi_{s(x)}(s(x)) \uparrow$ thus $s(x) \notin W_{s(x)}$, so $s(x) \notin A$

Therefore $A$ is r.e. but not recursive, and consequently $\bar{A}$ is not r.e.
## Exercise 8.5
![[Pasted image 20250103135818.png]]
We'll show that $K \leq_m A$ to prove $A$ is not recursive.

Define a function $g(x,y)$ as: $$g(x,y) = \begin{cases} 2^2 & \text{if } x \in K \\ \uparrow & \text{otherwise} \end{cases}$$
By s-m-n theorem, ∃s total computable such that $\phi_{s(x)}(y) = g(x,y)$. Then s is a reduction function because:

- If $x \in K$ then $s(x) = 4$ which can be written as $2^2$, so $s(x) \in A$
- If $x \notin K$ then $\phi_{s(x)}$ is undefined everywhere, so $s(x) \notin A$

Therefore $A$ is not recursive. However, $A$ is r.e. since: $$sc_A(x) = 1(\mu\langle y,z,w \rangle.(z > 1 \land x = y^z))$$
Given $A$ is r.e. but not recursive, $\bar{A}$ is also not recursive (otherwise both would be recursive) and also r.e.
## Exercise 8.6
![[Pasted image 20250103135827.png]]
The set $A$ is saturated since $A = \{x \ | \ \varphi_x \in \mathcal{A}\}$ where $\mathcal{A} = {f \in \mathcal{C} : f(y) = y \text{ for infinitely many } y}$.

By Rice-Shapiro theorem:

1. $A$ is not r.e.:
    - Let $id$ be the identity function. Then $id \in A$
    - Let $\theta \subset id$ be any finite subfunction. Then $\theta \notin A$
    - By Rice-Shapiro theorem, $A$ is not r.e.
2. $\bar{A}$ is not r.e.:
    - Let $f(x) = x+1$. Then $f \notin A$ (thus $f \in \bar{A}$)
    - Let $\emptyset \subset f$. Then $\emptyset \in A$ (thus $\emptyset \notin \bar{A}$)
    - By Rice-Shapiro theorem, $\bar{A}$ is not r.e.

Therefore $A$ is not recursive.
## Exercise 8.7
![[Pasted image 20250103135839.png]]
The set $A$ is saturated since $A = \{x \ | \ \varphi_x \in \mathcal{A}\}$ where $\mathcal{A} = {f \in \mathcal{C} : dom(f) \subseteq cod(f)}$.

By Rice-Shapiro theorem:

1. $A$ is not r.e.:
    - Let $f(x) = x+1$. Then $f \notin A$ since $\mathbb{N} \not\subseteq \mathbb{N}\setminus{0}$
    - Let $\emptyset$ be the empty function. Then $\emptyset \subset f$ and $\emptyset \in A$
    - By Rice-Shapiro theorem, $A$ is not r.e.
2. $\bar{A}$ is not r.e.:
    - Let $id$ be the identity function. Then $id \in A$, so $id \notin \bar{A}$
    - Let $\theta \subset id$ where $dom(\theta) \not\subseteq cod(\theta)$. Then $\theta \in \bar{A}$
    - By Rice-Shapiro theorem, $\bar{A}$ is not r.e.

Therefore $A$ is not recursive.

This was also solved by prof. Baldan in some older lessons:

![[Pasted image 20250104085312.png]]

![[Pasted image 20250104085326.png]]
## Exercise 8.8
![[Pasted image 20250103135849.png]]
The set $A$ is saturated since $A = \{x \ | \ \phi_x \in \mathcal{A}\}$ where $\mathcal{A} = {f \in \mathcal{C} : |dom(f)| > |cod(f)|}$.

By Rice-Shapiro theorem:

1. $A$ is not r.e.:
    - Let $id$ be the identity function. Then $id \notin A$
    - Let $\theta \subset id$ with $dom(\theta) > cod(\theta)$. Then $\theta \in A$
    - By Rice-Shapiro theorem, $A$ is not r.e.
2. $\bar{A}$ is not r.e.:
    - Let $f$ with finite domain be in $A$. Then $f \notin \bar{A}$
    - Let $\emptyset \subset f$. Then $\emptyset \in \bar{A}$
    - By Rice-Shapiro theorem, $\bar{A}$ is not r.e.

Therefore $A$ is not recursive.
## Exercise 8.12
![[Pasted image 20250103135902.png]]
The set $A$ is saturated since $A = {x | \phi_x \in \mathcal{A}}$ where $\mathcal{A} = {f \in \mathcal{C} : |\mathbb{N} \setminus dom(f)| < \infty}$.

1. Let's prove $A$ is not r.e. using Rice-Shapiro theorem:
    - Let $id$ be the identity function. Then $id \in A$ (since $dom(id) = \mathbb{N}$)
    - Let $\theta \subset id$ be any finite subfunction of $id$. Then $\theta \notin A$ since $|\mathbb{N} \setminus dom(\theta)| = \infty$
    - By Rice-Shapiro theorem, $A$ is not r.e.
2. Let's prove $\bar{A}$ is not r.e.:
    - Let $f \notin A$ (so $f \in \bar{A}$)
    - Let $\emptyset \subset f$ be the empty function. Then $\emptyset \in A$ (so $\emptyset \notin \bar{A}$)
    - By Rice-Shapiro theorem, $\bar{A}$ is not r.e.

Therefore, since neither $A$ nor $\bar{A}$ are r.e., $A$ is not recursive (and also $\bar{A}$ otherwise both would be recursive).

This was also solved by an old tutor:
![[Pasted image 20250104085354.png]]
## Exercise 8.13
![[Pasted image 20250103135912.png]]
The set $A$ is saturated since $A = {x | \phi_x \in \mathcal{A}}$ where $\mathcal{A} = {f \in \mathcal{C} : dom(f) \cap cod(f) = \emptyset}$.

1. Let's prove $A$ is not r.e. using Rice-Shapiro theorem:
    - Consider $id$. Then $id \notin A$ since $dom(id) \cap cod(id) = \mathbb{N} \neq \emptyset$
    - Let $\emptyset$ be the empty function. Then $\emptyset \subset id$ and $\emptyset \in A$
    - By Rice-Shapiro theorem, $A$ is not r.e.
2. Let's prove $\bar{A}$ is not r.e.:
    - Let $f$ be any function where $dom(f) \cap cod(f) \neq \emptyset$. Then $f \in \bar{A}$
    - Let $\emptyset \subset f$. Then $\emptyset \in A$ (so $\emptyset \notin \bar{A}$)
    - By Rice-Shapiro theorem, $\bar{A}$ is not r.e.

Therefore $A$ is not recursive (and $\bar{A}$ also, otherwise both would be recursive).
## Exercise 8.22
![[Pasted image 20250103135929.png]]
The set $A$ is saturated since $A = {x | \phi_x \in \mathcal{A}}$ where $\mathcal{A} = {f \in \mathcal{C} : |{y : f(y) = y}| = \infty}$.

1. Let's prove $A$ is not r.e. using Rice-Shapiro theorem:
    - Let $id$ be the identity function. Then $id \in A$
    - Any finite subfunction $\theta \subset id$ has only finitely many fixed points, so $\theta \notin A$
    - By Rice-Shapiro theorem, $A$ is not r.e.
2. Let's prove $\bar{A}$ is not r.e.:
    - Let $f(x) = x+1$. Then $f \in \bar{A}$ since it has no fixed points
    - Let $\emptyset \subset f$. Then $\emptyset \in A$ (so $\emptyset \notin \bar{A}$)
    - By Rice-Shapiro theorem, $\bar{A}$ is not r.e.

Therefore $A$ is not recursive.

This was also solved by an old tutor:
![[Pasted image 20250104085421.png]]
## Exercise 8.35
![[Pasted image 20250103135947.png]]
Let's prove $B$ is r.e. but not recursive by showing $K \leq_m B$.

1. First, $B$ is r.e. since: $$sc_B(x) = 1(\mu\langle w,t \rangle.S(x,w,x,t))$$ is computable.
2. To prove $B$ is not recursive, we show $K \leq_m B$: Define $g(x,y)$: $$g(x,y) = \begin{cases} x & \text{if } x \in K \\ \uparrow & \text{otherwise} \end{cases}$$ By s-m-n theorem, $\exists s$ total computable such that $\phi_{s(x)}(y) = g(x,y)$. Then:
    - If $x \in K$: $\phi_{s(x)}(s(x)) = x$, so $s(x) \in E_{s(x)}$, thus $s(x) \in B$
    - If $x \notin K$: $\phi_{s(x)}$ undefined everywhere, so $s(x) \notin E_{s(x)}$, thus $s(x) \notin B$

Therefore $B$ is r.e. but not recursive, and consequently $\bar{B}$ is not r.e.
## Exercise 8.36
![[Pasted image 20250103135957.png]]
The set $V$ is saturated since $V = {x | \phi_x \in \mathcal{V}}$ where $\mathcal{V} = {f \in \mathcal{C} : |dom(f)| = \infty}$.

1. $V$ is not r.e. by Rice-Shapiro theorem:
    - Let $id$ be the identity function. Then $id \in V$
    - Any finite subfunction $\theta \subset id$ has finite domain, so $\theta \notin V$
    - By Rice-Shapiro theorem, $V$ is not r.e.
2. $\bar{V}$ is not r.e.:
    - Consider any $f \in \bar{V}$ (finite domain)
    - Let $\emptyset \subset f$. Then $\emptyset \in \bar{V}$
    - By Rice-Shapiro theorem, $\bar{V}$ is not r.e.

Therefore $V$ is not recursive.

This was also solved by an old tutor:
![[Pasted image 20250104085442.png]]
## Exercise 8.37

![[Pasted image 20250103140016.png]]
1. $V$ is r.e. since: $$sc_V(x) = 1(\mu\langle y,k,t \rangle.(H(x,y,t) \land y = k \cdot x))$$ is computable.
2. To prove $V$ is not recursive, we show $K \leq_m V$: Define $g(x,y)$: $$g(x,y) = \begin{cases} 2x & \text{if } x \in K \\ \uparrow & \text{otherwise} \end{cases}$$ By s-m-n theorem, $\exists s$ total computable such that $\phi_{s(x)}(y) = g(x,y)$. Then:
    - If $x \in K$: $2x \in W_{s(x)}$ and $2x = 2 \cdot x$, so $s(x) \in V$
    - If $x \notin K$: $W_{s(x)} = \emptyset$, so $s(x) \notin V$

Therefore $V$ is r.e. but not recursive, and consequently $\bar{V}$ is not r.e.
## Exercise 8.38

![[Pasted image 20250103140023.png]]
The set $V$ is saturated since $V = {x | \phi_x \in \mathcal{V}}$ where $\mathcal{V} = {f \in \mathcal{C} : |dom(f)| > 1}$.

1. $V$ is not r.e. by Rice-Shapiro theorem:
    - Consider $id$. Then $id \in V$
    - Let $\theta \subset id$ be any function with $|dom(\theta)| = 1$. Then $\theta \notin V$
    - By Rice-Shapiro theorem, $V$ is not r.e.
2. $\bar{V}$ is not r.e.:
    - Let $f$ be any function with $|dom(f)| > 1$. Then $f \notin \bar{V}$
    - Let $\emptyset \subset f$. Then $\emptyset \in \bar{V}$
    - By Rice-Shapiro theorem, $\bar{V}$ is not r.e.

Therefore $V$ is not recursive (and also $\bar{V}$ otherwise both would be recursive).
## Exercise 8.39

![[Pasted image 20250103140029.png]]
- First, let's show $P \leq_m Pr$:
    - Define $f(x) = 2x + 3$
    - $f$ is total and computable
    - For any $x \in \mathbb{N}$:
        - If $x \in P$ (x is even), then $f(x) = 2x + 3$ is odd and $\geq 5$, thus not prime
        - If $x \notin P$ (x is odd), then $f(x) = 2x + 3$ is prime
    - Therefore $x \in P \iff f(x) \notin Pr$, so $P \leq_m \overline{Pr}$
- Now, let's show $Pr \leq_m P$:
    - Define $g(x) = 2x$
    - $g$ is total and computable
    - For any $x \in \mathbb{N}$:
        - If $x \in Pr$ (x is prime), then $g(x) = 2x$ is even
        - If $x \notin Pr$ (x is not prime), then $g(x) = 2x$ is even
    - Therefore $x \in Pr \iff g(x) \in P$
## Exercise 8.41

![[Pasted image 20250103140042.png]]
1. First, let's show that $B$ is not recursive by reducing $K$ to $B$ ($K \leq_m B$).

Let's construct a reduction function using s-m-n theorem. Define:

$$ \phi_e(y) = \begin{cases} f(0) & \text{if } x \in K \\ \uparrow & \text{otherwise} \end{cases} $$

By s-m-n theorem, there exists a total computable function $h$ such that:

- If $x \in K$, then $E_{h(x)} = {f(0)}$, thus $img(f) \cap E_{h(x)} \neq \emptyset$
- If $x \notin K$, then $E_{h(x)} = \emptyset$, thus $img(f) \cap E_{h(x)} = \emptyset$

Therefore, $x \in K \iff h(x) \in B$, proving that $K \leq_m B$.

2. Now let's show that $B$ is recursively enumerable.

The semi-characteristic function of $B$ can be written as:

$$ sc_B(x) = \mu w.(H(x, (w)_1, (w)_2) \land \exists y. f(y) = (w)_1) $$

This is computable because:

- $H$ is decidable (step counting predicate)
- $f$ is computable by hypothesis
- The existential quantification over a decidable predicate yields a semi-decidable predicate

3. Since $B$ is r.e. but not recursive, $\overline{B}$ cannot be r.e. (otherwise $B$ would be recursive).

**Conclusion:** $B$ is r.e. but not recursive, and $\overline{B}$ is not r.e.
## Exercise 8.42

![[Pasted image 20250103140052.png]]
1. First, let's prove that $B$ is not recursive by showing $K \leq_m B$.

By s-m-n theorem, define a reduction function $h$ where:

$$ \phi_{h(x)}(y) = \begin{cases} 1 & \text{if } x \in K \\ \uparrow & \text{otherwise} \end{cases} $$

Then:

- If $x \in K$, then $E_{h(x)} = {1}$ and $W_{h(x)} = \emptyset$, thus $E_{h(x)} \not\subseteq W_{h(x)}$
- If $x \notin K$, then $E_{h(x)} = \emptyset$ and $W_{h(x)} = \emptyset$, thus $E_{h(x)} \subseteq W_{h(x)}$

Therefore $x \in K \iff h(x) \in B$, establishing $K \leq_m B$.

2. $B$ is recursively enumerable since:

$$ sc_B(x) = \mu w.(S(x, (w)_1, (w)_2, (w)_3) \land \neg H(x, (w)_2, (w)_3)) $$

This is computable because:

- $S$ is decidable (step counting predicate)
- $H$ is decidable
- Composition of decidable predicates is decidable

3. Since $B$ is r.e. but not recursive, $\overline{B}$ is not r.e.

**Conclusion:** $B$ is r.e. but not recursive, and $\overline{B}$ is not r.e.
## Exercise 8.43

![[Pasted image 20250103140102.png]]
1. First, let's show that $B$ is not recursively enumerable by reducing $\overline{K}$ to $B$ ($\overline{K} \leq_m B$).

By s-m-n theorem, define:

$$ \phi_{g(x)}(y) = \begin{cases} 0 & \text{if } x \notin K \\ \uparrow & \text{otherwise} \end{cases} $$

Then for any $x$:

- If $x \in \overline{K}$, then $\forall m \in \mathbb{N}. m \cdot g(x) \in W_{g(x)}$
- If $x \notin \overline{K}$, then $\exists m \in \mathbb{N}. m \cdot g(x) \notin W_{g(x)}$

Therefore $x \in \overline{K} \iff g(x) \in B$

2. Now let's show that $\overline{B}$ is recursively enumerable.

The semi-characteristic function of $\overline{B}$ is:

$$ sc_{\overline{B}}(x) = \mu w.(\exists m \leq (w)_1. \neg H(x, m \cdot x, (w)_2)) $$

This is computable because:

- $H$ is decidable
- Bounded existential quantification preserves semi-decidability

3. Since $\overline{B}$ is r.e. but $B$ is not r.e., $B$ cannot be recursive.

**Conclusion:** $B$ is not r.e., $\overline{B}$ is r.e., and $B$ is not recursive.
## Exercise 8.45

![[Pasted image 20250103140112.png]]
1. First, let's show that $B$ is not recursive by reducing $K$ to $B$ ($K \leq_m B$).

By s-m-n theorem, define:

$$ \phi_{g(x)}(y) = \begin{cases} x+1 & \text{if } x \in K \\ \uparrow & \text{otherwise} \end{cases} $$
Then:

- If $x \in K$, then $x+1 \in E_{g(x)}$ and $x+1 > g(x)$
- If $x \notin K$, then $E_{g(x)} = \emptyset$, so $\nexists y > g(x). y \in E_{g(x)}$

Therefore $x \in K \iff g(x) \in B$

2. $B$ is recursively enumerable since:

$$ sc_B(x) = \mu w.(S(x, (w)_1, (w)_2, (w)_3) \land (w)_1 > x) $$

This is computable because:

- $S$ is decidable
- Greater-than relation is decidable
- Conjunction of decidable predicates is decidable

3. Since $B$ is r.e. but not recursive, $\overline{B}$ cannot be r.e.

**Conclusion:** $B$ is r.e. but not recursive, and $\overline{B}$ is not r.e.
# 9. Second recursion theorem
## Exercise 9.1
![[Pasted image 20250103140141.png]]
![[Pasted image 20250104083133.png]]
![[Pasted image 20250104083149.png]]
## Exercise 9.2
![[Pasted image 20250103140149.png]]
![[Pasted image 20250104083108.png]]
![[Pasted image 20250104083045.png]]
## Exercise 9.3
![[Pasted image 20250103140157.png]]
The Second Recursion Theorem states that for every total computable function $h : \mathbb{N} \rightarrow \mathbb{N}$, there exists $e \in \mathbb{N}$ such that $\varphi_{h(e)} = \varphi_e$.

We want to prove that for each $y \in \mathbb{N}$, there exists $x \in \mathbb{N}$ such that $\varphi_x(y) = y^x$.

Define $h(e) = s(e, y)$, where $s$ is a total computable function given by the $s$-$m$-$n$ theorem such that $\varphi_{s(e,y)}(z) = [\varphi_e(y)]^z$.

By the Second Recursion Theorem, there exists $x \in \mathbb{N}$ such that $\varphi_x = \varphi_{h(x)} = \varphi_{s(x,y)}$. Thus, $\varphi_x(y) = [\varphi_x(y)]^y = y^x$.
## Exercise 9.4
![[Pasted image 20250103140206.png]]
The Second Recursion Theorem states that for every total computable function $h : \mathbb{N} \rightarrow \mathbb{N}$, there exists $e \in \mathbb{N}$ such that $\varphi_{h(e)} = \varphi_e$.
We want to prove that there exists $n \in \mathbb{N}$ such that $W_n = E_n = {x \cdot n : x \in \mathbb{N}}$.

Define $h(e) = s(e)$, where $s$ is a total computable function given by the $s$-$m$-$n$ theorem such that $$\varphi_{s(e)}(x) = \begin{cases} e \cdot x & \text{if } \varphi_e(x)\downarrow \\ \uparrow & \text{otherwise} \end{cases}$$
By the Second Recursion Theorem, there exists $n \in \mathbb{N}$ such that $\varphi_n = \varphi_{h(n)} = \varphi_{s(n)}$. Thus, $$\varphi_n(x) = \begin{cases} n \cdot x & \text{if } \varphi_n(x)\downarrow \\ \uparrow & \text{otherwise} \end{cases}$$

This implies $W_n = E_n = {x \cdot n : x \in \mathbb{N}}$.
## Exercise 9.6
![[Pasted image 20250104083223.png]]
The Second Recursion Theorem states that for every total computable function $h : \mathbb{N} \rightarrow \mathbb{N}$, there exists $e \in \mathbb{N}$ such that $\varphi_{h(e)} = \varphi_e$.
We want to prove that there exists $x \in \mathbb{N}$ such that $\varphi_x(y) = x - y$.

Define $h(e) = s(e)$, where $s$ is a total computable function given by the $s$-$m$-$n$ theorem such that $\varphi_{s(e)}(y) = e - y$.

By the Second Recursion Theorem, there exists $x \in \mathbb{N}$ such that $\varphi_x = \varphi_{h(x)} = \varphi_{s(x)}$. Thus, $\varphi_x(y) = x - y$.