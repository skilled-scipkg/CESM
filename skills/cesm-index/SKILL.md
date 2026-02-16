---
name: cesm-index
description: This skill should be used when users ask how to use cesm and the correct generated documentation skill must be selected before going deeper into source code.
---

# cesm Skills Index

## Start here
- All paths in these skills are repository-root relative.
- If your current directory is `skills/`, run `cd ..` before executing commands.
- For first-run simulation bootstrap, open `skills/cesm-index/references/simulation_start.md`.

## Route the request
- Classify the request into one generated topic skill below.
- Prefer workflow-level guidance first; inspect function-level code only when docs are insufficient.

## Generated topic skills
- `cesm-getting-started`: First-run setup, case lifecycle, run/validation checkpoints.
- `cesm-inputs-and-modeling`: Externals/input data strategy, compset/grid selection, machine/science configuration.
- `cesm-readme`: Sandbox maintenance (`git-fleximod`), pin management (`.gitmodules`), docs build/publish flow.

## Documentation and behavior references
- Documentation roots: `README.rst`, `doc`, `doc/source`
- Validation/test roots: `cime_config/SystemTests`, `cime_config/testfiles`, `cime_config/testmods_dirs`, `cime_config/testlist_allactive.xml`
- Automation scripts: `tools/statistical_ensemble_test`

## Escalate only when needed
1. Start from the selected topic skill's primary docs.
2. If needed, inspect `skills/<topic>/references/doc_map.md`.
3. If ambiguity remains, inspect `skills/<topic>/references/source_map.md`.
4. Use targeted source search, for example:
   - `rg -n "<symbol_or_keyword>" .lib/git-fleximod bin cime_config tools/statistical_ensemble_test`

## Deeper source directories (after externals bootstrap)
- `cime`
- `components`
- `libraries`
- `share`
