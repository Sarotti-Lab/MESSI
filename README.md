
# MESSI  :atom:

## Multi Ensamble Strategy for Structural identification

![GRAPH_abstract2](https://user-images.githubusercontent.com/101136961/202787005-8666c08e-7126-46ae-a3d6-5f04068e9bde.jpg)

This repository contains all codes and data required to run MESSI calculations. 

### Description
MESSI is a Python program to compute Multi Ensamble DP4+ probabilities in the stereochemical assignament

### Installation Requirements

**MESSI.py** needs python 3.8 or later to work. The module can be installed by console using:
`pip3 install messi`

Usage: `messi`

### User Guide

To run MESSI it is required that the information is located in a folder containing the following files: 

      1. All the Gaussian outputs from the NMR and SCF energie calculations (all conformers for all isomers). 
      
      2. An Excel file containing the experimental data and the labels of each nucleus associated with each experimental value.
       
 **1) The output files:** must be named following this convention: number_*.log or .out, where number identifies the i<sup>th</sup> isomer, ranging from 1 to N (where N is the number of candidate isomers under study). For example: 
 
       1_NewNatProd_c01.log (Conformer 1 of isomer 1 of a compound named NewNatProd)

       1_NewNatProd_c02.log (Conformer 2 of isomer 1 of a compound named NewNatProd)

       2_NewNatProd_c01.log (Conformer 1 of isomer 2 of a compound named NewNatProd)
       
       2_NewNatProd_c02.log (Conformer 2 of isomer 2 of a compound named NewNatProd)

*The script handles outputs from Gaussian 03, 09 and 16.*

**2) The input Excel file:** The experimental data and the labels of the candidate structures must be provided in an Excel file which must be made as follows. The Excel file contains one sheet (named ‘shifts’) containing the data with the NMR chemical shifts and labeling. A template can be found in the examples provided in the Data section. 

**“shifts” sheet Structure:** the first column *“nuclei”* contains the identity of the atom ‘c or C’ for <sup>13</sup>C and ‘h or H’ for hydrogen atoms. The second column *“sp2”* contains the hibridization information as 0 (for sp3 nulei) or 1 (for sp/sp2 nuclei).  The third column *“exp_data”* contains the experimental chemical shifts, in case of interchangeable values, they should be indicated in the next column *“exchange”* by assigning the interchangable signals with the same character, for instance **a, b, c, etc**. The following columns are intended to place the labels of the nuclei associated to the corresponding chemical shift. If 2 or more values are added in the same row, the isotropic shielding values will be averaged (as in the case of methyl groups or equivalent methylene groups). If the isomers under study have different labeling schemes (as in the case of constitutional isomers), three colums for each isomer should be provied as indicated below.

**3) The output Excel file:** once the MESSI.py is executed, a filed named *‘Results_ML_J_DP4.xlsx’* is created in the same folder containing the Gaussian output files and the Excel input file. The Excel output file contains five sheets: 


**DP4 sheet:**  the DP4 probabilities are shown for each isomer considering the information of H, C and J individually, and altogether. Although the high accuracy in the ML predictions, it must be emphasized that some environments might not be correctly reproduced leading to large unscaled errors that would affect the scaling procedure and the concomitant J-DP4 values. Hence, to avoid potential misassignments, the following sheets contain information regrding the scaled and unscaled chemical shifts, and the corresponding errors (differences with the experimental values). In case all isomers display alarmingly high errors for a given nucleous, it would be advisable to re-compute J-DP4 after removing or revising the conflicting signal. 

**tensors sheet:** this sheet is labeled as *“Shifts_Unsc”*, and displays the experimental chemical shifts (<sup>13</sup>C and <sup>1</sup>H) and the coupling constants (<sup>3</sup>J), in that order, along with the predicted Boltzmann-averaged unscaled values computed for each isomer.
