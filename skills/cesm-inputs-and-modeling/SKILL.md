---
name: cesm-inputs-and-modeling
description: This skill should be used when users ask about inputs and modeling in cesm; it prioritizes documentation references and then source inspection only for unresolved details.
---

# cesm: Inputs and Modeling

## High-signal playbook
### Route conditions
- Use this skill for externals bootstrap, input-data strategy, compset/grid selection, and machine/science configuration validity.
- Route to `cesm-getting-started` for step-by-step case lifecycle execution.
- Route to `cesm-readme` for docs build/publish and sandbox maintenance details.

### Triage questions
- Which CESM tag/branch must be reproduced?
- Are externals already materialized (`./bin/git-fleximod status` clean)?
- Which compset alias and grid are scientifically appropriate?
- Is the machine supported, or will `--run-unsupported` and extra validation be required?
- Where is `DIN_LOC_ROOT`, and should case creation pass `--input-dir`?

### Canonical workflow
1. Checkout the target tag/branch and run `./bin/git-fleximod update`.
2. Confirm externals state with `./bin/git-fleximod status`.
3. Choose candidate compset/grid from `cime_config/config_compsets.xml` and `cime_config/testlist_allactive.xml`.
4. Create a case (`create_newcase`) with explicit `--compset`, `--res`, `--mach`; include `--input-dir` as needed.
5. Run `./case.setup`, then `./check_input_data --download` from case directory.
6. Validate configuration and input-data resolution before long integrations.

### Minimal working example
```bash
cd /path/to/cesm
./bin/git-fleximod update
./bin/git-fleximod status

rg -n "<alias>" cime_config/config_compsets.xml | head -20
rg -n "grid=|compset=" cime_config/testlist_allactive.xml | head -20

cd cime/scripts
./create_newcase --case $HOME/cases/<case_name> --compset <compset_alias> --res <grid_alias> --mach <machine> --run-unsupported --input-dir /path/to/inputdata

cd $HOME/cases/<case_name>
./case.setup
./xmlquery DIN_LOC_ROOT
./check_input_data --download
```

### Pitfalls/fixes
- Older docs mention a legacy externals checkout script; this checkout uses `bin/git-fleximod`. Fix: bootstrap with `git-fleximod`.
- Skipping externals status check causes late failures. Fix: run `./bin/git-fleximod status` before case creation.
- Pulling entire input-data repositories is wasteful/risky. Fix: use `check_input_data --download` for case-specific data only.
- Unsupported compset/grid/machine combinations can run but be scientifically invalid. Fix: anchor first runs to combinations seen in `cime_config/testlist_allactive.xml` and validate.

### Convergence/validation checks
- `./bin/git-fleximod status` shows required externals aligned.
- Selected compset alias exists in `cime_config/config_compsets.xml`.
- Selected grid/compset appears in known system-test tuples (`cime_config/testlist_allactive.xml`) when possible.
- `./xmlquery DIN_LOC_ROOT` is correct and `check_input_data --download` completes successfully.

## Scope
- Handle questions about inputs, model configuration, and setup constraints.
- Keep responses practical for real simulation startup and validation.

## Primary documentation references
- `README.rst`
- `doc/source/cesm_configurations.rst`
- `doc/source/downloading_cesm.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `skills/cesm-inputs-and-modeling/references/doc_map.md`.
- If ambiguity remains after docs, inspect `skills/cesm-inputs-and-modeling/references/source_map.md`.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `doc/source`

## Test references
- `cime_config/SystemTests`
- `cime_config/testfiles`
- `cime_config/testmods_dirs`
- `cime_config/testlist_allactive.xml`
- `tools/statistical_ensemble_test`

## Source entry points for unresolved issues
- `.gitmodules` (authoritative externals pin set)
- `bin/git-fleximod` (bootstrap/status entrypoint)
- `.lib/git-fleximod/git_fleximod/cli.py` (`find_root_dir`, `get_parser`)
- `.lib/git-fleximod/git_fleximod/git_fleximod.py` (`commandline_arguments`, `submodules_update`, `submodules_test`)
- `.lib/git-fleximod/git_fleximod/submodule.py` (`Submodule.status`, `Submodule.update`)
- `cime_config/config_compsets.xml` (compset alias/longname mapping)
- `cime_config/config_pes.xml` (machine/grid PE layout defaults)
- `cime_config/config_tests.xml` (CESM-specific test runtime defaults)
- `cime_config/testlist_allactive.xml` (known machine/grid/compset combinations)
- `cime_config/testfiles/ExpectedTestFails.xml` (known expected failure context)
- `tools/statistical_ensemble_test/single_run.py` (`process_args_dict`, `single_case`)
- `tools/statistical_ensemble_test/ensemble.py` (`get_pertlim_uf`, `main`)
