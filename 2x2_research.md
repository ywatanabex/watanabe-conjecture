# 2x2 grid case of the Watanabe conjecture: research note

## Status

This document is **not a proof**. It is a research note summarizing what was learned from the attempted proof in `2x2_proof.md`, the subsequent expert feedback, and the current best understanding of the $2\times 2$ grid case.

The main correction is that the proof draft contained a **fatal gauge-normalization gap**: it incorrectly reduced the $2\times 2$ grid cover to only three independent permutations after fixing a spanning tree. Since the cycle rank of the $3\times 3$ grid graph is $12-9+1=4$, a general $M$-cover still has **four independent edge parameters** after tree gauge-fixing. Because of this, the main reduction in the proof draft is not valid as written.

That said, the work was still useful. It produced:

1. a much clearer picture of where the genuine difficulty lies,
2. a plausible representation-theoretic route for a corrected proof,
3. several reductions and formulas that remain promising once rebuilt from a correct 4-parameter gauge normal form.

This note records the safe conclusions, the broken steps, and the most promising next directions.

---

## 1. Goal

Let $G$ be the $2\times 2$ grid, i.e. the $3\times 3$ rectangular grid graph. For an $M$-cover $\widetilde G$ of $G$, the Watanabe conjecture predicts
\[
\pi\bigl(p(\widetilde G)\bigr) \preceq p(G)^M,
\]
where $p(H)$ is the independent-set polynomial and $\pi$ identifies variables lying over the same base vertex.

For a fixed coefficient vector, this is a finite counting problem for families of subsets of $[M]$ satisfying edge-disjointness constraints twisted by the cover permutations.

The objective of the original draft was to prove this conjecture for the $2\times 2$ grid.

---

## 2. What turned out to be wrong

### 2.1 The key gap: over-fixing the gauge

The draft used the following gauge picture.

- First, all vertical edges and the two middle-row horizontal edges were set to the identity.
- Then an additional normalization was used to remove one more horizontal edge, leaving only three relative permutations.

This second step is **not valid in general**.

Why:

- The $3\times 3$ grid has cycle rank $4$.
- After fixing a spanning tree, there remain **four** independent cycle parameters.
- If the vertical edges in a column are already fixed to the identity, then any further gauge transform preserving those vertical identities must act by the **same permutation on all vertices of that column**.
- Therefore, one cannot in general kill a single horizontal edge without simultaneously changing another horizontal edge that had already been fixed.

So the passage from a correct 4-parameter gauge normal form to a 3-parameter form was illegitimate.

### 2.2 Why this breaks the later reductions

The invalid gauge step was used to justify formulas of the form
\[
U = [M]\setminus T, \qquad B,F \subset U,
\]
and then to count everything inside the same universe $U$.

But after the gauge issue is corrected, the relevant subsets on the left and right are naturally pulled back by different permutations. They do **not** automatically live in the same universe $U$.

As a result, several later steps in the proof draft are not currently justified:

- the fixed-$T$ counting formulas in the form written there,
- the cut-monotonicity argument in that form,
- the Vandermonde reduction to a $y=0$ slice in that form,
- the claimed complete proof for the full $2\times 2$ grid.

So `2x2_proof.md` should not be treated as a proof.

---

## 3. What still seems mathematically valuable

Even though the proof draft fails globally, it produced several ideas that still look important.

### 3.1 The right problem is global, not pointwise

A recurring false lead was to try to prove a pointwise inequality for each fixed boundary state or each fixed local occupancy pattern. Small examples strongly suggest that such pointwise inequalities are too strong and generally false.

The more promising viewpoint is global:

- cut the graph at the middle column,
- organize the coefficient as a bilinear or quadratic form on the boundary-state space,
- study the resulting operator using symmetry.

This is consistent with the original notes: the obstruction does not appear to be a simple injection on individual local configurations, but rather a positivity problem for an equivariant kernel on a $k$-subset state space.

### 3.2 Johnson-scheme / representation-theoretic structure is real

The most promising part of the failed proof draft is the observation that once one reaches a suitable reduced slice, the kernels depend only on set-intersection data. That places the problem naturally in the Johnson scheme and its representation theory.

Concretely, one expects:

- kernels on $b$-subsets and $e$-subsets depending only on intersection size,
- decomposition into isotypic components indexed by $i$,
- block coefficients expressible through disjointness or incidence operators,
- positivity of certain block products,
- maximality at the identity permutation via a character bound or operator norm bound.

This part must be rebuilt from a correct 4-parameter setup, but the general strategy still looks very plausible.

### 3.3 A corrected proof will probably not be local-combinatorial

Multiple attempted "elementary move" or "local split" arguments ran into counterexamples or structural obstacles. This strongly suggests that the final proof, if it exists, will likely be closer to:

- a positivity statement in the Johnson/Terwilliger algebra,
- or a carefully organized global averaging argument,

rather than a local injection on raw configurations.

---

## 4. What can currently be stated safely

At present, the following statements seem safe.

