# CESM Simulation Start (This Checkout)

## 1) Preflight from repository root
```bash
pwd
test -f .gitmodules
test -x bin/git-fleximod
```

## 2) Materialize externals and scripts
```bash
./bin/git-fleximod update
./bin/git-fleximod status
test -x cime/scripts/create_newcase
```

## 3) Pick practical inputs before creating a case
```bash
rg -n "<alias>" cime_config/config_compsets.xml | head -20
rg -n "grid=|compset=" cime_config/testlist_allactive.xml | head -20
```

## 4) Minimal case bring-up commands
```bash
cd cime/scripts
./query_config --help
./create_newcase --case $HOME/cases/<case_name> --compset <compset_alias> --res <grid_alias> --mach <machine> --run-unsupported

cd $HOME/cases/<case_name>
./case.setup
./xmlchange STOP_OPTION=nmonths,STOP_N=1,DOUT_S=FALSE
./case.build
./case.submit
```

## 5) Validation checkpoints
```bash
RUNDIR=$(./xmlquery --value RUNDIR)
./xmlquery RUNDIR,CASE,CASEROOT,DOUT_S,DOUT_S_ROOT
grep -n "SUCCESSFUL TERMINATION OF CPL7-cesm" "$RUNDIR"/cpl.log.*
```

## Notes
- `doc/source/downloading_cesm.rst` contains historical checkout script examples from older CESM layouts.
- In this checkout, use `bin/git-fleximod` + `.gitmodules` for externals bootstrap and status.
