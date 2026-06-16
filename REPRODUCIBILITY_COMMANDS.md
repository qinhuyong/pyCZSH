# Reproducibility Commands

Run from this package root.

```bash
python -m py_compile pyCSH_Zn/examples/17_generate_multi_zn_ensemble.py pyCSH_Zn/examples/18_run_selected_multi_zn_mechanics.py pyCSH_Zn/examples/19_generate_composition_targeted_zn_csh.py
python pyCSH_Zn/examples/01_generate_pure_csh.py
python pyCSH_Zn/examples/02_generate_q2b_zn.py
python pyCSH_Zn/examples/08_generate_q1_zn.py
python pyCSH_Zn/examples/04_build_lammps_inputs.py
python pyCSH_Zn/examples/06_run_static_relaxation.py
python pyCSH_Zn/examples/07_run_quasistatic_mechanics.py
```

Composition-targeted smoke checks:

```bash
python pyCSH_Zn/examples/19_generate_composition_targeted_zn_csh.py --target-ca-si 1.7 --ca-si-tol 0.15 --target-zn-si 0.03 --zn-si-tol 0.05 --site-mode q2b_only --n-models 2 --seed-start 13000 --output-dir output_composition_targeted_smoke
python pyCSH_Zn/examples/19_generate_composition_targeted_zn_csh.py --target-ca-si 1.7 --ca-si-tol 0.15 --target-zn-si 0.06 --zn-si-tol 0.06 --site-mode multi_q2b --n-models 2 --seed-start 14000 --output-dir output_composition_targeted_multi_smoke
```

Each smoke output should include `composition_target_manifest.json`,
`composition_target_summary.csv`, and `composition_target_summary.json`. The CSV
contains requested and actual Ca/Si and Zn/Si values, `composition_match`,
`validation_label`, `coordination_quality`, and `failure_reason`.

Overcoordinated composition-targeted candidates are included by default as
minimum-valid candidates. `--ideal-only` restricts accepted candidates to
`ideal_fourfold`. `--include-overcoordinated` is a retained compatibility flag
and does not change default acceptance behavior.

In a clean package checkout, `examples/07_run_quasistatic_mechanics.py` needs
the post-minimized pure C-S-H and Q2b_Zn references produced by
`04_build_lammps_inputs.py` and `06_run_static_relaxation.py`.

After running `examples/07_run_quasistatic_mechanics.py`, inspect:

```text
pyCSH_Zn/output_Y/workflow_v1/quasistatic_mechanics/mechanics_summary.json
```

The actual target list should be:

```text
pure_csh
q2b_zn
```

Q1_Zn mechanics and multi-Zn mechanics are opt-in workflows and should not
appear in the default `07` target list.

Composition-targeted generation is target-window screening. It does not change
force-field parameters, validation semantics, finite-temperature MD support, or
production mechanical-property claims.
