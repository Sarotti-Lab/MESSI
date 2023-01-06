
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

MESSI needs `tkinter` module to work. It will be automatically installed by pip in Windows and macOS, but for linux it must be installed separately by `apt-get`.

>The program can be executed by console using: `messi`

>or generate a `messi.py` shortcut on the desktop, which allows direct execution of the program without the use of a console, using: `messi_exe`
>
In order to test the correct software operation is recommended to run the provided example, which could be download by clicking the buttom `Create Example`. This will create a folder name `Example_messi_nmr` in desktop containing all the files needed by de use of MESSI. 

>> <picture>
 <img alt="Show" src="https://user-images.githubusercontent.com/101136961/210242460-2b028889-9d12-41f9-8323-c672cf0d092c.png" width="704" height="300"/>
</picture>

### User Guide

**Terms of use.** To run MESSI is required that the information is located in a folder containing the following
files:

      1) The Gaussian output files of the NMR and SCRF/SMD calculations (all conformers for all isomers).

      2) An excel file containing the experimental data and the labels of each nucleus associated with each experimental value.
       
 **1) The output files:** must be named following the next convention: **`n_*_m*.log`** or **`.out`**, where *n* identifies the *i<sup>th</sup>* isomer, ranging from 1 to *N* where *N* is the number of candidate structures under study, and *m* indicate the conformer number. For instance: 
 
       1_NewNatProd_c01.log (Conformer 1 of isomer 1 of a compound named NewNatProd)

       1_NewNatProd_c02.log (Conformer 2 of isomer 1 of a compound named NewNatProd)

       2_NewNatProd_c01.log (Conformer 1 of isomer 2 of a compound named NewNatProd)
       
       2_NewNatProd_c02.log (Conformer 2 of isomer 2 of a compound named NewNatProd)

>The NMR and SCRF/SMD energies calculation could be in the same or different outputs. If they are separated, both file must begin with the same name (**`n_*_m*`**) and a suffix must be added in order to differentiate the calculation type. If the number of files for NMR calculations does not match the number of SMD energy calculations the script will not run. 

>*The script handles outputs from Gaussian 09 and 16.*

>*Note*: Name files adequately is essential in order to match SMD energy with the NMR data for each conformer.

**2) The input Excel file:** The experimental data and the labels of the candidate structures must be placed in an excel file following the next rules. The excel file should be constituted by one sheet; containing the data of the NMR chemical shifts (*named* ‘shifts’). 

>**“shifts” sheet Structure:** the first column *“nuclei”* contain the identity of the atom ‘c or C’ for <sup>13</sup>C and ‘h or H’ for hydrogen atoms. The second column *“sp2”* serves to indicate **0** (for sp<sup>3</sup> C or H attached to) or **1** (for sp<sup>2</sup> and sp).  The third column *“exp_data”* contains the experimental chemical shifts. The column *“exchange”* allows to indicate interchangeable signals (for example, two diastereotopic hydrogens). Any character can be used to indicate a pair of interchangeable signals, which will cause that the experimental and calculated values to be ordered upside-down. When dealing with more than one pair of interchangeable signals, different characters should be used to differentiate them. For example, it can be used the letter “a to indicate one pair, and the letter “b” to indicate the other pair. The following columns are intended to place the labels of the nuclei associated to the corresponding chemical shift. If two or more values are added in that region, the isotropic shielding values will be averaged (as in the case of methyl groups or equivalent methylene groups). If the isomers under study have different labeling schemes (as in the case of constitutional isomers), three columns for each isomer should be provided as indicated below.

<picture>
 <img alt="Show" src="https://user-images.githubusercontent.com/101136961/210243637-0c7bf77d-968d-4b46-8d75-2337e3a34837.png" width="800" height="470"/>
</picture>

**3) The output excel file:** once the messi.py is executed, a file named *‘MESSI_Results.xlsx’* is created in the folder containing the Gaussian outputs. The file contains *n*+1 sheets where *n* is the number candidates structures:

>**Results sheet:**  contain the *PCM-DP4+* (row 19, standard DP4+), *SMD-DP4+* (row 20, standard DP4+ using the energies computed at the SMD/B3LYP/6-31+G** level), and the DP4+ results computed for the selected 16 ensembles (rows 3-18). The averaged values of those 16 calculations (***MESSI***.) are shown in row 2. If both <sup>1</sup>H and <sup>13</sup>C are used, the probabilities shown correspond to the full DP4+ results. In case only <sup>1</sup>H, or <sup>13</sup>C, data are used (not recommended), the probabilities shown correspond to H-DP4+ or C-DP4+ values, respectively.

><picture>
 <img alt="Show" src="https://user-images.githubusercontent.com/101136961/207931725-4a38a08b-730b-4648-abe4-ac7f55112123.png" width="800" height="470"/>
</picture>

>**NOTE:** *It is important to point out that ensembles 4, 11 y 12 are created by removing all conformations within 1 kcal/mol from the corresponding global minimum. In some systems with flat potential energy surface, the full conformational space could be confined within that energy window. This will cause all the conformations of that isomer to be eliminated, and therefore its probability will be zero. To indicate that situation, the corresponding cells will be highlighted in gray (in the given example, column H, rows 13 and 14).*

