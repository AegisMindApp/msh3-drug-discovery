# Getting a DOI for the Preprint

The manuscript currently lacks a Digital Object Identifier (DOI). Here are three options:

## Option 1: Zenodo (Recommended)
**Advantages**: Free, permanent, citable, endorses open science  
**Time**: 5 minutes

### Steps:
1. Go to https://zenodo.org/
2. Sign in with GitHub or ORCID
3. Click "New Upload" → "Publish"
4. Upload:
   - `HD_MSH3_preprint.pdf`
   - `Figure1_MSH3_Structure.png`
   - `Figure2_Nash_Heatmap.png`
   - `Figure3_ThreeWayConvergence.png`
   - `Figure4_CrossTarget_LMC.png`

5. Fill metadata:
   - **Title**: Multi-Target Drug Discovery for Huntington's Disease: Convergent Identification of MSH3 ATPase Inhibitors via Virtual Screening and Game-Theoretic Optimization
   - **Authors**: John Goodman
   - **Description**: [Copy abstract from manuscript]
   - **Type**: Preprint
   - **License**: CC-BY-4.0 (Attribution)
   - **Keywords**: Huntington's disease, MSH3, drug discovery, virtual screening, Nash equilibrium

6. Click "Publish" → Get **DOI** (e.g., 10.5281/zenodo.XXXXXXX)

---

## Option 2: arXiv (Computational + Biology Track)
**Advantages**: No review, instant publication, widely recognized in computational science  
**Time**: Immediate (automated processing)
**Note**: Better than medRxiv/bioRxiv for computational + game-theory work

### Steps:
1. Go to https://arxiv.org/
2. Create account
3. Select category: **cs.AI** (machine learning) or **q-bio.CB** (computational biology)
4. Upload PDF + metadata
5. Get arXiv ID + permanent URL within hours (can register DOI separately via Crossref)

**Alternative if you prefer biology-specific servers:**
- **bioRxiv** (https://www.biorxiv.org/) — BUT check their scope first; they may reject computational-only work
- **medRxiv** (https://www.medrxiv.org/) — Clinical medicine focus; likely to reject game-theory papers

---

## Option 3: SSRN
**Advantages**: Fast publication, abstract indexing  
**Time**: Immediate

### Steps:
1. Go to https://ssrn.com/
2. Upload paper → Receive DOI same day

---

## Once You Have a DOI:

1. **Update manuscript**:
   ```latex
   % In HD_MSH3_preprint.tex, add near title:
   DOI: 10.5281/zenodo.XXXXXXX
   ```

2. **Update README.md**:
   ```markdown
   ## Citation
   
   Goodman, J. (2026). Multi-target computational drug discovery identifies 
   FDA-approved MSH3 ATPase inhibitors as candidates for Huntington's disease. 
   Retrieved from https://doi.org/10.5281/zenodo.XXXXXXX
   ```

3. **Update email to Flaviano**:
   Replace `[pending Zenodo submission]` with actual DOI

4. **Regenerate PDF** and push to GitHub

---

## Recommended Action:
**Use Zenodo** — it's the best choice for this work because:
- ✅ Accepts computational + experimental hybrid papers (medRxiv/bioRxiv would likely reject)
- ✅ Fastest (5 minutes)
- ✅ Free with permanent archival
- ✅ High visibility in open science community
- ✅ Strengthens EHDN Seed Fund application

**Why not arXiv?** While arXiv accepts computational work, Zenodo's focus on research reproducibility (data + code) is better aligned with your GitHub repo + GCS data strategy.

Once you get your DOI:
- Email john.goodman@solver.press with "DOI: [number]"
- I'll update all files and push to GitHub
