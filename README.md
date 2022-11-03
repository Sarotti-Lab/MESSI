
# MESSI

## Multi Ensamble Strategy for Structural identification

*Graphical Abstract aca*

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

**2) The input Excel file:** The experimental data and the labels of the candidate structures must be provided in an Excel file which must be made as follows. The Excel file contains two sheets; one containing the data for the coupling constants (named ‘J’) and the other with the NMR chemical shifts (named ‘shifts’). A template can be found in the examples provided in the Data section. 


