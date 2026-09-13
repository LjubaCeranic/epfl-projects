# EPFL projects

Selected quantum computing and machine learning projects from my studies at EPFL — BSc Physics,
now MSc Quantum Science and Engineering, specialising in Quantum Information.

[LinkedIn](https://www.linkedin.com/in/ljubomirceranic)

> The code for the machine learning projects lives in private EPFL course repositories and is not
> mine alone to publish — EPFL reuses projects between years. The written reports are here in full.

---

## Factoring an Integer with Three Oscillators and a Qubit — a mathematical and energetic analysis

**QUANT-401 Project in Quantum Science I · EPFL · supervised by Prof. Nicolas Macris · grade 5.25/6**
**Single author.**
📄 **[Read the report](Shor_three_oscillators_report.pdf)** (34 pages)

A detailed analysis of the factoring algorithm of Brenner, Caha, Coiteux-Roy and König, which
factors an integer *N* using only three bosonic oscillators and a single qubit — independent of the
size of *N*. It reaches Shor's polynomial-time complexity by replacing modular arithmetic with real
arithmetic on continuous-variable position states, and the discrete Fourier transform with a
homodyne *P*-quadrature measurement.

The report develops the continuous-variable formalism from scratch, derives the action of every gate
in the circuit, analyses the idealised algorithm in full, and proves correctness of the physical
finitely-squeezed version together with its error bounds. Detailed proofs and technical lemmas are in
the appendices.

**The energetic analysis**

Beyond reproducing the protocol, the report asks what it would actually cost to run. The GKP states
the algorithm needs must be extremely tightly squeezed, and squeezing costs oscillator energy:

- Total energy scales as **2^Θ(n²)** where *n* = ⌈log₂ N⌉ — exponential in the *square* of the bit
  length, not in the bit length.
- For a **two-digit** modulus the requirement already exceeds the mass-energy of the observable
  universe (~4 × 10⁶⁹ J) by a factor of ~10⁴³⁷.
- For a **three-digit** modulus it exceeds it by ~990 orders of magnitude.
- Because the exponent grows as n², one extra bit multiplies the cost by ~10⁵⁴. The requirement
  vaults from nuclear-arsenal scale to beyond-the-universe scale within a single bit — there is no
  integer whose cost lands at an intermediate stellar or galactic scale.
- Restated in occupation number, the dominant mode would have to sit at roughly its 10¹⁰⁸³-th energy
  level for a three-digit modulus.

The conclusion is a trade-off worth stating plainly: the protocol buys a constant number of modes at
the price of an energy requirement that is not merely impractical but unphysical.

---

## Sharpness, Batch Size and Generalization — a controlled study of SGD and Adam

**CS-439 Optimization for Machine Learning · 2026 · with Alexandre Carel and Hervé Sérandour**
📄 **[Read the report](OptML_report.pdf)**

How does mini-batch size, and the choice between SGD and Adam, shape the curvature of the minimum a
CNN converges to on Fashion-MNIST — and does that curvature predict generalization?

Across 36 runs (six batch sizes × two optimizers × three seeds) we measured the top Hessian
eigenvalue by power iteration on Hessian-vector products, a random-direction sharpness probe, and
test accuracy, plus the loss along the linear interpolation between an SGD and an Adam minimum, and
Adam's curvature in its own preconditioned geometry.

**Findings**

- Sharpness rises steeply with batch size for both optimizers — roughly 23× for SGD from batch 32 to
  1024 — reproducing the Keskar et al. large-batch effect.
- Adam reaches sharper minima than SGD at every batch size, by 4× to 30× in raw top eigenvalue.
- Yet test accuracy stays within a narrow 89–92% band across that whole range. Raw sharpness is a
  weak predictor of generalization within an optimizer and an unreliable one across optimizers.
- The raw Hessian is the wrong ruler for Adam: in its preconditioned geometry the top eigenvalue is
  50–90× larger and climbs toward the edge-of-stability scale, so cross-optimizer raw-Hessian
  comparisons do not mean what they appear to.

---

## Neural Architectures for Tweet Sentiment Analysis — a comparative study

**CS-433 Machine Learning, project 2 · with Ondrej Zedka and Rouzbeh Jeiranzadeh**
📄 **[Read the report](ML_project2_report.pdf)**

A controlled comparison of four architectures — MLP, 1D CNN, LSTM and a transformer encoder — for
binary sentiment classification on tweets whose smileys have been stripped out. Input representations
are GloVe embeddings trained from scratch on the corpus co-occurrence statistics, at 20 and 100
dimensions, over training sets of 200,000 and 2.5 million tweets.

**Findings**

- More data helps, but capacity decides who benefits. The MLP gains almost nothing from 200k → 2.5M
  (0.7321 → 0.7995 at best), being capacity-limited rather than data-limited; the sequence models
  gain substantially.
- **The 1D CNN reached 86.25% validation accuracy, effectively matching the LSTM (86.31%)** while
  remaining fully parallelisable and far cheaper to train.
- For short, informal text, a lightweight convolutional model over local n-gram patterns is the
  better accuracy-per-unit-compute choice than a recurrent one.
- Training on the full 2.5M set on consumer hardware required a lazy-loading dataset that builds
  sequences on the fly rather than holding the corpus in memory.

---

## Coronary Heart Disease Prediction from Survey Data

**CS-433 Machine Learning, project 1 · with Ondrej Zedka and Rouzbeh Jeiranzadeh**
📄 **[Read the report](ML_project1_report.pdf)**

Predicting coronary heart disease from the BRFSS 2015 health survey — a large, noisy, ~90/10
imbalanced dataset of nearly 300 mixed-type features. **The six learning methods used here were
implemented from scratch, without any machine learning library.**

**Approach**

- Mapped the survey's per-column missing and refusal codes (7, 8, 9, 77, 99, 999…) to NaN, dropped
  administrative columns and features above 95% missing, then imputed by mean or mode according to
  feature type and standardised the continuous ones.
- Correlation-based feature selection (|r| ≥ 0.05 to target, dropping one of any pair above 0.95),
  then a degree-2 polynomial expansion to ~2,500 features, then stricter re-filtering
  (|r| ≥ 0.1, inter-correlation ≤ 0.75).
- Majority-class undersampling for the imbalance, and a decision threshold swept in steps of 0.005
  to maximise F1 rather than accuracy.
- 4-fold cross-validation over λ; validation loss rose monotonically with λ, so the final model uses
  no regularisation — 326 parameters against 238,588 training samples was not at risk of overfitting.

**Result: F1 = 0.433 on AIcrowd**, on a dataset where accuracy is a meaningless metric.

---

## Notes

Reports are the authors' own written work, shared with their agreement. Course code is deliberately
not published. The quantum report is single-author and published with my supervisor's agreement.
