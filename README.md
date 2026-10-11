# Regression Benchmark: ECoG Finger-Flexion Decoding

Diagnostic benchmark comparing four regression methods for continuous
finger-flexion decoding from ECoG on BCI Competition IV, Dataset 4 (three
subjects, within-subject, 400 s train / 200 s test). The four methods span the
classical-linear → deep-learning spectrum and each operationalizes a specific
hypothesis rather than competing for a single "best" score.

## Methods

| Directory | Method | Hypothesis |
|---|---|---|
| `wiener/` | Wiener Filter (Liang & Bougrain 2012) | a linear, time-invariant map suffices |
| `switching_lm/` | Switching Linear Model (Flamary & Rakotomamonjy 2012) | per-state linear maps are needed |
| `fingerflex/` | FingerFlex (deep autoencoder) | a learned time-frequency representation suffices |
| `dtcnet/` | DTCNet | per-time-step supervision + retained ch-freq 2D structure |

## Evaluation protocol

- **Split**: fixed temporal, first 400 s train / last 200 s test, per subject.
- **Metrics**: official_r (mean Pearson correlation over the four fingers
  excluding the ring, the primary ranking metric), official_R² (variance
  explained vs. predicting the test-set mean), and calibration gap (per-finger
  r² − R², the error recoverable by an optimal affine rescaling).
- **Statistics**: per-finger Wilcoxon signed-rank tests (15 paired observations,
  5 fingers × 3 subjects) with Bonferroni correction; Cohen's d; Demšar CD
  diagrams.
- **Electrode QC**: method-specific (see the paper's Methods and Appendix F);
  all methods converge on the same four cross-verified bad channels
  (S1 ch55, S2 ch21+38, S3 ch50, 1-based).

## Results

| Method | official_r | official_R² | calibration gap |
|---|---|---|---|
| Wiener Filter | 0.460 | 0.054 | (see paper) |
| Switching Linear Model | 0.226 | negative | (see paper) |
| FingerFlex | 0.642 | (see paper) | (see paper) |
| DTCNet | 0.519 | −0.152 | 0.44 |

Full per-finger, per-subject tables and the statistical analysis are in the
paper (Results §3.1, Appendix C–E, H).

## Data

BCI Competition IV Dataset 4 (Miller & Schalk, 2008). Download instructions and
path configuration are in `data/README.md`. Each method reads the data from its
own `data/` or `code/data/` directory; see each method's README.

## Citation

If you use this benchmark, cite the original methods (per-method README) and the
dataset: Miller, K. J. & Schalk, G. (2008). BCI Competition IV, Dataset 4.
