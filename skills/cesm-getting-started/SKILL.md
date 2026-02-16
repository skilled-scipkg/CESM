---
name: cesm-getting-started
description: This skill should be used when users ask about getting started in cesm; it prioritizes documentation references and then source inspection only for unresolved details.
---

# cesm: Getting Started

## High-signal playbook
### Route conditions
- Use this skill for first-run setup, case creation, case lifecycle (`case.setup`, `case.build`, `case.submit`), and run-output validation.
- Route to `cesm-inputs-and-modeling` for compset/grid science choices and input-data policy.
- Route to `cesm-readme` for sandbox maintenance and docs build/publish workflow.

### Bootstrap preflight (this checkout)
1. Run `./bin/git-fleximod update` from repo root.
2. Validate bootstrap with `./bin/git-fleximod status`.
3. Confirm case tools exist: `test -x cime/scripts/create_newcase`.

### Canonical workflow
1. Confirm release/doc version alignment (`README.rst`, `doc/source/index.rst`).
2. Inspect available configurations: `./query_config --help` from `cime/scripts` (`doc/source/quickstart.rst`).
3. Create a case with explicit `--case`, `--compset`, `--res` (and `--mach` / `--project` as required).
4. In case directory, use `xmlchange` for runtime controls; avoid manual XML edits.
5. Run `./case.setup`, `./case.build`, `./case.submit`.
6. Validate run/archives via `xmlquery` and coupler success string in `cpl.log.*`.

### Minimal working example
```bash
cd /path/to/cesm
./bin/git-fleximod update
./bin/git-fleximod status

rg -n "<alias>" cime_config/config_compsets.xml | head -20
rg -n "grid=|compset=" cime_config/testlist_allactive.xml | head -20

cd cime/scripts
./query_config --help
./create_newcase --case $HOME/cases/<case_name> --compset <compset_alias> --res <grid_alias> --mach <machine> --run-unsupported

cd $HOME/cases/<case_name>
./case.setup
./xmlchange STOP_OPTION=nmonths,STOP_N=1,DOUT_S=FALSE
./case.build
./case.submit

RUNDIR=$(./xmlquery --value RUNDIR)
./xmlquery RUNDIR,CASE,CASEROOT,DOUT_S,DOUT_S_ROOT
grep -n "SUCCESSFUL TERMINATION OF CPL7-cesm" "$RUNDIR"/cpl.log.*
```

### Pitfalls/fixes
- Missing `cime/scripts` usually means externals were not materialized. Fix: run `./bin/git-fleximod update`.
- Manual XML edits are fragile. Fix: use `xmlchange` / `xmlquery` only.
- Default short run settings are for smoke tests, not production statistics. Fix: explicitly set `STOP_OPTION` / `STOP_N`.
- Output-location confusion is common. Fix: query `RUNDIR` and `DOUT_S_ROOT` before debugging missing files.

### Convergence/validation checks
- `./bin/git-fleximod status` is clean for required externals.
- `cime/scripts/create_newcase` exists and is executable.
- `./case.setup`, `./case.build`, `./case.submit` all return success.
- Coupler log contains `SUCCESSFUL TERMINATION OF CPL7-cesm`.

## Scope
- Handle questions about initial setup, quickstarts, and core execution lifecycle.
- Keep responses practical and command-oriented for real simulation startup.

## Primary documentation references
- `README.rst`
- `doc/source/quickstart.rst`
- `doc/source/introduction.rst`
- `doc/source/index.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `skills/cesm-getting-started/references/doc_map.md`.
- If ambiguity remains after docs, inspect `skills/cesm-getting-started/references/source_map.md`.
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
- `bin/git-fleximod` (CLI wrapper entrypoint)
- `.lib/git-fleximod/git_fleximod/cli.py` (`find_root_dir`, `get_parser`)
- `.lib/git-fleximod/git_fleximod/git_fleximod.py` (`commandline_arguments`, `submodules_status`, `submodules_update`)
- `.lib/git-fleximod/git_fleximod/submodule.py` (`Submodule.status`, `Submodule.update`)
- `tools/statistical_ensemble_test/single_run.py` (`process_args_dict`, `single_case`)
- `tools/statistical_ensemble_test/ensemble.py` (`get_pertlim_uf`, `main`)
- `cime_config/config_tests.xml` (CESM-specific system-test defaults)
- `cime_config/SystemTests/funitshare.py` (`FUNITSHARE.get_test_spec_dir`, `FUNITSHARE.get_extra_run_tests_args`)
- `.gitmodules` (externals pinning and required/optional policy)
