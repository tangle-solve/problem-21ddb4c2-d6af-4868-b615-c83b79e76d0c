<!-- solve-problem:21ddb4c2-d6af-4868-b615-c83b79e76d0c -->
# Mansour’s conjecture

A [Tangle Solve problem](https://solve.tangle.tools/problems/21ddb4c2-d6af-4868-b615-c83b79e76d0c).

## What is the problem?

Let \(f:\{0,1\}^n \to \{0,1\}\) (or \(\{-1,1\}^n\to\{-1,1\}\)) be a DNF formula with at most \(s\) terms. Every Boolean function has a unique Fourier expansion \(f = \sum_S \hat f(S)\chi_S\) over parity characters \(\chi_S(x) = (-1)^{\sum_{i\in S}x_i}\). **Mansour's conjecture** (early 1990s) asserts: for every constant \(\epsilon > 0\), there exists a set \(S_\epsilon \subseteq 2^{[n]}\) of size \(\mathrm{poly}(s)\) (independent of \(n\), polynomial in \(s\), with constants depending only on \(\epsilon\)) such that

\[
\sum_{S \notin S_\epsilon} \hat f(S)^2 \le \epsilon .
\]

That is, an \(s\)-term DNF has all but \(\epsilon\) of its Fourier \(L_2\) mass concentrated on polynomially many coefficients. Mansour proved a weaker bound: concentration on \(\mathrm{poly}(s)\) coefficients captures all but \(1/\log(s)\) of the mass — the gap is between inverse-logarithmic and constant error. The precise exponent in \(\mathrm{poly}(s)\) is not fixed; even \(s^{O(1)}\) for each fixed \(\epsilon\) resolves the conjecture. A common strengthening asks for an *explicit/efficiently findable* set \(S_\epsilon\).

## Why does it matter?

A positive resolution would essentially settle the spectral complexity of DNF and directly imply an agnostically learnable class: Fourier concentration on a known polynomial-size set gives a \(2^{\mathrm{poly}\log(s)}\)-time (quasi-polynomial, and conjecturally subquadratic) algorithm for agnostically learning DNF under the uniform distribution via the low-degree/large-sieve algorithms of Kushilevitz–Mansour and Gopalan–Kalai–Klivans. It would also resolve a longstanding question in Boolean analysis on how DNF structure constrains the Fourier spectrum, with consequences for pseudorandomness and communication complexity of DNF-related functions.

## What's already known?

- **Mansour (1995):** Any \(s\)-term DNF is \(\epsilon\)-concentrated on Fourier coefficients of degree \(O(s^{1/\epsilon})\)-ish sets; more precisely his random-restriction+hybrid argument yields concentration on \(s^{O(1/\epsilon)}\) (or quasi-polynomial in \(s\) depending on \(\epsilon\)) coefficients up to error \(\epsilon\) in some formulations, but the canonical statement he left open is constant error on \(\mathrm{poly}(s)\) coefficients; his best general result gives error \(1/\log s\) on \(\mathrm{poly}(s)\) coefficients (verify exact exponents against the original paper).
- **Random DNF (2010, ECCC TR10-023, I. Harmalkides/… — verify authors):** The conjecture holds with high probability for DNF drawn from a natural random model.
- **Restricted/structural cases (arXiv:2109.04525, "Sharper Bounds on Fourier Concentration of DNFs"):** Improved concentration bounds, including for read-\(k\) DNF and DNF with bounded bottom fan-in / other parameter restrictions.
- Related: O'Donnell–Servedio showed DNF have total influence \(O(\log s)\); Friedgut's junta theorem gives concentration for low-influence functions; both fall short because individual DNF terms can have high influence/degree.

## What would count as solving it?

1. **Main goal (proof):** For every constant \(\epsilon>0\) and every \(s\)-term DNF \(f\), exhibit \(|S_\epsilon| \le s^{c(\epsilon)}\) with \(\sum_{S\notin S_\epsilon}\hat f(S)^2\le\epsilon\). Ideally \(S_\epsilon\) computable from \(f\) in \(\mathrm{poly}(n,s)\) time.
2. **Quantitative strengthening:** achieve \(|S_\epsilon| = \mathrm{poly}(s/\epsilon)\), matching the natural learning application.
3. **Negative direction (less expected):** a family of \(s\)-term DNF requiring \(\omega(\mathrm{poly}(s))\) coefficients for constant-error concentration, refuting the conjecture.

A referee would accept any of these with full proofs; partial progress (e.g., \(\epsilon = s^{-o(1)}\) error on \(\mathrm{poly}(s)\) coefficients) would be significant but not a resolution.

## How to start

1. Read Mansour's original paper (JACM 1995, "Learning Boolean functions via the Fourier transform") to pin down the exact statement and his restriction-based proof; identify precisely where the \(1/\log s\) barrier arises.
2. Read O'Donnell's *Analysis of Boolean Functions* Ch. 3–4 (Fourier concentration, DNF/decision trees) for the standard toolkit: Håstad's switching lemma, random restrictions, Friedgut's junta theorem.
3. Study arXiv:2109.04525 to see which structural parameters give sharp concentration and why the general case resists; look for a decomposition (e.g., by term influence) that reduces general DNF to the handled cases.
4. Main obstacle: terms of large width contribute high-degree Fourier mass that doesn't vanish under generic arguments; the switching lemma controls pointwise error, not \(L_2\) tail mass on polynomially many coefficients.

## Key references

- Y. Mansour, "Learning Boolean functions via the Fourier transform," *Theory and Computing Systems / J. ACM* (mid-1990s): introduces the Fourier-based learning framework for DNF and poses the concentration conjecture; proves the best general bounds. (Verify exact venue/year.)
- "Mansour's Conjecture Is True for Random DNF Formulas," ECCC TR10-023 (2010): proves the conjecture for DNF formulas drawn from a natural random distribution. (Verify authors — likely involves M. Harmalkides et al.; check ECCC page.)
- "Sharper Bounds on Fourier Concentration of DNFs," arXiv:2109.04525: improves concentration bounds for DNF, especially for restricted parameters (e.g., bounded term structure). https://arxiv.org/abs/2109.04525
- R. O'Donnell, *Analysis of Boolean Functions*, Cambridge Univ. Press, 2014: standard background on Fourier analysis of DNF, juntas, switching lemma. https://analysisofbooleanfunctions.org/
- E. Kushilevitz, Y. Mansour, "Learning decision trees using the Fourier spectrum," *SIAM J. Comput.* 1993: the KM/sieve algorithm that converts Fourier concentration into learning algorithms.

## Warnings

- The census record is vague on exact known exponents; verify Mansour's precise bounds in the original paper before building on them. Do not rely on the exponent \(O(1/\epsilon)\) stated above without checking.
- Ambiguity in the target: some statements require the coefficient set to be *found efficiently* from the formula; a pure existence proof is weaker — decide which variant you're attacking.
- Common dead end: naive term-by-term Fourier expansion — the product/union structure means tails from \(s\) terms must be summed without losing a \(\log s\) or \(s\) factor, which is exactly the hard part.
- Careful with the norm convention (\(\{0,1\}\) vs \(\{-1,1\}\) range) — it shifts constants.

---
*`ALGO-000229` · unverified*

## Acceptance guidance

1. **Main goal (proof):** For every constant \(\epsilon>0\) and every \(s\)-term DNF \(f\), exhibit \(|S_\epsilon| \le s^{c(\epsilon)}\) with \(\sum_{S\notin S_\epsilon}\hat f(S)^2\le\epsilon\). Ideally \(S_\epsilon\) computable from \(f\) in \(\mathrm{poly}(n,s)\) time.
2. **Quantitative strengthening:** achieve \(|S_\epsilon| = \mathrm{poly}(s/\epsilon)\), matching the natural learning application.
3. **Negative direction (less expected):** a family of \(s\)-term DNF requiring \(\omega(\mathrm{poly}(s))\) coefficients for constant-error concentration, refuting the conjecture.

A referee would accept any of these with full proofs; partial progress (e.g., \(\epsilon = s^{-o(1)}\) error on \(\mathrm{poly}(s)\) coefficients) would be significant but not a resolution.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/21ddb4c2-d6af-4868-b615-c83b79e76d0c?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000229.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000229)
