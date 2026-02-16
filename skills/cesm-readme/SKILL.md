---
name: cesm-readme
description: This skill should be used when users ask about readme in cesm; it prioritizes documentation references and then source inspection only for unresolved details.
---

# cesm: Readme

## High-signal playbook
### Route conditions
- Use this skill for repository-level sandbox bootstrap/maintenance (`git-fleximod`), `.gitmodules` pin updates, and documentation build/publish workflow.
- Route to `cesm-getting-started` for case setup/build/submit lifecycle.
- Route to `cesm-inputs-and-modeling` for compset/grid/input-data strategy and scientific configuration validity.

### Canonical workflow
1. Clone CESM and checkout target tag/branch (`README.rst`).
2. Run `./bin/git-fleximod update`; rerun whenever `.gitmodules` changes (`README.rst`).
3. Verify externals state with `./bin/git-fleximod status`.
4. For component pin changes, edit `.gitmodules`, run `./bin/git-fleximod update <component>`, then commit `.gitmodules` and updated component pointer.
5. For docs publishing, follow `doc/README.md` and run `build_docs -d -c -r <gh-pages-path> -v <version>` from `doc/`.

### Minimal working example
```bash
cd /path/to/cesm
git checkout <tag_or_branch>
./bin/git-fleximod update
./bin/git-fleximod status
./bin/git-fleximod --help

# example component retarget
./bin/git-fleximod update cam

# docs build (from repo doc/ directory)
cd doc
build_docs -d -c -r /PATH/TO/cesm-gh-pages -v <version>
```

### Pitfalls/fixes
- Skipping `git-fleximod update` after tag/branch change leaves externals stale. Fix: rerun update after every `.gitmodules`-affecting change.
- Manual submodule drift without `.gitmodules` updates breaks reproducibility. Fix: commit pin metadata and component pointer changes together.
- Docs build can target wrong output/version. Fix: validate `-r` and `-v` arguments before publish.

### Convergence/validation checks
- `./bin/git-fleximod status` is clean for required externals.
- `.gitmodules` changes are committed with matching component pointer updates.
- Docs build output lands in expected `gh-pages` tree before commit/push.

## Scope
- Handle questions about top-level repository operations and README-level workflows.
- Keep responses concise and operational.

## Primary documentation references
- `README.rst`
- `doc/README.md`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `skills/cesm-readme/references/doc_map.md`.
- If ambiguity remains after docs, inspect `skills/cesm-readme/references/source_map.md`.
- Cite exact documentation file paths in responses.

## Test references
- `cime_config/SystemTests`
- `cime_config/testfiles`
- `cime_config/testmods_dirs`
- `tools/statistical_ensemble_test`

## Source entry points for unresolved issues
- `.gitmodules` (pin metadata and required/optional policy)
- `bin/git-fleximod` (CLI wrapper)
- `.lib/git-fleximod/git_fleximod/cli.py` (`get_parser`, `find_root_dir`)
- `.lib/git-fleximod/git_fleximod/gitmodules.py` (`GitModules.sections`, `GitModules.get`, `GitModules.save`)
- `.lib/git-fleximod/git_fleximod/git_fleximod.py` (`commandline_arguments`, `submodules_status`, `submodules_update`)
- `.lib/git-fleximod/git_fleximod/submodule.py` (`Submodule.status`, `Submodule.update`)
- `tools/statistical_ensemble_test/single_run.py` (scripted case lifecycle reference)
- `tools/statistical_ensemble_test/ensemble.py` (multi-case/ensemble orchestration)
