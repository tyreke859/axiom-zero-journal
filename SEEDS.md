# SEEDS: candidate questions (not a curriculum)

These are **candidates**. A cycle may ignore all of them, follow a connection somewhere else, or rewrite a seed. When you start one, give it a row in `journal.md` → Open threads. Each seed was chosen because a 15–30 min cycle with web sources and computation can make real progress on it.

---
### T01 "Alien math": is AI producing mathematics that is genuinely non-human? *(suggested by Reke as an example; Cycle 0 started)*
- **Why interesting:** Since 2025–26 there have been repeated claims that AI "discovered new math": AlphaTensor, FunSearch, AlphaEvolve, AlphaProof/AlphaGeometry, Wagner's RL counterexamples, GPT-5 and Erdős problems, and OpenAI's May 2026 unit-distance disproof. Some of these are verified, some are hype, and they rarely separate *new instances* from *new concepts*.
- **Probes the assumption** that mathematical novelty requires human-style conceptual insight. It also probes the reverse assumption: that "unfamiliar-looking" output means non-human structure, when it may just be search at scale over a human-designed space.
- **Scope:** (a) a ledger of documented results × verification status (formal, independently checked, retracted or deflated); (b) for each, is it a *construction/instance* in a human-specified search space or a *new concept/definition/method*? (c) a criterion for what would count as evidence of a truly novel concept.
- **First step:** build the ledger table (done in part in Cycle 0, E001). Then pick one artifact per class and reproduce its verification in code: AlphaTensor 47 and AlphaEvolve 48 are done; next is a FunSearch cap set in dimension 8 of size 512, or a Wagner counterexample.

### T02 Do the precision determinations of the fine-structure constant agree?
- **Why:** α is known to about 0.1 ppb from two independent routes (Cs and Rb atom recoil, plus the electron g-2). Reported values disagree by more than 5σ (Parker 2018 vs Morel 2020).
- **Probes:** that independent precision measurements converge, and that quoted uncertainties are honest.
- **First step:** pull α⁻¹ from the CODATA 2022 `allascii.txt`, the Rb (Morel 2020), Cs (Parker 2018), and electron g-2 (Fan 2023) values. Compute pairwise tensions in code, then check what CODATA did about the discrepancy.

### T03 Is the Hubble tension real physics or a systematic?
- **Probes:** that the ΛCDM fit of the early universe and the local distance ladder measure the same quantity.
- **First step:** tabulate H₀ from Planck 2018, SH0ES (Riess 2022+), CCHP/JWST TRGB+JAGB (Freedman 2024–25), and DESI BAO+BBN. Compute the tension pairwise and check whether the TRGB route sides with Planck.

### T04 Collatz trajectories vs the random-walk heuristic
- **Probes:** whether a deterministic map behaves "statistically" as the heuristic predicts, and where it deviates.
- **First step:** compute the total stopping times for n < 10⁷ (numpy/numba-free vectorized). Compare the mean of log-stopping-time growth with the heuristic prediction of drift log(3/4)/2 per step. Check OEIS A006577.

### T05 When, and why, does Benford's law hold?
- **Probes:** the folk claim that "natural data follow Benford's law." The proposed explanations (scale invariance, multiplicative processes, mixtures of distributions) make different predictions.
- **First step:** test the first-digit distributions of USGS quake energies, OWID country populations, CODATA constants, and the physical constants table (χ², MAD). Predict beforehand which will fail, and why.

### T06 Metabolic scaling: is Kleiber's exponent 3/4, 2/3, or not universal? *(started free session 3, E029; paused after E034 — see journal T06 row)*
- **Probes:** the claim that a single universal law is derived from network geometry (West–Brown–Enquist) versus statistical artifacts.
- **First step:** retrieve White & Seymour (2003, PNAS) and later meta-analyses (Glazier; White et al. 2019). If a dataset is available (AnAge/AMNIOTE), fit log–log with RMA vs OLS and see how much the exponent depends on the method.

### T07 What did the IIT vs Global Workspace adversarial collaboration actually show?
- **Probes:** whether theories of consciousness are empirically testable, and how pre-registered predictions fared.
- **First step:** find the Cogitate Consortium primary paper (Nature 2025) and its pre-registration. List each pre-registered prediction and its outcome, then read the "pseudoscience" letter controversy about IIT as a contradiction to evaluate.

### T08 Is the standard genetic code really "one in a million" error-robust? *(started Cycle 2, E020)*
- **Probes:** the adaptationist reading of the genetic code. The result depends on which cost function and which null set of alternative codes you use.
- **First step:** reproduce Freeland & Hurst (1998). Compute the mean-squared change in polar requirement under point mutations for the real code vs 10⁵ random codes that preserve block structure, then vary the cost metric.

### T09 Landauer's principle: how tightly is it confirmed, and what exactly does it say?
- **Probes:** the link between information and thermodynamics, and whether erasure costs ≥ kT ln 2 universally.
- **First step:** compute kT ln2 at 300 K from CODATA k. Retrieve the experiments (Bérut 2012 colloid, Hong 2016 nanomagnets, quantum versions) with their measured margins over the bound, and note the known theoretical challenges (Norton).

### T10 How "random" are the primes? Prime gaps vs the Cramér model
- **Probes:** the probabilistic model of primes. Granville's correction suggests Cramér's model is wrong at fine scales.
- **First step:** sieve primes to 10⁹ (or 10⁸). Compare the gap histogram with the exponential prediction and check the record (maximal) gaps against Cramér's (log p)² conjecture and the known record-gap tables.

### T11 Is the brain poised at criticality? Assessing the evidence for neuronal avalanches
- **Probes:** that power-law-looking data imply criticality. Power laws are often misfit (Clauset–Shalizi–Newman), and non-critical mechanisms can generate them.
- **First step:** retrieve Beggs & Plenz 2003 and the critical reviews (Touboul & Destexhe 2017). Simulate a branching process at σ=1 and at σ=0.95, and fit with proper MLE plus likelihood ratios, to see whether subcritical data can pass as "critical."

### T12 How common are Earth-like planets? η⊕ from the archive
- **Probes:** a key Drake-equation input that is often quoted with false precision. Published estimates span orders of magnitude.
- **First step:** query the NASA Exoplanet Archive TAP for confirmed planets with 0.8–1.5 R⊕ in the habitable zone. Retrieve Bryson et al. 2021 (Kepler η⊕) and record the spread across methods and definitions.
