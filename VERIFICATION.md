# Verification notes on the OpenAI Hikita preprint

Date: 2026-10-06.  Target: `openai-preprint/build/` (release of 24 Sep 2026).

## How this was done, and what it is worth

Each of the seven mathematical sections (§2–§8) was read independently by a
separate Claude instance acting as an adversarial referee, with
instructions to recompute every formula it could, classify each step as
CORRECT / GAP / ERROR / NEEDS-BACKGROUND, and tag its own confidence
([proved] / [checked] / [plausible] / [unknown]).  The §2 and §8 readers
fetched the cited external papers (BFN18, Weekes, Hoskins, McGerty–Nevins,
Tsymbaliuk 2207.02804, Jindal–Neguț 2607.23544) and checked citations
against the sources; the other readers worked from the preprint and memory.
The reports were then reconciled here.

This is **not** a human referee report.  It is a careful machine reading
that found the argument internally consistent and the checkable
computations correct.  It can miss a subtle error that a specialist would
catch, and it inherits any shared blind spots of the model.  Treat it as
raising the prior that the paper is right, not as settling it.

## Overall verdict

**No mathematical error and no load-bearing gap was found in any section.**
Every computation that could be redone by hand was redone and agreed
(a dozen explicit checks are listed below).  All cited external results
that were looked up say what the paper says they say.

The issues found are all presentational: terse steps that a reader would
need expanded, citations that should be made precise, and conventions that
should be stated once.  They are collected in §"Recommended expansions."

## Section-by-section

### §2  Coefficient rings, minuscule classes, flavor — CORRECT [checked]

- Abelianization formula (2.2) rederived; matches BFN18 Prop 6.6 verbatim.
  The one-sided exponent `(−⟨β,λ⟩)_+` reproduces BFN's symmetric structure
  constants via `2(−a)_+ = |a| − a`.
- **Degree convention.**  `deg M_{λ,p} = 2c_λ − 2a_λ + deg p` is exactly
  BFN18 Lemma 2.6 (the `N_O`-relative grading).  It is *not* the symmetric
  physics degree `2Δ(λ) = Σ|⟨β,λ⟩| − 2 dim Gr^λ`; the two differ by
  `−⟨det N, λ⟩`, a function of `[λ] ∈ π₁(G)` only (BFN18 Rem. 2.8(2)).
  They agree on charge zero, so `B_F`, neutral words and all Hilbert-series
  comparisons are unaffected.  Three independent readers (§2, §3, §5)
  flagged this; the paper should say it in one sentence.
- Weekes's generation theorem: Prop 3.1 there covers arbitrary quivers with
  loops/multiple arrows (Rem 3.4, §1.4) and `ħ=0` (Rem 3.3).  The flavor
  extension is asserted in Weekes §1.6.1 "with minor changes"; the paper's
  own one-line justification (sign pattern of `⟨β,·⟩` uses gauge components
  only) is correct and should be presented as the argument.
- Lemma 2.1 silently deletes loops at rank-one vertices — harmless, worth a
  sentence.  Lemma 2.5: "finitely many cones" is true because `C(gx)`
  depends only on `wt_T(gx) ⊆ wt(N⊕N*)`, but no reason is given.
- McGerty–Nevins assume `w ≠ 0`; for `w = 0` regularity forces `D = ∅`,
  covered by the empty case — one clause would close it.

### §3  Finite correspondences — CORRECT [checked]

- Hom/Borel–Moore identification and the degree bookkeeping `q_j` recomputed;
  `Σ q_j = d` telescopes correctly (toy check: `G = C^×`, `N = C`,
  word `M_{+1}M_{−1} = x`, shifts `(2,0)`, `d = 2`).
- Freeness of `H_*^{T×F}(C_Z)` via orbit strata: strata are vector bundles
  over affine bundles over partial flag varieties; even and free.  Loop
  scaling is unnecessary but harmless.  Weight-zero summands of `N` only
  affect fibers.
- Faithfulness holds on the *full* Hom space (torsion-free ↪ localized iso).
  Whole-fiber classes `e^η` correctly avoid zero Euler classes.
