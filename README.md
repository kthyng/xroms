# `xroms`
[![DOI](https://zenodo.org/badge/265067025.svg)](https://zenodo.org/badge/latestdoi/265067025)

[![Build Status](https://img.shields.io/github/workflow/status/xoceanmodel/xroms/Tests?logo=github&style=for-the-badge)](https://github.com/xoceanmodel/xroms/actions)
[![Code Coverage](https://img.shields.io/codecov/c/github/xoceanmodel/xroms.svg?style=for-the-badge)](https://codecov.io/gh/xoceanmodel/xroms)
[![License:MIT](https://img.shields.io/badge/License-MIT-green.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)
[![Documentation Status](https://img.shields.io/readthedocs/xroms/latest.svg?style=for-the-badge)](https://xroms.readthedocs.io/en/latest/?badge=latest)
[![Code Style Status](https://img.shields.io/github/workflow/status/xoceanmodel/xroms/linting%20with%20pre-commit?label=Code%20Style&style=for-the-badge)](https://github.com/xoceanmodel/xroms/actions)
[![Conda Version](https://img.shields.io/conda/vn/conda-forge/xroms.svg?style=for-the-badge)](https://anaconda.org/conda-forge/xroms)
[![Python Package Index](https://img.shields.io/pypi/v/xroms.svg?style=for-the-badge)](https://pypi.org/project/xroms)


`xroms` contains functions for commonly used scripts for working with ROMS output in xarray.

There are functions to...
* help read in model output with automatically-calculated z coordinates
* calculate many derived variables with correct grid metrics in one line including:
  * horizontal speed
  * kinetic energy
  * eddy kinetic energy
  * vertical shear
  * vertical vorticity
  * Ertel potential vorticity
  * density as calculated in ROMS
  * potential density
  * buoyancy
  * $N^2$ (buoyancy frequency/vertical buoyancy gradient)
  * $M^2$ (horizontal buoyancy gradient)
* useful functions including:
  * derivatives in all dimensions, accounting for curvilinear grids and sigma layers
  * grid metrics (i.e., grid lengths, areas, and volumes)
  * subset horizontal grid such that the staggered grids are consistent
  * easily change horizontal and vertical grids using `xgcm` grid objects
  * easily reorder to dimensional convention
  * slice along a fixed value
  * wrapper for interpolation in longitude/latitude and for fixed depths
  * mixed-layer depth
* Demonstrations:
  * selecting data in many different ways
  * interpolation
  * changing time sampling
  * calculating climatologies
  * various calculations
* provide/track attributes and coordinates through functions
  * wraps [`cf-xarray`](https://cf-xarray.readthedocs.io/en/latest/) to generalize coordinate and dimension calling.
* ability to automatically choose colormaps for plotting with `xarray`
  * wraps `xcmocean` for this


## Installation

You need to have `conda` installed for these installation instructions. You'll have best results if you use the channel `conda-forge`, which you can prioritize with `conda config --add channels conda-forge --force`.

### Create environment if needed

As a first step, you can create an environment for this package with conda if you want. If you do this, you'll need to git clone the package first as below.

    conda create --name XROMS python=3.8 --file requirements.txt

### Install `xroms`

You can choose to install with conda the optional dependencies for full functionality:

    conda install --file requirements-opt.txt

and to install optional dependency `xcmocean`:

    pip install git+https://github.com/pangeo-data/xcmocean

Then choose one of the following to install `xroms` from GitHub:

1. Clone `xroms` into a particular directory then install so that it is editable (`-e`)

    ```
    git clone https://github.com/xoceanmodel/xroms.git
    cd xroms
    pip install -e .
    ```

1. Directly install `xroms` from github

    ```
    pip install git+https://github.com/xoceanmodel/xroms
    ```

### Optional additional installation for horizontal interpolation

If you want to be able to horizontally interpolate with `xroms.interpll`, you should install xESMF. This is currently the only way that has worked.

1. Install `ESMF` with mpi support.

    For Mac:

    ```
    conda install esmf=8.0.1=mpi_openmpi_ha78a60a_0
    ```

    For Linux:

    ```
    conda install esmf=8.0.1=mpi_openmpi_hda7c4e6_0
    ```

1. Install esmpy

    ```
    conda install esmpy=8.0.1=mpi_openmpi_py38h51f2404_0
    ```

1. Install xESMF from github (pip version will not work)

    ```
    pip install git+https://github.com/pangeo-data/xESMF.git#egg=xESMF
    ```

### Recommended: Jupyter Lab extensions

If you are using Jupyter Lab, the Table of Contents and Dask extensions are really helpful:

```
jupyter labextension install @jupyterlab/toc
jupyter labextension install dask-labextension
jupyter serverextension enable dask_labextension
```

Notes:
* Additionally installing [bottleneck](https://github.com/pydata/bottleneck/) is supposed to improve the speed of `numpy`-based calculations.
* Installing so that package is editable is not required but is convenient. You can remove the `-e` from any installation line to not do that.


## Quick Start

After installation, read in model output with one of three load methods:
 * `xroms.open_netcdf(filename)`: if model output is in a single netcdf file or at a single thredds address;
 * `xroms.open_mfnetcdf(filenames)`: if model output is available in multiple accessible local netcdf files;
 * `xroms.open_zarr(locations)`: if model output is available in multiple accessible zarr directories.
More information about reading in model output is available in Jupyter notebook `examples/io.pynb`.

Other common tasks to do with model output using `xroms` as well as other packages are demonstrated in additional Jupyter notebooks:
 * select_data
 * calc
 * interpolation
 * plotting
