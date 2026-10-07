# Notes on the OpenAI Hikita preprint

Source: family 044 of the `openai/math` release (24 Sep 2026),
`preprints/The-equivariant-cohomological-Hikita-conjecture-for-arbitrary-quivers-September-24-2026/`.
Local clone: `~/GitHub/openai-math`.  No Lean formalization for this family.

Status vocabulary: [proved] / [checked] / [plausible] / [hope] / [unknown],
as in research-mode.  Nothing below has been verified against the proofs;
"the paper claims" throughout.

## What the paper does (2026-10-06)

- Proves the equivariant cohomological Hikita conjecture (Dumanski–Krylov
  Conj. 2.1, eq. (2.3)) for every finite quiver, loops and multiple arrows
  included, any flavor torus, any *regular* stability (semistable = stable,
  free action).  Keeps nilpotents; includes the empty case.
- Previously known: Jordan quiver (Krylov–Shlykov), finite type ADE with
  E7/E8 framing restrictions (Dumanski–Krylov).
- Not covered: quantized version, non-GL gauge groups, K-theory.  Paper
  cites Hoang–Krylov–Matvieievskyi Ex. 6.7 for a failure outside the quiver
  setting — **not yet read; check which hypothesis fails there.**

## Structure of the proof

Chain `C[Y^ν] → B_F → H*_F(X)`, where `B_F` = coordinate ring of the
full-topological-torus fixed scheme.  Two independent halves:

1. `B_F ≅ H*_F(X)` (§§3–7):
   - stable-pair vanishing-cycle test gives `B_F ↠ H*_F(X)` for all data;
   - add a loop at every vertex, no flavor, det stability: Laurent model
     (loop weights cancel Grassmannian Euler denominators), multipartition
     filtration, cut ideals, Hilbert series matched to Hausel's formula →
     equality;
   - remove loops by giving them mass z, localize at (x,z)=(0,1), descend
     homogeneous ideals; other regular stabilities by Betti constancy;
     flavor by graded Nakayama.
2. `C[Y^ν] ≅ B_F` (§8): adjoin a rank-1 framing vertex; central monopole z
   gives `M^+_b = z M^-_{d-b}`; polynomial CoHA (Jindal–Neguț, Tsymbaliuk)
   decomposes surviving monopoles into Kac-support charges of weight 0;
   Crawley-Boevey lifting + direct sum gives a semistable point with
   positive-dimensional stabilizer, contradicting regularity.

## Verification (2026-10-06)

Seven independent adversarial readings, one per section; see
`VERIFICATION.md`.  [checked] No error or load-bearing gap found; ~15
explicit computations agree; external citations that were fetched (BFN18,
Weekes, Hoskins, MN18, Tsymbaliuk, Jindal–Neguț) say what the paper says.
Issues are all presentational (16 listed).  Hausel's formula was checked
from memory, pinned by the Jordan v=1 sign check.  The one convergent flag
(degree convention in Prop 2.2) resolved: it is BFN Lemma 2.6's grading,
differing from 2Δ(λ) by ⟨det N, λ⟩ — charge-dependent only, harmless.

## Precedent for the added-loop step

The paper does not claim the trick is new and cites no direct precedent.
It cites Krylov–Shlykov Rem. 1.15 for "deformation arguments" and
Dumanski–Krylov Prop. 2.3 for prequotient localization.  The denominator
cancellation itself is attributed only to the Grassmannian tangent-weight
calculation (cf. Weekes Lemma 2.10).  [unknown] whether anyone has used
loops this way for Hikita before — not searched.

## Ben's suggestion: general (G,N) via a copy of the adjoint (2026-10-06)

- [plausible] Massless adjoint summand contributes
  `∏_α α^{(−⟨α,λ⟩)_+}` to the abelianized monopole of *any* coweight λ, which
  cancels `eu(T_{t^λ} Gr^λ)` up to sign (tangent weights of Gr^λ at t^λ are
  roots α with ⟨α,λ⟩>0, multiplicity ⟨α,λ⟩, at ħ=0 — recalled, not checked).
  So the Laurent-model step works for all λ, not just minuscule.
- [plausible] Mass-deformation removal (§7) is not quiver-specific.
- Quiver-specific as written, no replacement in hand:
  - minuscule generation (Weekes) — many G have no minuscule coweights;
  - Kirwan surjectivity (McGerty–Nevins is for quiver varieties);
  - cut-ideal count vs Hausel (GL/S_n combinatorics);
  - Part II entirely (Kac support, CoHA).
- [proved] Semisimple G has no nontrivial characters, so regularity needs
  a big center: interesting cases are products of GL's with non-quiver N
  (Sym², Λ², tensors), or GL×Sp mixtures.
- Next: read HKM24 Ex. 6.7; try GL₂, N = Sym²C² ⊕ C², det stability by hand.

## Files

- `hikita-summary.tex/.pdf` — reader's guide for SLMath QFT participants.
- `openai-preprint/` — verbatim copy of the preprint directory (PDF, source,
  OpenAI's README with BibTeX, the CONTENTS.md entry, Apache-2.0 LICENSE).
