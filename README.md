# CZSH_FF pyCSH_Zn paper code package

This package provides a clean paper-code snapshot of the pyCSH_Zn workflow for
constructing, validating, screening, and selected quasi-static deformation
diagnostics of Zn-modified C-S-H atomistic models.

## Supported

- Brick-based C-S-H model construction based on pyCSH logic.
- Q1_Zn and Q2b_Zn motif construction.
- Single-Zn and multi-Zn model generation.
- Composition-targeted target-window generation and screening by requested
  Ca/Si and Zn/Si.
- CementFF4-Zn compatible typing and output.
- LAMMPS read/run0/static minimization workflow.
- Post-min Zn-O coordination diagnostics.
- Ensemble analysis and representative model selection.
- Selected x-direction quasi-static deformation diagnostics.

## Not Supported Or Not Claimed

- No finite-temperature MD.
- No `md_ready_candidate` label.
- No final elastic constants.
- No production mechanical properties.
- Overcoordinated models are minimum-valid, not ideal ZnO4 tetrahedral
  structures.

## Composition-Targeted Screening

v1.12 adds `pyCSH_Zn/examples/19_generate_composition_targeted_zn_csh.py`.
This is a target-window screening interface: it requests Ca/Si and Zn/Si
windows, generates candidates, records actual compositions, and separates the
validation gate from the composition-match gate. It does not guarantee exact
arbitrary final ratios because integer Zn counts, available Q1/Q2b sites,
Zn-Zn compatibility, and validation can constrain the result.

Example:

```bash
python pyCSH_Zn/examples/19_generate_composition_targeted_zn_csh.py --target-ca-si 1.5 --ca-si-tol 0.08 --target-zn-si 0.05 --zn-si-tol 0.03 --site-mode multi_q2b --n-models 5 --seed-start 12000 --output-dir output_composition_targeted
```

For LAMMPS read/run0/static minimization or quasi-static deformation, continue
with the existing `04`, `06`, `07`, or opt-in mechanics workflows. Composition
targeting is construction, validation, and screening only.

## Start Here

- `QUICK_START.md`: minimal command sequence.
- `REPRODUCIBILITY_COMMANDS.md`: lightweight verification commands.
- `pyCSH_Zn/FINAL_WORKFLOW.md`: full workflow reference.
- `pyCSH_Zn/SUPPLEMENTARY_WORKFLOW_TABLES.md`: supplement-ready tables.
- `checks/PAPER_CODE_AUDIT.md`: package audit summary.
