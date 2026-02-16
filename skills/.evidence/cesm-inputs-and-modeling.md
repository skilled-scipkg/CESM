# Evidence: cesm-inputs-and-modeling

## Primary docs
- `doc/source/cesm_configurations.rst`
- `doc/source/downloading_cesm.rst`

## Primary source entry points
- `skills/cesm-inputs-and-modeling/references/doc_map.md`
- `tools/statistical_ensemble_test/single_run.py`
- `tools/statistical_ensemble_test/ensemble.py`

## Extracted headings
- (none extracted)

## Executable command hints
- ./manage_externals/checkout_externals
- ./manage_externals/checkout_externals --help
- ./manage_externals/checkout_externals -S
- ./cime
- ./components/cam
- ./components/cam/chem_proc
- ./components/cam/src/atmos_phys
- ./components/cam/src/dynamics/fv3/atmos_cubed_sphere
- ./components/cam/src/physics/carma/base
- ./components/cam/src/physics/clubb
- ./components/cam/src/physics/cosp2/src
- ./components/cam/src/physics/pumas

## Warnings and pitfalls
- "ocean", "ocn", "docn", "data", "The `data ocean <http://esmci.github.io/cime/versions/master/html/data_models/data-ocean.html>`_ component has two distinct modes of operation. It can run as a pure data model, reading ocean SSTs (normally climatological) from input datasets, interpolating in space and time, and then passing these to the coupler. Alternatively, docn can compute updated SSTs based on a slab ocean model where bottom ocean heat flux convergence and boundary layer depths are read in and used with the atmosphere/ocean and ice/ocean fluxes obtained from the coupler."
- .. warning:: When contacting the Subversion server for the first time, you may need to
- .. warning:: If a problem was encountered during checkout_externals, which may happen with an older version of the svn client software, it may appear to have downloaded successfully, but in fact only a partial checkout has occurred.
- .. warning:: The input data repository contains datasets for many configurations and resolutions and is well over 10 TByte in total size. DO NOT try to download the entire dataset.
- .. warning:: Again, users are **STRONGLY DISCOURAGED** from downloading the entire input dataset from the repository.
