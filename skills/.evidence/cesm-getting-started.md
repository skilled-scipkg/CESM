# Evidence: cesm-getting-started

## Primary docs
- `doc/source/quickstart.rst`
- `doc/source/introduction.rst`
- `doc/source/index.rst`

## Primary source entry points
- `skills/cesm-getting-started/references/doc_map.md`
- `tools/statistical_ensemble_test/single_run.py`
- `tools/statistical_ensemble_test/ensemble.py`

## Extracted headings
- (none extracted)

## Executable command hints
- ./query_config --help
- ./create_newcase --case CASENAME --compset COMPSET --res GRID
- ./create_newcase --case /glade/scratch/$USER/cases/b.e20.B1850.f19_g17.test --compset B1850 --res f19_g17
- ./case.setup
- ./case.build
- ./xmlquery EXEROOT
- ./xmlquery STOP_OPTION,STOP_N
- ./xmlchange STOP_OPTION=nmonths,STOP_N=1
- ./xmlchange DOUT_S=FALSE
- ./case.submit
- ./xmlquery RUNDIR,CASE,CASEROOT,DOUT_S,DOUT_S_ROOT

## Warnings and pitfalls
- is a very important piece of metadata that will be used in filenames, internal metadata
- There could be standard out and/or standard error files output from the batch system.
- .. warning:: NetCDF must be built with the same Fortran compiler as CESM. In the netCDF build the FC environment variable specifies which Fortran compiler to use. CESM is written mostly in Fortran, netCDF is written in C. Because there is no standard way to call a C program from a Fortran program, the Fortran to C layer between CESM and netCDF will vary depending on which Fortran compiler you use for CESM. When a function in the netCDF library is called from a Fortran application, the netCDF Fortran API calls the netCDF C library. If you do not use the same compiler to build netCDF and CESM you will in most cases get errors from netCDF saying certain netCDF functions cannot be found.
- .. important::
