# cesm source map: Inputs and Modeling

Generated from source roots:
- `.lib/git-fleximod`
- `bin`
- `cime_config`
- `tools/statistical_ensemble_test`
- `.gitmodules`

Use this map only after exhausting topic docs in `skills/cesm-inputs-and-modeling/references/doc_map.md`.

## Topic query tokens
- `git-fleximod`
- `fxrequired`
- `fxtag`
- `compset`
- `grid`
- `DIN_LOC_ROOT`
- `check_input_data`
- `config_pes`
- `config_tests`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" .lib/git-fleximod bin cime_config tools/statistical_ensemble_test`
- `rg -n "def |class |<test |<compset|<grid" .lib/git-fleximod cime_config tools/statistical_ensemble_test`

## Suggested source entry points
- `.gitmodules` | component pin set + required/optional flags used by bootstrap
- `bin/git-fleximod` | CLI wrapper for update/status/test operations
- `.lib/git-fleximod/git_fleximod/cli.py` | parser behavior (`get_parser`) and root discovery (`find_root_dir`)
- `.lib/git-fleximod/git_fleximod/git_fleximod.py` | update/status/test flow (`commandline_arguments`, `submodules_update`, `submodules_test`)
- `.lib/git-fleximod/git_fleximod/submodule.py` | per-component status/update behavior
- `cime_config/config_compsets.xml` | compset alias-to-longname definitions
- `cime_config/config_pes.xml` | PE/task/thread defaults by grid/compset/machine
- `cime_config/config_tests.xml` | CESM-specific test defaults
- `cime_config/testlist_allactive.xml` | tested tuples for practical first-run choices
- `cime_config/testfiles/ExpectedTestFails.xml` | expected-failure context for verification triage
- `tools/statistical_ensemble_test/single_run.py` | case setup + input/runtime tuning automation
- `tools/statistical_ensemble_test/ensemble.py` | clone/perturbation workflow for ensemble validation

## Post-bootstrap command wrappers (expected after `./bin/git-fleximod update`)
- `cime/scripts/create_newcase`
- `cime/scripts/query_config`
- `cime/scripts/create_clone`
