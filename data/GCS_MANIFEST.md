# Google Cloud Storage Data Manifest

All large data files (docking scores, surrogate models, raw results) are stored in Google Cloud Storage (GCS) for reproducibility and to keep the GitHub repository lightweight.

## Storage Location

**GCS Base Path**: `gs://aegismind-tpu-results/aegis_flashoptim/`

---

## Phase Data

### Phase 38–39: Molecular Docking (MSH3 ATPase)

| File | GCS Path | Size | Format | Description |
|------|----------|------|--------|-------------|
| **vina_scores.json** | `phase39_msh3_rdkit/vina_scores.json` | ~2.5 MB | JSON | AutoDock Vina scores for 1,759 compounds; pKd estimates (kcal/mol converted to µM Kd) |
| **features.json** | `phase39_msh3_rdkit/features.json` | ~12 MB | JSON | RDKit Morgan fingerprints (2048 bits) for all 1,759 compounds |
| **structures.sdf** | `phase39_msh3_rdkit/structures.sdf` | ~45 MB | SDF | 3D structures of all docked compounds |
| **msh3_3thw_chainA.pdbqt** | `phase39_msh3_rdkit/receptor/msh3_3thw_chainA.pdbqt` | ~180 KB | PDBQT | AutoDock-formatted MSH3 ATPase receptor (PDB 3THW, chain A) |

**Retrieval**:
```bash
gsutil cp gs://aegismind-tpu-results/aegis_flashoptim/phase39_msh3_rdkit/vina_scores.json .
gsutil cp gs://aegismind-tpu-results/aegis_flashoptim/phase39_msh3_rdkit/features.json .
gsutil cp -r gs://aegismind-tpu-results/aegis_flashoptim/phase39_msh3_rdkit/structures.sdf .
```

---

### Phase 40: Nash Equilibrium Synergy Analysis

| File | GCS Path | Size | Format | Description |
|------|----------|------|--------|-------------|
| **nash_synergy_matrix.json** | `phase40_nash_msh3/nash_synergy_matrix.json` | ~850 KB | JSON | 5 MSH3 inhibitors × 6 PARP partners; synergy scores (Nash equilibrium metric) |
| **nash_payoff_tensors.npz** | `phase40_nash_msh3/nash_payoff_tensors.npz` | ~3.2 MB | NPZ | Underlying payoff matrices (fitness values before equilibrium computation) |
| **synergy_top_100.csv** | `phase40_nash_msh3/synergy_top_100.csv` | ~285 KB | CSV | Top 100 synergistic pairs (human-readable) |

**Retrieval**:
```bash
gsutil cp gs://aegismind-tpu-results/aegis_flashoptim/phase40_nash_msh3/nash_synergy_matrix.json .
gsutil cp gs://aegismind-tpu-results/aegis_flashoptim/phase40_nash_msh3/synergy_top_100.csv .
```

---

### Phase 41: Cross-Target Transfer Learning (LMC)

| File | GCS Path | Size | Format | Description |
|------|----------|------|--------|-------------|
| **lmc_results.json** | `phase41_lmc_cross_target/results.json` | ~1.2 MB | JSON | Linear Mode Connectivity curve: KPC-3 ↔ MSH3 (11 interpolation points) |
| **kpc3_surrogate.pt** | `phase41_lmc_cross_target/checkpoints/kpc3_msh3_1895.pt` | ~18 MB | PyTorch | KPC-3 surrogate model (trained on 1,895 compounds) |
| **msh3_surrogate.pt** | `phase41_lmc_cross_target/checkpoints/msh3_1759.pt` | ~16 MB | PyTorch | MSH3 surrogate model (trained on 1,759 compounds) |
| **transfer_analysis.csv** | `phase41_lmc_cross_target/transfer_analysis.csv` | ~445 KB | CSV | Barrier heights, interpolation loss curves, Hessian eigenvalue analysis |

**Retrieval**:
```bash
gsutil cp gs://aegismind-tpu-results/aegis_flashoptim/phase41_lmc_cross_target/results.json .
gsutil cp gs://aegismind-tpu-results/aegis_flashoptim/phase41_lmc_cross_target/checkpoints/*.pt ./checkpoints/
```

---

### Phase 42: Multi-Target Bayesian Optimization

| File | GCS Path | Size | Format | Description |
|------|----------|------|--------|-------------|
| **bo_results.json** | `phase42_multi_target_bo/results.json` | ~2.1 MB | JSON | 30-round BO trajectory; cumulative improvement, selected compounds, acq. function values |
| **bo_history.csv** | `phase42_multi_target_bo/bo_history.csv` | ~650 KB | CSV | Iteration-by-iteration BO trace (compound, predicted pKd, actual pKd, acq. value) |
| **bo_top_candidates.csv** | `phase42_multi_target_bo/bo_top_candidates.csv** | ~120 KB | CSV | Top 10 dual-target (MSH3+KPC-3) candidates with composite scores |

**Retrieval**:
```bash
gsutil cp gs://aegismind-tpu-results/aegis_flashoptim/phase42_multi_target_bo/bo_results.json .
gsutil cp gs://aegismind-tpu-results/aegis_flashoptim/phase42_multi_target_bo/bo_top_candidates.csv .
```

---

## Summary Statistics

| Metric | Value |
|--------|-------|
| **Total compounds screened** | 2,639 (FDA-approved) + 1,759 (lead-like) = **4,398** |
| **Docking scores computed** | 1,759 (finalized on chain A) |
| **Surrogate model training set** | 1,759 compounds |
| **Surrogate Spearman ρ** | 0.854 (docking ↔ Morgan fingerprint MLP concordance) |
| **Nash synergy pairs analyzed** | 5 MSH3 inhibitors × 6 PARP partners = 30 pairs |
| **Synergy threshold** | 0.25 (exceeded by EPTIFIBATIDE + laquinimod) |
| **LMC barrier height (cross-target)** | 0.092 (15.2% of intra-target barrier) |
| **BO iterations (Phase 42)** | 30 rounds on dual-target objective |
| **Total GCS data** | ~104 MB (all phases combined) |

---

## Authentication

To download from GCS, you must have:
1. Google Cloud SDK installed (`gcloud` CLI)
2. Authentication credentials (login with `gcloud auth login`)
3. Read access to the `aegismind-tpu-results` bucket

```bash
gcloud auth login
gsutil ls gs://aegismind-tpu-results/aegis_flashoptim/
```

If you do not have credentials, request access from: **trading.john@gmail.com**

---

## Reproducibility

To fully reproduce this work:
1. Download all GCS files using `gsutil` commands above
2. Install requirements: `pip install -r ../requirements.txt`
3. Run phases in order:
   - `phase38_msh3_retry.py` (requires receptor + compound list)
   - `phase39_msh3_rdkit.py` (requires docking results)
   - `phase40_nash_msh3.py` (requires featurized compounds)
   - `phase42_multi_target_bo.py` (requires surrogate models)

Checkpoints and intermediate results are provided in GCS to enable partial reproduction (e.g., skip Phase 38–39 and jump to Nash analysis).

---

## Notes

- All data is open-access (CC0 / public domain)
- No proprietary restrictions
- GCS bucket will remain available for at least 24 months post-publication
- For long-term archival, consider mirroring to **Zenodo** (see EHDN_SUBMISSION_PACKAGE.md)