- Chain calculation: Chriss–Ginzburg 8.6.7 applies verbatim (all three
  spaces smooth at each step; `u_j, v_j` need not be smooth).
- **Key structural remark, worth stating in the paper:** the section never
  needs `Ψ_w` to *equal* BFN convolution, only that both sides of the
  factorization have the same localized image.  This is what makes
  reordering the word legitimate.
- Minor non sequitur: "fiber ranks at the endpoint equal `r`" — what is used
  is that `S_{B_k} → S_Z` is an isomorphism on fibers.

### §4  Stable-pair test — CORRECT [proved / checked]

- Lemma 4.1 (degree of character line bundle): all three steps checked.
  "Relatively ample over the affine quotient ⇒ ample on the fiber" is right;
  one could also just say a nonconstant map from `P¹` is finite onto its
  image.  Regularity delivers King-stability (closed orbit + finite
  stabilizer), which is what "fiber = single orbit" needs.
- Support lemma: product-chart vanishing of `φ` off the critical locus is
  valid for the constant sheaf over a singular base.
- Quadratic lemma: `W_crit = ⟨μ(s,p), ξ⟩ = 0` recomputed two ways.
  **Expository gap:** Massey's Thom–Sebastiani is for a product with a
  product function; on Borel approximations one needs the vector-bundle
  version, where `Φ_q C` is the base constant sheaf ⊗ a rank-one local
  system with monodromy `det : O(q) → ±1`.  The sentence "structure group
  acts as `g ⊕ g^{−T}`" is the right fact (`det = 1`, so the group lies in
  the connected `SO(q)`) but should say so.
- **Expository gap:** the two identifications in (4.x) — direct over `D`,
  and pushed from `U×D` along `j` — are asserted compatible without
  argument.  Harmless: any discrepancy is a unit in `H⁰_K(D)`, and
  `u·unit·1 = 0 ⇒ u|_D = 0` still.
- Nice observation: one-factor words cannot occur (a nontrivial minuscule
  coweight has nonzero charge), so `k_w ≥ 2` automatically and "nonzero
  charge AND nonpositive degree" is automatic for the chosen first step.
- Citation hygiene: `\cite[Theorem, pp. 1–2 of the arXiv preprint]{Massey99}`
  while the bib entry is the Compositio 2001 article.

### §5  Laurent model — CORRECT [proved / checked]

- Loop cancels `eu(T Gr^λ)`: verified for `GL₂`, `λ = (1,0)`; ratio `−1` at
  both fixed points; general sign `(−1)^{|I|(v_i−|I|)}`.
- Induction on `‖λ‖²`: `f, g` nondecreasing with `f+g = id`, `fg ≥ 0`, so
  `r_α r_γ = r_λ`; rearrangement inequality and uniqueness of the
  decomposition at the fixed representative both check; generation
  `P^{W_λ} = ⟨P^{W_α}, P^{W_γ}⟩` verified for `λ = (2,1,0)`.
- Derivation `D_{i,k}`: Leibniz, `W`-equivariance, preservation of the
  algebra and the charge ideal, and vanishing on `B_0` all check.
- Cut excess `u_+ + v_+ − (u+v)_+` = 0 for same weak sign, `min(|u|,|v|)`
  otherwise — gives exactly `q_S`.
- Reynolds averaging and `δ_m` both check.
- Checks: Jordan `v=2, w=1` gives `1 + q` ✓; Jordan `v=2, w=2` gives
  `1 + q + 2q² + q³`, agreeing with Nakajima–Yoshioka ✓.

### §6  Cut ideals and Hausel — CORRECT [checked]

- Nullstellensatz lemma, reachability stratification, `Z_S = L_S ∩ U_r`,
  `e_S = q_S`, injectivity of `e_S` over a non-reduced ring (top-form
  argument), Gysin splitting, and "no binomial multiplicity"
  (`(Ind_H^G M)^G = M^H`) all check.
- Recurrence verified numerically on a case with `b ≠ 0`.
- Hyperkähler rotation: `Sp(1)` acts on the flat quaternionic `T*N` commuting
  with `G_c`; no compactness needed; Kempf–Ness on the closed affine
  subvariety `μ_C^{−1}(cη)`.