### 4.1 The $2\times 2$ grid remains open in this project

As of now, we do **not** have a valid proof of the $2\times 2$ grid case.

### 4.2 The correct gauge normal form must retain four free edge parameters

Any future proof should begin from a proper gauge normalization that leaves exactly four independent edge permutations corresponding to the cycle rank.

A convenient choice is:

- fix a spanning tree of 8 edges to the identity,
- keep the 4 non-tree edges as the genuine free parameters.

Any later reduction must be checked directly in that 4-parameter model.

### 4.3 The middle-column cut is still the right place to analyze the problem

Even though the previous implementation was flawed, cutting along the middle column still appears to be the natural decomposition. The coefficient should be rewritten as a sum over middle-column states, producing a bilinear form between left and right half-contributions.

The challenge is to keep the four remaining edge parameters correctly visible in that decomposition.

### 4.4 The symmetric / reduced slices deserve separate treatment

The expert feedback plausibly identifies the later “$y=0$ slice” representation-theoretic argument as a genuinely strong idea, though it must be rederived independently from the corrected gauge form.

So one good strategy is:

1. define a corrected 4-parameter model,
2. identify a reduced slice or reduced family of coefficients,
3. prove a standalone Johnson-scheme theorem there,
4. then connect the full problem to that theorem without illegal gauge simplifications.

---

## 5. A plausible corrected roadmap

Here is the most credible route forward.

### Step 1. Rebuild the middle-cut formulas from the correct 4-edge gauge form

Write the cover in a genuine 4-parameter normal form and derive the exact coefficient formula after cutting at the middle column.

This step should be done from scratch, without reusing the invalid formulas from `2x2_proof.md`.

### Step 2. Isolate a correct “reduced slice” theorem

The later proof draft suggests that some reduced slice—morally the analogue of the old $y=0$ slice—may admit a clean Johnson-scheme formulation.

This should be stated and proved as an independent theorem, without relying on the invalid earlier reductions.

### Step 3. Express the full coefficient as a positive combination of reduced-slice quantities

The failed proof tried to do this by a Vandermonde identity after forcing all sets into one common universe. That exact implementation fails.

A corrected version may still exist, but it must explicitly track the four remaining edge parameters and the pullbacks of the relevant subsets.

### Step 4. Compare the reduced-slice operators by representation theory

If the reduced slice really leads to kernels depending only on intersection size, then one can try to prove maximality of the trivial cover by:

- decomposing the relevant permutation modules,
- factoring the kernels via disjointness/incidence matrices,
- proving nonnegativity of block coefficients,
- applying character bounds at the identity.

This is currently the most promising structural idea on the table.

---

## 6. Methods that were tried and did not work

This section is included on purpose, because these failures clarify what the proof probably is **not**.

### 6.1 Pointwise domination by the trivial cover

Trying to show that each boundary-state contribution is individually maximized by the trivial cover is too strong. Small cases indicate this fails.

### 6.2 Simple defect parameters

Several attempts tried to organize the problem by a few scalar “defect” quantities, such as sizes of certain pulled-back subsets or overlaps between two images. These parameters were not rich enough to control the full count.

### 6.3 Local split / local move inequalities on atomized state spaces

A more elaborate attempt decomposed the state space into finitely many atom types and tried to prove that certain local moves always push the count toward the trivial case. This also appears too naive: the global hypergeometric sampling over $k$-subsets introduces correlations that simple local factor comparisons do not capture.

### 6.4 Overly aggressive gauge fixing

The biggest concrete failure was the illegal reduction from four cycle parameters to three. Any future argument should be very conservative about gauge fixing and check carefully which edges can genuinely be normalized simultaneously.

---

## 7. Immediate next tasks

The most useful next tasks are probably the following.

### Task A. Write down the exact 4-parameter middle-cut formula

This is the highest priority. Without it, it is too easy to smuggle in invalid assumptions about which sets live in which universes.

### Task B. Re-derive the candidate reduced slice in that exact model

If a $y=0$-type slice survives the correct setup, that would be a major step.

### Task C. Extract the operator actually acting on the boundary-state space

The final object should probably be an operator or bilinear form on a direct sum of Johnson spaces rather than a raw sum over configurations.

### Task D. Test the reduced slice numerically for small $M$

Small exact computations for $M=3$ and $M=4$ can help identify the correct representation-theoretic statement before trying to prove it abstractly.

---

## 8. Bottom line

The current situation is:

- the previous proof draft is **not valid** as a proof of the $2\times 2$ grid case,
- the fatal issue is the illegal gauge reduction from four free cycle parameters to three,
- however, the later representation-theoretic direction remains highly promising,
- the problem now looks much more sharply focused: the real challenge is to rebuild the middle-cut reduction correctly and then prove positivity for the resulting boundary operator.

So the project is not finished, but it is in a much better state conceptually than before. The most important lesson is that the final proof, if it exists, will likely come from a **correct global operator formulation** and not from a local configuration-by-configuration comparison.
