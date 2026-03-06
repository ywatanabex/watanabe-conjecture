# A proof write-up for the $2\times 2$ grid case of the Watanabe conjecture

## Status note

This document is a polished write-up of the proof strategy developed in the conversation.
It is intended as a clean research note for further checking and use.
The argument is self-contained at the level of the reductions and lemmas stated below, but it has not yet been independently referee-checked.

---

## 1. Statement

Let $G$ be the $2\times 2$ grid, i.e. the $3\times 3$ rectangular grid graph with vertex set
\[
\{(i,j): i,j\in\{0,1,2\}\}
\]
and edges joining nearest horizontal and vertical neighbors.

For a graph $H$, write
\[
p(H)=\sum_{I\in \mathcal I(H)} \prod_{v\in I} x_v
\]
for its independent-set polynomial.

If $\widetilde G$ is an $M$-cover of $G$, let $\pi$ denote the projection that identifies all variables above the same base vertex. The Watanabe conjecture asserts that
\[
\pi\bigl(p(\widetilde G)\bigr) \preceq p(G)^M,
\]
where $\preceq$ means coefficientwise inequality.

The goal of this note is to prove this conjecture for the $2\times 2$ grid.

---

## 2. Coefficientwise interpretation

Fix a coefficient vector
\[
a=(a_v)_{v\in V(G)}\in \{0,1,\dots,M\}^{V(G)}.
\]
The coefficient of the monomial $\prod_v x_v^{a_v}$ in $\pi(p(\widetilde G))$ counts families of subsets
\[
S_v\subset [M],\qquad |S_v|=a_v,
\]
one for each base vertex $v$, satisfying the disjointness constraints induced by the cover permutations:
for every oriented edge $u\to v$ with edge permutation $\alpha(u\to v)\in S_M$,
\[
S_v\cap \alpha(u\to v)(S_u)=\varnothing.
\]
In the trivial cover all edge permutations are the identity, so the constraints reduce to
\[
S_u\cap S_v=\varnothing
\]
for every edge $uv$ of $G$.

Thus the conjecture for $G$ is a purely finite counting inequality.

---

## 3. Gauge normal form for the $2\times 2$ grid

Write the $3\times 3$ grid in three columns:

- left column: top, middle, bottom occupancies $(\alpha,b,\gamma)$,
- middle column: $(x,y,z)$,
- right column: $(\delta,e,\phi)$.

By a standard gauge transformation on the cover, we may assume:

- all vertical edges carry the identity permutation,
- the two middle-row horizontal edges also carry the identity,
- the only remaining free edge permutations are the four horizontal edges on the top and bottom rows.

Equivalently, after a further normalization on one side, we may work with three relative permutations
\[
\rho,\ \sigma,\ \tau\in S_M.
\]
These encode the nontrivial twisting seen from the central cut.

Nothing in the coefficient count changes under this gauge normalization.

---

## 4. Cutting at the middle column

Fix the middle-column state
\[
(S,T,R),\qquad |S|=x,\ |T|=y,\ |R|=z,
\]
subject to the vertical disjointness constraints
\[
S\cap T=\varnothing,\qquad T\cap R=\varnothing.
\]

For a fixed cover in gauge normal form, the coefficient for the chosen occupancy data is
\[
N=\sum_{(S,T,R)} L(S,T,R)\,R(S,T,R),
\]
where the left and right factors count admissible choices in the left and right columns, respectively.

More explicitly, after fixing the gauge so that the upper left horizontal edge is the identity, the fixed-$T$ contribution may be written as
\[
N_T(\rho,\sigma,\tau)
=
\sum_{\substack{S,R\subset U\\ |S|=x,\ |R|=z}}
\sum_{\substack{B\subset U\\ |B|=b}}
\sum_{\substack{F\subset U\\ |F|=e}}
\Pi_{\rho,\sigma,\tau}(S,R,B,F),
\]
where
\[
U=[M]\setminus T,
\]
and
\[
\Pi_{\rho,\sigma,\tau}(S,R,B,F)
=
\binom{M-|S\cup B|}{\alpha}
\binom{M-|R\cup \rho(B)|}{\gamma}
\binom{M-|S\cup \sigma(F)|}{\delta}
\binom{M-|R\cup \tau(F)|}{\phi}.
\]
The full coefficient is obtained by summing over all $T\subset [M]$ of size $y$.

This is the starting point for the proof.

---

## 5. Cut-monotonicity

For a permutation $\pi\in S_M$ and a fixed subset $T\subset [M]$, define the associated cut set
\[
X_\pi:=\pi^{-1}(T)\cap U,
\qquad U=[M]\setminus T.
\]
Thus $X_\pi$ is the set of points in $U$ that are sent by $\pi$ into $T$.