- **Hausel's formula reconstructed from memory** by the reader, but the
  transcription is pinned by the Jordan `v=1, w=1` check (any sign flip
  gives `−1` or `q` instead of `q^{−1}`) and consistent with `v=2`.
  `E_Q(λ) = D_m` after loop removal and `δ = C(v) + w·v` check.
- Checks: Jordan `v=2,w=1` → `1+q` ✓; `A₁`+loop `v=1,w=2`
  (`X = C² × T*P¹`) → `1+q` ✓; `A₂`+loops `v=w=(1,1)` → `1+2q` ✓.
- Cosmetic: the Poincaré-duality identity `P_c(u) = u^{2δ}P(u^{−1})` is in
  half-degree variables; say so.

### §7  Deformations — CORRECT [checked]

- Betti independence: rotation, constructibility of `Rπ_!C`, perturbation
  into the good open set, Poincaré duality with `dim = 2(dim N − dim G)`,
  empty case — all check.  The "clear denominators, dilate by inverse square
  root" sentence is confusing; the closing dilation remark
  (`μ(ax) = a²μ(x)`) is the load-bearing one and should replace it.
- Flavor lift: Leray–Hirsch, `Tor₁` vanishing, graded Nakayama (`B_F` is
  nonnegatively graded because `R → B_F` is a graded surjection) check.
- Loop removal: `E_λ` is exactly the loop's contribution to (2.2);
  `Δ_λ(0,1) = 1`; both algebras embed in a common fraction ring where
  `R_0[z]∖0` is invertible, so the localized algebras coincide (not just
  generators).  Brion's "Lemma 4" could not be confirmed; the needed
  statement is the Borel/Hsiang/Quillen localization theorem (finitely many
  isotropy types; no compactness), e.g. GKM §6.  `(D⁺)^H = D` including
  stability checks.  Homogeneous-ideal descent is standard and correct.
- Theorem 7.4: order of quantifiers is sound.  Implicit input: `det` is
  regular for arbitrary quivers with loops — established in §6 (the
  cyclicity argument); cross-reference it.

### §8  Cocharacter fixed scheme — CORRECT [checked against sources]

- Opening example verified (regular, `ν·(1,1) = 0`, joint monopole dies).
- Lemma 8.1: Tsymbaliuk (80) kernel, order table, `D`-convention, sign
  `(−1)^{L⁺·n + κ(n)}`, and specialization `ħ → 0` (a ring map from the Ore
  ring; no `ħ` or `u_a` ever inverted in `C_S`) all check against the
  source.  Theorem 5.7 there is on the *big* shuffle algebra, so no wheel
  conditions are needed.
- Lemma 8.2: JN Prop 3.14 + (122) give support exactly `Δ_Γ`, with the
  implication in the right direction (each cohomological degree in its own
  power of `t`, no Euler-characteristic cancellation).  Generation over `S`
  suffices.
- Lemma 8.3: Chevalley/constructibility passage to char 0, Crawley-Boevey
  lifting, Kempf–Ness, rotation — all [proved].
- Prop 8.4: the central splitting is exact — under `(g,c) ↦ (cg,c)` the
  `GL₁` at `∞` scaling `Hom(V_i, C)` is cancelled by the diagonal scalar in
  `G`.  Complementary-monopole identity is an exact equality from (2.2).
  Only injectivity of `B_ν → B_ν ⊗ C[ξ, z^±]` is needed, not faithful
  flatness.  Direct-sum stabilizer count and final ideal equality check.
- **Expository:** the one-arrow example meant to show the sign twist is
  necessary has trivial twist (`n_j m_i = 0`); the opposite order
  (`e_{(0,1)}` then `e_{(1,0)}`) is where the untwisted product fails.
