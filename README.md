# HPC4WC Group10 Structured vs. Unstructured

The root repository contains the Fortran files (for different versions of the stencil2d program) and the jupyter notebook files (for validating and plotting experiment results). The data and figures folders contain the raw data of different experiments and the figures on the report respectively. 

Here is the list of Fortran files in the root repository:
* stencil2d-base.F90: The unmodified base version of the stencil2d program in the day2 folder
* stencil2d-sequential.F90: Based on the base version, we modified the code and implemented new functions to make unstructured grid possible. The name sequential refers to the method to map the unstructured grid, where an index for indirect addressing is given to each grid point row-by-row.
* stencil2d-random.F90: The unstructured grid version of the stencil2d program where the indices are shuffled and assigned to the grid points
* stencil2d-hilbert.F90: The unstructured grid version of the stencil2d program where the indices are computed using Hilbert curve and assigned to the grid points
* stencil2d-unstructured_i_out.F90: The unstructured grid version of the sequential stencil2d program where conversion was made column-by-column.
* stencil2d-unstructured_j_out.F90: The unstructured grid version of the sequential stencil2d program where conversion was made row-by-row.
* stencil2d-hilbert_nPoint,4.F90: Based on the stencil2d-hilbert.F90, the dimension of the 2D array neighbor(4, nPoint) is changed to (nPoint, 4)
* stencil2d-random_nPoint,4.F90: Based on the stencil2d-hilbert.F90, the dimension of the 2D array neighbor(4, nPoint) is changed to (nPoint, 4)
* stencil2d-sequential_nPoint,4.F90: Based on the stencil2d-hilbert.F90, the dimension of the 2D array neighbor(4, nPoint) is changed to (nPoint, 4)
* m_utils.F90 and Makefile: Necessary for compiling the stencil2d programs. They are copied from the day2 folder. Slight modification was made in m_utils.F90

The jupyter notebooks are used for compiling fortran programs, analysing and plotting results. Here, we describe the steps and the scripts used for the figures and results in the report: 
* Section 2.4 (Figure 1): This figure (comparison of Hilbert curve in different grid sizes) is generated in the script visualize_hilbert.ipynb.
* Section 3.1 (Result Validation): This is done in the script validate_unstructured.ipynb. Each version of the stencil2d program is compiled and simulated with a specific setting. The results are then plotted and validated. We also subtracted the results each other to ensure they are the same.
* Section 3.2 (Lookup table comparison): TBD
* Section 3.3 (i and j loop in the sequential method): This is done in i_and_j_runtime.ipynb. Each setting was manually run 10 times. The default setting is i loop out, and it can be replaced by j loop out by commenting out the default line and uncommenting line for j loop out. The runtime for each run must be noted, and difference can be investigated using HPC4WC_TimePlot_loop.ipynb.
* Section 3.4 (Comparison of conversion techniques across domain sizes): This is done in runtime_compare.ipynb. Using for loops, we simulated each version of the stencil2d program for various domains sizes. The runtime of all the simulations are saved and then plotted as a scatter plot (Figure 5 in the report). Cache reports for sequential version and Hilbert curve version of the programs are also generated in this script for comparison (Section 3.4.1) 
