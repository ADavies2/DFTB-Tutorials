# Minimization of COF TpPa-1 with 3ob-3-1 Slater Koster parameter set

The Slater-Koster parameter set used in this tutorial is 3ob-3-1 (Third Order Density Functional Tight-Binding). This parameter set is currently the most accurate available through DFTB+. When using it, be sure to include your atomic Hubbard Derivatives, which can be found at [this link](https://dftb.org/parameters/download/3ob/3ob-3-1-cc). A breakdown of the input and output files is given below. The material modeled in this tutorial is COF TpPa-1. The file POSCAR can be downloaded and visualized with most visualization software. 

## dftb_in.hsd

This is the instructional file. DFTB+ always expects the instructional file to be called dftb_in.hsd, and if it cannot find a file called dftb_in.hsd, it will end with an error. 

- DFTB+ takes three types of input file formats: .vasp, .gen or .xyz. Where .vasp and .gen file types contain the simulation cell parameters, DFTB+ does not read extended .xyz files, so the .xyz files do not contain simulation lattice parameters. If your simulation is not periodic, this is not an issue. However, it is recommended for periodic systems to always use .vasp or .gen input types. This tutorial uses a .vasp input type called POSCAR. 
- In this tutorial, the ion relaxation scheme used is the conjugate gradient method. You will notice in the output that this driver is deprecate with current DFTB+ models, so the developers recommend using their developed GeometryOptimisation driver. 
    - Many of the tags under the ion relaxation block are self explanatory. Descriptions can also be found in the DFTB+ manual. I will draw attention to the use of <code>FixAngles</code> and <code>FixLengths = {No No No}</code>. These tags were used to maintain the AA eclipsed stacking configuration of the TpPa-1 COF. If these tags are removed, the stacking will minimize into an AA slipped configuration. 
- The current method for self-consistent charge optimization is via the DFTB model. There are also extended tight-binding models implemented in DFTB+. An example using xTB-GFN1 is also given in this repository. 
    - Again, many of the tags under this block are self explanatory. Otherwise, the manual can be consulted. However, there are a few useful things to note. 
    - If you are doing calculations with the 3ob-3-1 parameter set, you must include the following tags in your Hamiltonian block: <code>ThirdOrderFull</code>, <code>HCorrection</code> and <code>HubbbardDerivs</code>. The manual explains the options for each of these blocks. 
    - Because this is a two-dimensional material with strong van der Waals forces between the layers, a dispersion correction is also included. This is switched on via the tag <code>Dispersion</code> where the type of dispersion model is selected and the parameter set is indicated. In this example, the parameters are from a Lennard-Jones style model taken from the Universal Force Field (UFF). The manual describes other options available. 
    - The tag <code>ReadInitialCharges = No</code> specifies that this calculation is not starting from an existing minimized charge file, charges.bin. If you have an existing charges.bin file, you can set this tag to <code>Yes</code> to read charges.bin.
    - The current example is for use with the UWyo ARCC MedicineBow HPC. You will need to edit your dftb_in.hsd file at line 32 to specify the path to the Slater-Koster files. 
    - A Gamma-centered 4×4×4 k-point mesh is used in this example. 
    - For metallic systems or from unstable initial geometries, it can sometimes be useful to turn on the <code>Temperature</code> flag under the <code>Filling</code> block in order to smear the electron configuration and ease the optimization constraints. 
- If you have compiled DFTB+ to run in parallel either across MPI or OpenMP, be sure to include the block <code>Parallel</code>. 

## TpPa1-Out.gen and TpPa1-Out.xyz

These are both final structural files produced by DFTB+. They are updated at each step, so if you need to restart a calculation after a time-out, you can use the .gen file to restart from the last minimization step. Again, the .xyz file does not contain the simulation lattice parameters, so the .gen is recommended. There is a built-in DFTB+ tool called gen2cif that can convert your .gen file type to a .cif file type. Alternatively, the Python package ASE can read .gen types and convert to other file types, if something other than a .cif is required. Most visualization software does not read .gen file types, so it is recommended to convert the output for ease. 

## charges.bin and charges.dat

charges.bin is the binary version of the compiled charges while charges.dat is the human-readable data file containg the Mulliken Charge atomic electron populations. This file is generated from the <code>Options</code> block, which can be removed if a .dat file is not desired. If the <code>WriteChargesAsText</code> tag is turned to <code>Yes</code>, a binary file will not be generated. Only the .dat file will be generated. To restart from a .dat file, include <code>ReadChargesAsText = Yes</code> under the <code>Options</code> block. 

## detailed.out

This file contains the primary energetic information from the minimization calculation. Please consult the manual for a description of its contents. 

## minimize-tppa1.log

This file includes all the run-time information of the minimization calculation. The header of this file can also be checked for proper calling of OpenMP and MPI tags. 