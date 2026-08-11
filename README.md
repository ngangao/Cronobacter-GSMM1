# Cronobacter-GSMM
Genome-scale metabolic model of Cronobacter sakazakii 
# iMN1443 — A Genome-Scale Metabolic Model of *Cronobacter sakazakii* ATCC BAA-894

This repository contains the curated genome-scale metabolic model (GEM) of
*Cronobacter sakazakii* ATCC BAA-894.

## Model summary

| | |
|---|---|
| Organism | *Cronobacter sakazakii* ATCC BAA-894 |
| Reactions | 2,902 |
| Metabolites | 1,849 |
| Genes | 1,443 |
| GPR coverage | 73.2% |
| Format | SBML Level 3, FBC v2 |
| Reconstruction tool | CarveMe, followed by manual curation |

## Curation history

The initial draft reconstruction (CarveMe + gap-filling) contained several
structural issues identified through flux variability analysis (FVA) and
corrected in two rounds of manual curation. 

**Round 1**
- Trace-metal and select ion exchange bounds (cobalt, copper, manganese,
  molybdate, zinc, sodium, phosphate), initially unconstrained at 1000 mM
  uptake capacity, were revised to physiologically realistic values.
- `PFK` and `PYK`, both canonically irreversible in vivo, were found
  unconstrained in the reverse direction and fixed to forward-only.
- `F6PA` (fructose-6-phosphate aldolase), found to provide a
  thermodynamically free bypass around canonical PFK/FBA-mediated
  glycolysis despite carrying gene support, was constrained to zero flux
  for simulation purposes (not deleted).

**Round 2**
- `MDH2`, `MDH3`, `FRD2`, `FRD3` — menaquinone-linked isozymes running in
  parallel with their ubiquinone-linked counterparts (`MDH`, `SUCDi`)
  under aerobic simulation — were blocked, removing a thermodynamically
  free loop.

Each fix was verified to leave the FBA-optimal growth rate unchanged,
confirming these were structural/thermodynamic corrections rather than
changes to the model's predicted growth phenotype.

### Known, unresolved limitation

Flux variability analysis shows that `MDH`, `FUM`, and `FBA` (aldolase)
individually remain non-uniquely determined at the optimal growth rate
even after curation — i.e., a wide range of flux values through these
three reactions is equally optimal. This appears to be a separate loop
from the one addressed in Round 2 and has not yet been isolated or fixed.
**Flux values for these three reactions should be interpreted
qualitatively (pathway active, direction X) rather than as precise
point estimates**, and this limitation is explicitly acknowledged. Contributions toward resolving
this are welcome.
