# cesm source map: Getting Started

Generated from source roots:
- `.lib/git-fleximod`
- `bin`
- `cime_config`
- `tools/statistical_ensemble_test`
- `.gitmodules`

Use this map only after exhausting topic docs in `skills/cesm-getting-started/references/doc_map.md`.

## Topic query tokens
- `git-fleximod`
- `create_newcase`
- `query_config`
- `xmlchange`
- `xmlquery`
- `case.setup`
- `case.build`
- `case.submit`
- `STOP_OPTION`
- `DOUT_S`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" .lib/git-fleximod bin cime_config tools/statistical_ensemble_test`
- `rg -n "def |class |async def " .lib/git-fleximod tools/statistical_ensemble_test`

## Suggested source entry points
- `bin/git-fleximod` | thin CLI handoff into Python implementation
- `.lib/git-fleximod/git_fleximod/cli.py` | parser behavior: `find_root_dir`, `get_parser`
- `.lib/git-fleximod/git_fleximod/git_fleximod.py` | action flow: `commandline_arguments`, `submodules_status`, `submodules_update`
- `.lib/git-fleximod/git_fleximod/submodule.py` | checkout/status behavior: `Submodule.status`, `Submodule.update`
- `tools/statistical_ensemble_test/single_run.py` | lifecycle orchestration: `process_args_dict`, `single_case`
- `tools/statistical_ensemble_test/ensemble.py` | ensemble orchestration: `get_pertlim_uf`, `main`
- `cime_config/config_tests.xml` | CESM-specific runtime defaults for system tests
- `cime_config/SystemTests/funitshare.py` | CESM SystemTest subclass behavior
- `.gitmodules` | authoritative externals pins and required/optional metadata

## Post-bootstrap command wrappers (expected after `./bin/git-fleximod update`)
- `cime/scripts/query_config`
- `cime/scripts/create_newcase`
- `cime/scripts/create_clone`
