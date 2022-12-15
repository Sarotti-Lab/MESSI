
# MESSI  :atom:

## Multi Ensamble Strategy for Structural identification
<picture>
 <img alt="Show" src="https://user-images.githubusercontent.com/101136961/202787005-8666c08e-7126-46ae-a3d6-5f04068e9bde.jpg" width="450" height="350"/>
</picture>

>This repository contains all codes and data required to run MESSI calculations. 

### Description
>MESSI is a Python program to compute Multi Ensamble DP4+ probabilities in the stereochemical assignament of new organic compounds.


### Installation Requirements

**MESSI.py** needs python 3.8 or later to work. The module can be installed by console using:
`pip3 install messi_nmr`

Usage by console: `messi`

>Installing the python module will automatically generate a `messi.py` shortcut on your desktop, which allows direct execution of the program without the use of a console.
In order to test the correct software operation is recommended to run the provided example, which could be download by clicking the buttom `Create Example`. This will create a folder name `Example_messi_nmr` in desktop containing all the files needed by de use of MESSI. 

>![image](https://user-images.githubusercontent.com/101136961/207873766-486bf7d6-c95e-405b-a70c-72be24fbfd47.png)

### User Guide

**Terms of use.** You need to create a folder containing the following files:

      1) The outputs of the NMR and SCF calculations (all conformers for all isomers).

      2) An excel file containing the experimental data and the labels of each nucleus associated with each experimental value.
       
 **1) The output files:** must be named following the next convention: **`n_*_m*.log`** or **`.out`**, where *n* identifies the *i<sup>th</sup>* isomer, ranging from 1 to *N* where *N* is the number of candidate structures under study, and *m* indicate the conformer number. For instance: 
 
       1_NewNatProd_c01.log (Conformer 1 of isomer 1 of a compound named NewNatProd)

       1_NewNatProd_c02.log (Conformer 2 of isomer 1 of a compound named NewNatProd)

       2_NewNatProd_c01.log (Conformer 1 of isomer 2 of a compound named NewNatProd)
       
       2_NewNatProd_c02.log (Conformer 2 of isomer 2 of a compound named NewNatProd)

>The NMR and SCRF/SMD energies calculation could be in the same or different outputs. If they are separated, both file must begin with the same name (**`n_*_m*`**) and a suffix must be added in order to differentiate the calculation type. If the number of files for NMR calculations does not match the number of SMD energy calculations the script will not run. 

>*The script handles outputs from Gaussian 03, 09 and 16.*

>*Note*: Name files adequately is essential in order to match SMD energy with the NMR data for each conformer.

**2) The input Excel file:** The experimental data and the labels of the candidate structures must be placed in an excel file following the next rules. The excel file should be constituted by one sheet; containing the data of the NMR chemical shifts (*named* ‘shifts’). 

>**“shifts” sheet Structure:** the first column *“nuclei”* contain the identity of the atom ‘c or C’ for <sup>13</sup>C and ‘h or H’ for hydrogen atoms. The second column *“sp2”* serves to indicate **0** (for sp<sup>3</sup> C or H attached to) or **1** (for sp<sup>2</sup> and sp).  The third column *“exp_data”* contains the experimental chemical shifts. The column *“exchange”* serves to indicate by any character experimental data interchangeable (for instance two diatereotopics H must be indicated by an *“a”* in this column, this will cause for each candidate both the experimental and calculated values to be ordered from highest to lowest. The following columns are intended to place the labels of the nuclei associated to the corresponding chemical shift. If two or more values are added in that region, the isotropic shielding values will be averaged (as in the case of methyl groups or equivalent methylene groups). In the cases where isomers have different labels, there should be three columns for each isomer as indicated below.

<picture>
 <img alt="Show" src="https://user-images.githubusercontent.com/101136961/207889663-2fc393f1-6cfe-44e8-a21a-377459b1a176.png" width="800" height="470"/>
</picture>

**3) The output excel file:** once the messi.py is executed, a file named ‘MESSI_Results.xlsx’ is created in the folder containing the Gaussian outputs. The file contains n+1 sheets where n is the number candidates structures:

>**Results sheet:**  this sheet contain the *PCM-DP4+* (row 19, DP4+ standard), *SMD-DP4+* (row 20, DP4+ standard but using SCF energies at the level SMD/B3LYP/6-31+G**), from row 3 to 18 you can find each of the *16 selected ensembles* and in the second row it’s the average probability named ***MESSI***.  These probabilities are the full-DP4+ if both data <sup>1</sup>H and <sup>13</sup>C are available or it can be a partial probability, depending on whether data from H or C is used.

>![image](https://user-images.githubusercontent.com/101136961/207931725-4a38a08b-730b-4648-abe4-ac7f55112123.png)

>**NOTE:** *It is important to point out that filters 4, 11 y 12 remove a fixed energy window of 1 Kcal from minimum, so if any isomer is left without conformations the probability will be 0 for that isomer. However, to notice of this situation, the cells corresponding to the isomer that did not participate in that ensemble will be indicated in gray.*

>**Isomers tensors sheets:** the excel file will contain as many sheets as candidate structures you modeled label as “Tens_Isomer N”, where N is the isomer number. Each sheet contains the weighted isotropic shielding constants according to the used ensemble; each assembly will be represented in a row in the same order as the probability results. As indicate in Figure 3.

![image](https://user-images.githubusercontent.com/101136961/207932075-e29c7a3e-92c9-406f-8e57-62c5e543bae2.png)