>**Ten_isomers sheets:** the Excel file contains as many sheets as candidate structures are considered, labeled as “Tens_Isomer N”, where N is the isomer number. Each cell contains the isotropic shielding values corresponding to each ensemble (row) and Gaussian label (column). For example, the value shown in cell C2 (91.5338) is the isotropic shielding value of the atom nº 2 (according to Gaussian labeling scheme) computed using ensemble 2 [A-1-0-2]. 
>
![image](https://user-images.githubusercontent.com/101136961/210259165-1156d7c3-68ca-4112-9166-f5e66b48da30.png)

## Workflow and general recommendations

>**Step 1:** Despite the new MESSI can handle any amount of isomers, keeping the number of candidates to a minimum has several advantages, as it reduces both the overall computational cost and the probability that the calculated data for an incorrect isomer ends up having better fit with the experimental values than the correct candidate.

>**Step 2:** The conformational search should provide a good description of the conformational landscape of the system under study. Improper computational work might lead to potentially negative consequences in the overall results. Systematic sampling is always recommended, but impractical in highly flexible molecules. In those cases, stochastic searches using a reasonably large number of steps should be carried out. To avoid missing potentially relevant conformations, all conformations within a safe energy window from the corresponding global minimum should be kept. For this application, we recommend a 10 kcal/mol cutoff value using the MMFFaq force field. 

>**Step 3:** All conformations found in Step 2 must be fully optimized at the PCM/B3LYP/6-31G* level.

>**Step 4:** After removing duplicates, all structures found must be submitted to NMR calculations at the level A (PCM/mPW1PW91/6-31+G**). In parallel, the same PCM/B3LYP/6-31G* optimized structures must be used as inputs for single point energy calculations at level B (SMD/B3LYP/6-31+G**). *__Important:__ MESSI requires that all conformations found to be considered, not just the most stable ones. Therefore, keeping only the most stable conformations found in Step 3 could give erroneous results. In the same way, it is important to respect the suggested theory levels, since MESSI was optimized for those levels.* 

>**Step 5:** The output files must be compiled in a folder. Additionally, an Excel file with the experimental data and labels is needed. The NMR data must be assigned (know which shift corresponds to which nuclei). Using unassigned or misassigned NMR data can lead to erroneous results. The chemical shifts of equivalent nuclei that show fast interconversion should be averaged (such as the case of methyl groups, or some methylene groups). Treating the signal of each individual proton independently is wrong (for example, computing three different chemical shifts for the same methyl group). Another problem arises when dealing with diastereotopic methylene protons, which are ofen arbitrarily correlated. Unless the discrimination of both signals as pro-R and pro-S is made using additional NMR information (such as NOE or J coupling), the most convenient way to tackle this issue is to treat them as interchangeable signals.

>**Step 6:** Run the script `messi.py` to perform the PCM-DP4+, SMD-DP4+ and MESSI probabilities calculations. The script opens a pop-up window that requests to select the folder that contains the Gaussian output files (either as `*.log or *.out`), and the Excel input file. The script feeds on the corresponding NMR and SCRF/SMD single point Gaussian output files. Both types of calculations could be run separately or together through the "link" option. The script automatically extracts the isotropic shielding values and energies from each output and classifies them per isomer.  Finally, the chemical shifts are averaged according the filter type and correlated with the experimental data to use it in the DP4+ formalism. The results are printed in an Excel file named *‘MESSI_Results.xlsx’*.
>
>> <picture>
 <img alt="Show" src="https://user-images.githubusercontent.com/101136961/210239258-463e1585-049a-4b22-ba88-1d7ae5ebf5a7.png" width="704" height="430"/>
</picture>

## Case study: 1,6-anhydrohexopyranosides

In order to illustrate the MESSI workflow, we present the analysis of 1,6-anhydrohexopyranosides family. As indicated in the Figure, there are eight possible isomers.

> <picture>
 <img alt="Show" src="https://user-images.githubusercontent.com/101136961/208667453-a3f8c7ce-b338-4260-9b57-5098232dc80f.png" width="616" height="344"/>
</picture>

>Following the recommended computational procedure, a total number of 130 conformers were found after the optimization at the B3LYP/6-31G* level (the standard for DP4+ calculations). Each structure was submitted to NMR and SCRF calculations at the PCM/mPW1PW91/6-31+G** and SMD/B3LYP/6-31+G** level respectively. The corresponding output files are provided in the Folder “Example”. According to Gaussian numbering scheme, the labels corresponding to each nuclei are given in Figure, Carbon label followed by its corresponding proton(s) label(s) between parenthesis.

><picture>
 <img alt="Show" src="https://user-images.githubusercontent.com/101136961/208426346-58680274-4ada-482d-af23-713d141f1a4e.png" width="215" height="224"/>
</picture>

## MESSI Analysis

MESSI calculations were running for the eight possible distereoisomer, and placed in a folder. Once the script is run, the resulting excel report file *“MESSI_Results”* will be generated.

> ### MESSI input and output excel files

![image](https://user-images.githubusercontent.com/101136961/208428264-15c58051-c2c7-44db-917a-399960f53920.png)

![image](https://user-images.githubusercontent.com/101136961/208428589-cb4b4bd7-358d-4ea7-8826-489a478b1675.png)

