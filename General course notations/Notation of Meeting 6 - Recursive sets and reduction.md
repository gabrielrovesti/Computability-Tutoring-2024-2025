## Recursive Sets

A set A ⊆ ℕ is recursive (or decidable) if its characteristic function χ_A is computable:

χ_A: ℕ → ℕ
χ_A(x) = {
    1 if x ∈ A
    0 if x ∉ A
}

## Many-One Reduction

For sets A, B ⊆ ℕ, we write A ≤_m B (read as "A reduces to B") if there exists a total computable function f: ℕ → ℕ such that for all x ∈ ℕ:

x ∈ A ⟺ f(x) ∈ B

The function f is called the reduction function.

## Important Properties of Reductions

1. If A ≤_m B and B is recursive, then A is recursive
2. If A is not recursive and A ≤_m B, then B is not recursive

## Recursive Set Properties

A set A ⊆ ℕ is recursive if and only if both A and its complement Ā are recursively enumerable (r.e.).

## Semi-Characteristic Functions

For a set A ⊆ ℕ, the semi-characteristic function sc_A is defined as:

sc_A: ℕ → ℕ
sc_A(x) = {
    1 if x ∈ A
    ↑ if x ∉ A
}

## Structure Theorem for Semi-Decidable Predicates

A predicate P(x⃗) is semi-decidable if and only if there exists a decidable predicate Q(t,x⃗) such that:

P(x⃗) ≡ ∃t.Q(t,x⃗)

## Projection Theorem

If P(x,y⃗) is semi-decidable, then ∃x.P(x,y⃗) is also semi-decidable.

## Notable Non-Recursive Sets

1. K = {x | x ∈ W_x}
2. T = {x | φ_x total}

These sets serve as fundamental examples of non-recursive sets and are often used in reductions to prove other sets non-recursive.

## Domain and Range Notation

- W_e denotes the domain of φ_e (the e-th partial computable function)
- E_e denotes the range (or codomain) of φ_e