For a subset $Y\subset U$ and a test set $W\subset U$, write
\[
\kappa_\pi(Y;W):=|Y\cap X_\pi|+|W\cup \pi(Y\setminus X_\pi)|.
\]
Then
\[
|W\cup \pi(Y)|=\kappa_\pi(Y;W).
\]
So the fixed-$T$ summand becomes
\[
\Pi_{\rho,\sigma,\tau}
=
\binom{M-|S\cup B|}{\alpha}
\binom{M-\kappa_\rho(B;R)}{\gamma}
\binom{M-\kappa_\sigma(F;S)}{\delta}
\binom{M-\kappa_\tau(F;R)}{\phi}.
\]

### Lemma 5.1 (one-step cut monotonicity)
Fix $T$. Suppose $u\in U\setminus X_\sigma$ and modify $\sigma$ to a permutation $\sigma'$ so that $u$ is newly sent to $T$, while all other cut data are unchanged. Then
\[
N_T(\rho,\sigma',\tau)\le N_T(\rho,\sigma,\tau).
\]
The same statement holds with $\sigma$ replaced by $\rho$ or $\tau$.

#### Proof
Fix $(S,R,B,F)$. We compare the factor involving $\sigma$:
\[
\binom{M-\kappa_\sigma(F;S)}{\delta}
\quad\text{vs.}\quad
\binom{M-\kappa_{\sigma'}(F;S)}{\delta}.
\]
If $u\notin F$, nothing changes. If $u\in F$, then the new cut contributes one extra point to $|F\cap X_{\sigma'}|$, while the image-side union can decrease by at most one, depending on whether $\sigma(u)\in S$ or not. Hence
\[
\kappa_{\sigma'}(F;S)\ge \kappa_\sigma(F;S).
\]
Since the map $q\mapsto \binom{M-q}{\delta}$ is nonincreasing in $q$, the corresponding factor does not increase. The other three factors are unchanged, so the whole summand does not increase pointwise. Summing over all variables gives the claim.

The cases of $\rho$ and $\tau$ are identical. $\square$

### Corollary 5.2 (zero-cut endpoint)
For every fixed $T$ and every triple $(\rho,\sigma,\tau)$,
\[
N_T(\rho,\sigma,\tau)
\le
N_T(\rho_0,\sigma_0,\tau_0),
\]
where $\rho_0,\sigma_0,\tau_0$ preserve $U$ setwise, equivalently
\[
X_{\rho_0}=X_{\sigma_0}=X_{\tau_0}=\varnothing.
\]

#### Proof
Apply Lemma 5.1 repeatedly until all cut sets are empty. $\square$

So for each fixed middle set $T$, the largest contribution is attained when no permutation sends any point of $U$ into $T$.

---

## 6. Reduction to the $y=0$ slice

Assume now that $\rho_0,\sigma_0,\tau_0$ preserve $U$. Then all unions in the fixed-$T$ expression take place purely inside the smaller universe $U$ of size
\[
N=M-y.
\]
For any nonnegative integers $q,k$ one has the Vandermonde-type identity
\[
\binom{M-q}{k}=
\sum_{r=0}^{k}\binom{y}{r}\binom{N-q}{k-r}.
\]
Applying this to the four binomial factors shows that the zero-cut quantity is a positive linear combination of coefficients coming from the $y=0$ slice on the smaller label universe $[N]$.

More precisely,
\[
N_T(\rho_0,\sigma_0,\tau_0)
=
\sum_{r_1=0}^{\alpha}
\sum_{r_2=0}^{\gamma}
\sum_{r_3=0}^{\delta}
\sum_{r_4=0}^{\phi}
\binom{y}{r_1}\binom{y}{r_2}\binom{y}{r_3}\binom{y}{r_4}
\,
\mathcal C_N^{(0)}(\alpha-r_1,\gamma-r_2,\delta-r_3,\phi-r_4;\rho_0,\sigma_0,\tau_0),
\]
where $\mathcal C_N^{(0)}$ denotes the mixed coefficient for the $y=0$ slice on the universe $[N]$.

Since all coefficients in this decomposition are nonnegative, it is enough to prove the desired inequality for the $y=0$ slice.

---

## 7. The $y=0$ slice as a Johnson-scheme problem

Set $T=\varnothing$, so $U=[N]$ and the central middle occupancy is zero.
The mixed coefficient becomes
\[
\mathcal C_N^{(0)}(\rho,\sigma,\tau)
=
\sum_{\substack{|B|=b,\ |F|=e\\ |S|=x,\ |R|=z}}
\binom{N-|S\cup B|}{\alpha}
\binom{N-|R\cup \rho(B)|}{\gamma}
\binom{N-|S\cup \sigma(F)|}{\delta}
\binom{N-|R\cup \tau(F)|}{\phi}.
\]

Define kernels
\[
A(B,C):=
\sum_{|S|=x}
\binom{N-|S\cup B|}{\alpha}
\binom{N-|S\cup C|}{\delta},
\]
\[
C(B,C):=
\sum_{|R|=z}
\binom{N-|R\cup B|}{\gamma}
\binom{N-|R\cup C|}{\phi}.
\]
Then
\[
\mathcal C_N^{(0)}(\rho,\sigma,\tau)
=
\sum_{|B|=b,\ |F|=e}
A(B,\sigma F)\,C(\rho B,\tau F).
\]

A change of variables shows that this depends only on the single relative permutation
\[
\pi:=\tau\sigma^{-1}\rho^{-1}.
\]
Thus we may write
\[
\mathcal C_N^{(0)}(\pi)
=
\sum_{|H|=b,\ |K|=e}
A(H,K)\,C(H,\pi K).
\]

Since both $A$ and $C$ depend only on the intersection size of their arguments, they are $S_N$-equivariant kernels between the permutation modules
\[
V_b:=\mathbb R^{\Omega_b},\qquad V_e:=\mathbb R^{\Omega_e},
\]
where $\Omega_k$ denotes the family of $k$-subsets of $[N]$.
Hence
\[
\mathcal C_N^{(0)}(\pi)=\langle A,CP_\pi\rangle_F,
\]
where $P_\pi$ is the permutation matrix on $V_e$ induced by $\pi$.

---

## 8. Multiplicity-free decomposition and character expansion

The Johnson permutation modules decompose multiplicity-free:
\[
V_k\cong \bigoplus_{i=0}^{r_k} V_k^{(i)},
\qquad r_k=\min(k,N-k),
\]
with each $V_k^{(i)}$ isomorphic to the Specht module $S^{(N-i,i)}$.
Let
\[
r:=\min(r_b,r_e).
\]
Then each equivariant map $V_e\to V_b$ decomposes blockwise as a scalar on the common isotypic components.
Choose norm-one intertwiners
\[
J_i:V_e^{(i)}\to V_b^{(i)}.
\]
There exist scalars $a_i,c_i$ such that
\[
A=\bigoplus_{i=0}^{r} a_i J_i,
\qquad
C=\bigoplus_{i=0}^{r} c_i J_i.
\]
Therefore
\[
\mathcal C_N^{(0)}(\pi)
=
\sum_{i=0}^{r} a_i c_i\,\chi_i(\pi),
\]
where $\chi_i$ is the irreducible character of $S^{(N-i,i)}$.

So the problem reduces to showing
\[
a_i c_i\ge 0 \qquad \text{for all }i.
\]

---

## 9. Positivity of the block coefficients

Define the disjointness incidence matrices
\[
D_{p,q}(X,Y)=\mathbf 1[X\cap Y=\varnothing],
\]
where $X$ ranges over $p$-subsets and $Y$ over $q$-subsets.
A standard identity gives
\[
\binom{N-|S\cup B|}{\alpha}
=
\sum_{|Y|=\alpha}
\mathbf 1[Y\cap S=\varnothing]\,\mathbf 1[Y\cap B=\varnothing].
\]
Hence the matrix
\[
M^{(x)}_{\alpha}(B,S):=\binom{N-|S\cup B|}{\alpha}
\]
factors as
\[
M^{(x)}_{\alpha}=D_{b,\alpha}\,D_{x,\alpha}^{\top}.
\]
Similarly,
\[
A=M^{(x)}_{\alpha}(M^{(x)}_{\delta})^{\top}
= D_{b,\alpha}\,(D_{x,\alpha}^{\top}D_{x,\delta})\,D_{e,\delta}^{\top}.
\]
The disjointness incidence matrices are diagonal on the Johnson blocks, with eigenvalues of the form
\[
(-1)^i d_i(p,q),\qquad d_i(p,q)\ge 0.
\]
Therefore the block coefficient of $A$ on the $i$-th common summand is
\[
a_i=d_i(b,\alpha)\,d_i(x,\alpha)\,d_i(x,\delta)\,d_i(e,\delta)\ge 0.
\]
Exactly the same argument gives
\[
c_i=d_i(b,\gamma)\,d_i(z,\gamma)\,d_i(z,\phi)\,d_i(e,\phi)\ge 0.
\]
Hence
\[
a_i c_i\ge 0 \qquad \text{for all }i.
\]

---

## 10. Maximization at the identity

For any irreducible character,
\[
|\chi_i(\pi)|\le \chi_i(\mathrm{id})=\dim V_e^{(i)}.
\]
Since every coefficient $a_i c_i$ is nonnegative,
\[
\mathcal C_N^{(0)}(\pi)
=
\sum_i a_i c_i\chi_i(\pi)
\le
\sum_i a_i c_i\chi_i(\mathrm{id})
=
\mathcal C_N^{(0)}(\mathrm{id}).
\]
So the $y=0$ slice is maximized by the trivial cover.

Combining this with the reduction in Sections 5 and 6 yields the following theorem.

### Theorem 10.1
For every $M$-cover of the $2\times 2$ grid,
\[
\pi\bigl(p(\widetilde G_{2\times 2})\bigr)
\preceq
p(G_{2\times 2})^M.
\]
That is, the Watanabe conjecture holds coefficientwise for the $2\times 2$ grid.

---

## 11. Remarks on routes that were tried and abandoned

Several natural-looking approaches were explored before the final argument above emerged.
They are worth recording, because they clarify what really fails and why the final proof is organized the way it is.

### 11.1 Pointwise domination of half-kernels
A very tempting idea is to prove, for each fixed middle state $(S,T,R)$, that the number of left-half extensions is pointwise maximized by the trivial cover. This is false in general. Even for small $M$, one can find states for which a twisted half-cover has more extensions than the trivial one. So any proof that works must use cancellation or averaging over states.

### 11.2 A naive two-variable defect inequality
Another early attempt is to track only how much of a right-hand set stays inside the cut complement and how much survives after a second permutation. That is too coarse. There are small counterexamples showing that improving one of these parameters can worsen the other enough to reverse the inequality.

### 11.3 Fixed-$(T,B)$ pointwise maximization
A stronger idea is to fix $T$ and a left middle set $B$, then try to show the corresponding local quantity is maximized by the trivial configuration. This is also false in that form. Small exact computations show that the local maximum need not occur at the trivial point, even though the full coefficient still appears to do so.

### 11.4 High-dimensional local polytope approaches
A large part of the exploration tried to parameterize the local problem by many overlaps and then prove monotonicity on a polytope of feasible data. This helped identify the correct variables but did not produce a stable proof. The decisive simplification came only after recognizing that cut-monotonicity allows one to throw away all states with nonzero cut and reduce to the $y=0$ slice.

In hindsight, the real lesson is that local pointwise optimization is the wrong target; the useful structure is the global equivariance of the $y=0$ slice.

---

## 12. Ideas for generalization

The proof above suggests a three-step template that may extend beyond the $2\times 2$ grid.

### 12.1 Cut-monotonicity at a chosen separator
The first step was to cut the graph along a separator and show that sending more labels across that separator can only decrease the corresponding coefficient contribution. For wider strips or bounded-treewidth graphs, one should look for the analogous monotonicity with respect to separator crossing sets.

### 12.2 Reduction to a zero-cut endpoint
Once cut-monotonicity is available, the next step is to push every cover to a zero-cut endpoint. In the $2\times 2$ grid this endpoint decomposed into a positive linear combination of smaller-$y$ slices, eventually reaching $y=0$. For a more general graph family, one would want a recursive reduction that lowers the separator occupancy or the effective width.

### 12.3 Equivariant kernel analysis on boundary-state spaces
The final step in the $2\times 2$ proof was representation-theoretic: the $y=0$ slice became an equivariant bilinear form on Johnson permutation modules, and the positivity of block coefficients forced the identity permutation to maximize the coefficient.

For wider strips, the relevant boundary-state spaces will no longer be single Johnson schemes. They are likely governed by:

- products or towers of Johnson schemes,
- Terwilliger algebras attached to boundary-state graphs,
- partition-algebra type centralizers when multiple subset coordinates interact.

This is the conceptual reason those objects kept appearing during the exploration.

### 12.4 What a plausible next target looks like
A realistic next target is the width-$3$ strip or another class where the separator still has small complexity. The proof strategy would be:

1. identify the right separator states,
2. prove cut-monotonicity,
3. reduce to a zero-cut endpoint,
4. write the resulting slice as an equivariant kernel on the separator-state module,
5. prove positivity of the block coefficients.

If this can be done uniformly for bounded width, it would be a substantial step toward the general conjecture.

---

## 13. Final summary

For the $2\times 2$ grid, the proof has three main ingredients:

1. **cut-monotonicity:** adding crossings from the cut complement into the middle set decreases the fixed-$T$ contribution,
2. **zero-cut reduction:** the maximal fixed-$T$ contribution is therefore attained when the cover permutations preserve the cut complement,
3. **Johnson-scheme positivity:** the resulting $y=0$ slice is an equivariant bilinear form whose block coefficients are nonnegative, so it is maximized by the identity permutation.

Together these imply coefficientwise domination by the trivial cover, proving the Watanabe conjecture for the $2\times 2$ grid.
