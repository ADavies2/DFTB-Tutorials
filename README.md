# Tutorials for DFTB+ 

This repository contains tutorials for running various calculations with the software package DFTB+. If publishing your work, please cite the developers of DFTB+ and any associated Slater-Koster parameter sets. 

The tutorials included in this repository are:
- Geometry optimization of COF TpPa-1 using the 3ob-3-1 parameter set
- Band structure calculation of COF TpPa-1 with the 3ob-3-1 parameter set
- Density of state (DOS) calculation of COF TpPa-1 with the 3ob-3-1 parameter set
- Geometry optimization of MOF UiO-66 using the extended tight-binding model GFN1-xTB
- Molecular dynamics simulation under NPT ensemble of stacked COF TpPa-1

An accompanying README.md is included in each of the tutorial sub-directories. [Similar tutorials are availble by the DFTB+ developers](https://dftbplus-recipes.readthedocs.io/en/latest/). The DFTB+ manual can also be found [here](https://dftbplus.org/documentation.html).

## Installation

1. Load the module for or install Conda/MiniConda
2. <code>conda create dftbplus</code>
3. <code>conda activate dftbplus</code>
4. <code>conda install mamba</code>
5. <code>mamba install 'dftbplus=\*=mpi_openmpi_\*'</code>
6. <code>mamba install dftbplus-tools dftbplus-python</code>
7. <code>conda deactivate</code>