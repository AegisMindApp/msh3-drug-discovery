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
   - `HD_MSH3_preprint_draft.pdf`
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

## Option 2: medRxiv / bioRxiv
**Advantages**: Discipline-specific preprint servers, widely cited  
**Time**: 1–2 days (peer review of submission)

### Steps:
1. Go to https://www.medrxiv.org/ (for medical/biomedical research)
2. Click "Submit"
3. Create account, upload PDF + metadata
4. Wait for acceptance (typically < 24 hrs)
5. Get DOI automatically assigned

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
   % In HD_MSH3_preprint_draft.tex, add near title:
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
**Use Zenodo** — it's the fastest (5 min), free, and gives your work permanent visibility in the open science community. This strengthens your EHDN Seed Fund application by demonstrating open-science commitment.

Once you get your DOI:
- Email john.goodman@solver.press with "DOI: [number]"
- I'll update all files and push to GitHub
