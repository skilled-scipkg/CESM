# cesm source map: Readme

Generated from source roots:
- `.lib/git-fleximod`
- `bin`
- `tools/statistical_ensemble_test`
- `.gitmodules`

Use this map only after exhausting topic docs in `skills/cesm-readme/references/doc_map.md`.

## Topic query tokens
- `git-fleximod`
- `submodule`
- `fxrequired`
- `fxtag`
- `status`
- `update`
- `optional`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" .lib/git-fleximod bin tools/statistical_ensemble_test .gitmodules`
- `rg -n "def |class |async def " .lib/git-fleximod tools/statistical_ensemble_test`

## Suggested source entry points
- `.gitmodules` | authoritative pin set and metadata used by bootstrap/status
- `bin/git-fleximod` | user-facing CLI entrypoint
- `.lib/git-fleximod/git_fleximod/cli.py` | argument parser and root resolution (`get_parser`, `find_root_dir`)
- `.lib/git-fleximod/git_fleximod/gitmodules.py` | `.gitmodules` parsing/filtering (`GitModules.sections`, `GitModules.get`)
- `.lib/git-fleximod/git_fleximod/git_fleximod.py` | command dispatch (`commandline_arguments`), status/update loops (`submodules_status`, `submodules_update`)
- `.lib/git-fleximod/git_fleximod/submodule.py` | per-submodule sync/status logic (`Submodule.status`, `Submodule.update`)
- `.lib/git-fleximod/git_fleximod/gitinterface.py` | git command execution wrapper (`git_operation`, `git_operation_async`)
- `tools/statistical_ensemble_test/single_run.py` | practical case orchestration script for behavior cross-checks
- `tools/statistical_ensemble_test/ensemble.py` | ensemble case automation path for multi-run workflows
