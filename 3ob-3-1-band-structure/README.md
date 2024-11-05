# Band structure calculation from minimized 3ob-3-1 COF TpPa-1

This band structure calculation will begin from a well-minimized TpPa-1 geometry and charge distribution. That means that the .gen output file and the charges.bin file produced from 3ob-3-1-minimization will be used as inputs to this calculation. 

## dftb_in.hsd

- The <code>Driver</code> block has been removed from this calculation as we do not wish to conduct an ionic relaxation, only a charge minimization along the path of high symmetry within the Brillouin zone. The path of high symmetry here was selected from the P6/mmm scace group from the [Bilbao Crystallographic Server](https://www.cryst.ehu.es/cryst/get_kvec.html). 
- Under the <code>Hamiltonian</code> block, a few tags have changed/been added:
    - <code>ConvergentSCCOnly = Yes</code> ensures that your calculation doesn't "fail" as we are only doing 1 SCC iteration (<code>MaxSCCIterations = 1</code>) since we do not want to recalculate the charge distribution. Related to this, when you look in the .log file, it will appear as if the inital charge distribution is not well-converged as the SCC iteration says it has failed. However, this is because the charges file is being read from a 4×4×4 Gamma-center k-point mesh and is being used to calculate the charge distribution along the path of high symmetry. The output system and input system are different, so the initial charges won't "converge" properly for this system in one SCC iteration.
    - <code>KpointsAndWeights</code> has now changed to <code>KPointsAndWeights [relative] = Klines</code> to specify the path of high symmetry. Consult the manual for a description of the format entered in this block. The path used here is from GAMMA - K - M - GAMMA - A, which samples the x- and y-plane, returns to GAMMA, and samples the z-axis.

## band.out and bands_tot.dat

This file contains the band energies for each k-point specified. If you wish to plot the band structure, this file requires some post-editing in order to be plottable. DFTB+ includes a tool called <code>dp_dos</code> that will convert the band.out file into a plottable data file. This can be executed with the following command: <code>dp_dos -B band.out bands</code> which generates the file bands_tot.dat. For more information on this tool, consult the manual or the DFTB+ tutorials.