- Residual: JN Thm 2.4 is only sketched in its source ("completely
  analogous to …").

## Recommended expansions (for a readable version)

Conventions to state once:
1. The grading is BFN's `N_O`-relative one (BFN18 Lemma 2.6), not `2Δ(λ)`;
   they differ by `⟨det N, λ⟩` and agree on charge zero.  (§2)
2. Sign convention for the dual action `ξ·p`.  (§4)
3. Half-degree variables in the Poincaré-duality identity.  (§6)

Steps to expand:
4. Equivariant Thom–Sebastiani: bundle version + `det(g ⊕ g^{−T}) = 1`.  (§4)
5. Compatibility of the two vanishing-cycle identifications, or the
   remark that only a unit's worth of ambiguity matters.  (§4)
6. Why the chain correspondence need not equal convolution — only
   localized images are compared.  (§3)
7. Why there are finitely many cones in Lemma 2.5.  (§2)
8. The `w = 0` case before invoking McGerty–Nevins.  (§2)
9. Replace the "inverse square root" sentence by the dilation remark.  (§7)
10. Cross-reference regularity of `det` (§6) from Theorem 7.4.  (§7)
11. Fix the one-arrow sign-twist example.  (§8)

Citations to make precise:
12. Chriss–Ginzburg 8.6.7 for convolution composition.  (§3)
13. Massey: cite the Compositio theorem number.  (§4)
14. Brion "Lemma 4" → standard localization theorem (Hsiang / GKM 6.2).  (§7)
15. Present the flavor extension of Weekes's theorem as the paper's own
    argument.  (§2)
16. Maxim–Schürmann / Schnürer–Soergel proposition numbers.  (§3, §4)

## Background a non-specialist would need

In rough order of appearance:
- BFN Coulomb branches: the space of triples, convolution, abelianization,
  the `N_O`-relative grading, dressed monopoles.  (BFN18 §§2, 5, 6)
- Minuscule generation for quiver gauge theories.  (Weekes 2019)
- King's affine GIT with a character; Kempf–Ness; Hilbert–Mumford cones.
  (King 1994; Hoskins 2014)
- Hyperkähler rotation on a flat quaternionic representation.  (HKLR §3(D))
- Equivariant Borel–Moore homology, localization, Hom ↔ BM via dualizing
  complexes; convolution composition.  (Chriss–Ginzburg ch. 8)
- Vanishing cycles, Thom–Sebastiani, compatibility with proper pushforward.
  (Maxim–Schürmann; Massey)
- Kirwan surjectivity for quiver varieties.  (McGerty–Nevins)
- Hausel's arithmetic Fourier transform formula.  (Hausel 2006)
- Kac polynomials; Crawley-Boevey's lifting lemma.
- Cohomological Hall algebras, BPS Lie algebras, shuffle algebras, and
  their difference-operator realizations.  (Jindal–Neguț; Tsymbaliuk)

## Explicit computations performed

| Check | Result |
|---|---|
| Statement, `A₁`, `v=1,w=2`, `ν=det` | `C[x]/(x²)` both sides ✓ |
| Statement, `v=1,w=1` | `C` both sides ✓ |
| §3 toy word `M₊M₋ = x`, `G = C^×`, `N = C` | shifts `(2,0)`, `d=2` ✓ |
| §5 loop cancellation, `GL₂`, `λ=(1,0)` | ratio `−1` at both fixed points ✓ |
| §5 generation `P^{W_λ}`, `λ=(2,1,0)` | ✓ |
| §5 Jordan `v=2,w=1` bound | `1+q` ✓ |
| §5 Jordan `v=2,w=2` bound | `1+q+2q²+q³` = Nakajima–Yoshioka ✓ |
| §6 recurrence, one vertex, `c₁₁=2`, `w=1`, two slots | ✓ |
| §6 Hausel `v=1` Jordan (pins signs) | `q^{−1}` ✓ |
| §6 Hausel `v=2` Jordan | `q^{−2}(1+q)` ✓ |
| §6 `A₁`+loop `v=1,w=2` | `1+q` ✓ |
| §6 `A₂`+loops `v=w=(1,1)` | `1+2q` ✓ |
| §8 opening example | regular, joint monopole dies ✓ |
| §8 Tsymbaliuk kernel / order table / signs | match source ✓ |
| §8 central splitting `(g,c) ↦ (cg,c)` | scalar cancels on `Hom(V_i,C)` ✓ |
