# Minimization of MOF UiO-66 with xTB-GFN1 model 

While accurate, the drawback of using the 3ob-3-1 parameter set is that it is only parameterized for a select number of atom types. With COFs, many of these atom types are included. However, if you wish to simulate metals, beyond row 1 alkali or halide ions, or any other atom type, the parameterization for 3ob-3-1 is not included. The extended tight-binding models, GFN1 and GFN2, are accurate alternatives to the Slater-Koster parameterized DFTB model. 

Both GFN1 and GFN2 are included in the the DFTB+ package and can be used to minimize geometries, calculate band structures and density of states, and to simulate molecular dynamics. It is recommended to read the literature for each model before determining which is most accurate for your system. A drawback of using the xTB models is that they can be slower than the parameterized DFTB model. However, these models are still faster than traditional DFT. 

## dftb_in.hsd

- The primary difference between the 3ob-3-1 dftb_in.hsd file and the GFN1-xTB calculation is the Hamiltonian block. In line 13, the Hamiltonian driver has been specified as xTB rather than DFTB. 
    - In line 16, the specific xTB model is defined, either "GFN1-xTB" or "GFN2-xTB". 
- It is noted here that dispersion corrections can still be applied with either of the xTB models. However, in this example, as UiO-66 is a 3D MOF, and for the sake of sped up calculations for the example, the dispersion corrections have been dropped. 

The output files are all the same as the 3ob-3-1 parameter set. 