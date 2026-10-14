<!-- solve-problem:ab32c89d-5052-4c05-92b2-20c2644b71b3 -->
# Recognizing polygon vertex-visibility graphs

A [Tangle Solve problem](https://solve.tangle.tools/problems/ab32c89d-5052-4c05-92b2-20c2644b71b3).

## What is the problem?

Let P be a simple polygon with vertices v₁, …, vₙ and boundary cycle C = (v₁, v₂, …, vₙ, v₁). Two vertices u, v are **visible** if the open segment uv lies in the interior of P (visibility along the boundary edges is conventionally excluded, so the visibility graph G together with the boundary cycle satisfies G ⊇ C minus edges, depending on convention — this must be fixed explicitly; the standard convention: uv ∈ E(G) iff uv is a diagonal of P, i.e., the open segment lies in int(P)).

The **vertex-visibility graph** of P is G(P). The recognition problem, in its "ordered" form (TOPP Problem 17 / O'Rourke 1993):

**Input:** A graph G and a Hamiltonian cycle C of G (the proposed boundary order).
**Question:** Is there a simple polygon P whose vertices in boundary order realize G as its vertex-visibility graph? If yes, output coordinates for a realization.

The "unordered" variant (decide whether some cyclic order works) is strictly harder; the census record targets the ordered version, and that is the version to attack. A key subtlety: the natural formulation is over the **real numbers** — the coordinates of a realization are reals, so complexity is naturally phrased relative to the existential theory of the reals (∃ℝ). Whether recognition is in NP (i.e., admits rational or polynomial-precision solutions) is itself open.

## Why does it matter?

Visibility graphs are the canonical compressed representation of "what a robot/sensor inside a polygon can see," and recognition is the soundness question for that representation: given line-of-sight data, can a consistent shape actually be reconstructed? A positive algorithmic result unlocks reconstruction pipelines in robotics, art-gallery/illumination computations, and CAD; a hardness result (∃ℝ-hardness or NP-hardness) would justify the field's reliance on heuristics. It is also the most famous remaining gap in a family of visibility-type recognition problems where relatives (bar visibility, point visibility) are settled.

## What's already known?

- **The problem is open even with the boundary order given.** No polynomial algorithm and no hardness result is known for the exact ordered variant; this has been open since at least O'Rourke's 1993 column and is TOPP Problem 17.
- **Necessary conditions are known** (Ghosh's program): the visibility graph plus boundary order must admit a "visibility ordering" (an ordering of reflex chains at each vertex consistent with visibility), properties of "clumps"/"blocks", and the ε-neighborhood structure. These give polynomial-time **necessary** checks but no sufficiency.
- **Everett et al.** showed recognition is possible in polynomial time under an additional "ε-visibility" / ordered-visibility assumption stronger than the plain input (verify exact statement).
- **Pseudovisibility / pseudo-polygon visibility graphs** (O'Rourke–Streinu): realizability by pseudo-segment arrangements — a relaxation that is settled or nearly so, but it does not decide the straight-line model.
- **Point visibility graphs** (every point of the polygon is a vertex): recognized for certain subclasses; different model, doesn't settle this one.
- **Related complexity facts:** recognition of *segment* visibility graphs of arrangements was recently shown ∃ℝ-hard (Bertschi–Bhattiprolu–Fulek–Lochet, 2024-ish) — this is the closest hardness technique transferable here (verify). Nothing analogous is known for polygon vertex-visibility graphs; membership in ∃ℝ for the ordered version should follow from the obvious first-order sentence, but even that deserves a careful write-up.
- Every vertex-visibility graph with the cycle has: Hamiltonian boundary, all "blocks" along the cycle are intervals, vertices see all vertices of their own reflex chain except neighbors (verify details in Ghosh's book).

## What would count as solving it?

Any of the following, in decreasing order of strength:

1. **Recognition algorithm:** a polynomial-time (or ∃ℝ-decision-procedure) algorithm that, given (G, C), decides realizability and outputs coordinates. Even an algorithm in any "reasonable" complexity class (e.g., singly exponential) with a correctness proof would be major new progress — note there is currently *no* decision procedure at all.
2. **Hardness:** a proof that recognition is NP-hard, ∃ℝ-hard, or undecidable. This closes the "is it feasible?" question in the standard sense.
3. **Structural characterization:** a combinatorial characterization of realizable (G, C) pairs checkable in finite time, even if slow — this converts a real-algebraic problem into a finite one and is the classic route to 1 or 2.
4. **In NP?** Resolving whether every realizable pair has a realization with polynomially-bounded rational coordinates.

## How to start

1. **Read first:** O'Rourke's 1993 computational geometry column (the problem statement) and Ghosh's book *Visibility Algorithms in the Plane* (esp. chapters on visibility graph characterization — the visibility ordering, blocks, and clump machinery). These give every known necessary condition and explain exactly where sufficiency fails.
2. **Reproduce the ∃ℝ formulation:** write the first-order real sentence expressing realizability of (G, C) — simplicity of the polygon plus segment-interior conditions. Confirm membership in ∃ℝ rigorously; this is worth stating in print if not already.
3. **Try the hardness route:** study the Bertschi et al. ∃ℝ-hardness proof for segment visibility graphs and test whether its reduction gadgets (stretchability-based constructions) can be embedded inside polygon vertex-visibility recognition. The obstacle: vertices are constrained to a single boundary cycle, so gadget wiring is far more rigid.
4. **Try the structural route:** pick a subclass (e.g., triangulated visibility graphs / weakly externally visible polygons) and attempt full characterization + recognition; historical partial results (Everett et al.'s ε-condition) show this yields publishable stepping stones.

## Key references

- J. O'Rourke, "Computational geometry column 18" (SIGACT News / Int. J. Comput. Geom. Appl., 1993). States the recognition problem and surveys the state of the art as of 1993; the origin of the modern formulation (TOPP Problem 17). Link: via CGAL/ToP pages — the Open Problems Project, Problem 17: https://topt.cs.nuim.ie/p17.html (verify availability).
- J. O'Rourke and I. Streinu, "The vertex-edge visibility graph of a polygon," Comput. Geom. 11 (1998) and related pseudovisibility papers. Develop visibility via pseudo-edge/interval structures on a single vertex's fan — the "vertex-edge" relaxation that the census record cites.
- S. K. Ghosh, *Visibility Algorithms in the Plane*, Cambridge University Press, 2007 (esp. Ch. 2–3, 7). The definitive treatment of visibility graph properties: visibility orderings, clumps, Hamiltonian-cycle structure, and the known reconstruction attempts; contains the precise statement of the open recognition problem.
- M. Bertschi, V. Bhattiprolu, R. Fulek, H. Lochet, "The complexity of recognizing segment visibility graphs" (SoCG 2024 / arXiv 2023). Proves ∃ℝ-hardness for recognizing visibility graphs of segment arrangements — the closest hardness result and the natural technical template for an attack here (verify exact venue/year).
- H. Everett, "Visibility graph recognition," Ph.D. thesis / with S. A. (Louvain-la-Neuve) and follow-up papers on visibility orderings and ε-property recognition (verify exact citations via Ghosh's bibliography). Give polynomial-time recognition under an ordering assumption stronger than the plain input.

## Warnings

- **Convention traps:** whether boundary-cycle edges belong to G, and whether visibility means open vs. closed segment, changes the problem's fine structure. Fix conventions from Ghosh's book and state them.
- **Pseudovisibility ≠ visibility:** O'Rourke–Streinu's results are about a relaxation; do not cite them as solving the straight-line problem. Similarly, point-visibility and bar-visibility results do not transfer.
- **Ordered vs. unordered:** almost every partial result assumes the cyclic order. Claims must say which variant they address.
- **No decision procedure exists at all** — even a slow one — so "improved algorithm" framings are premature; the honest targets are decidability-in-∃ℝ write-ups, hardness, or characterization.
- Dead end repeatedly hit in the literature: the necessary visibility-ordering conditions are known to be insufficient in general; don't re-verify sufficiency for them without a new idea.

---
*`ALGO-000160` · unverified*

## Acceptance guidance

Any of the following, in decreasing order of strength:

1. **Recognition algorithm:** a polynomial-time (or ∃ℝ-decision-procedure) algorithm that, given (G, C), decides realizability and outputs coordinates. Even an algorithm in any "reasonable" complexity class (e.g., singly exponential) with a correctness proof would be major new progress — note there is currently *no* decision procedure at all.
2. **Hardness:** a proof that recognition is NP-hard, ∃ℝ-hard, or undecidable. This closes the "is it feasible?" question in the standard sense.
3. **Structural characterization:** a combinatorial characterization of realizable (G, C) pairs checkable in finite time, even if slow — this converts a real-algebraic problem into a finite one and is the classic route to 1 or 2.
4. **In NP?** Resolving whether every realizable pair has a realization with polynomially-bounded rational coordinates.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/ab32c89d-5052-4c05-92b2-20c2644b71b3?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000160.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000160)
