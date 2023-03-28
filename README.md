# Tutorial: Docking of glycosaminoglcyan (GAG) substrate to 3-O-sulfotransferase (3-OST-1)

### Requirements
**Minimal requirement**: a recent version of PyMOL installed on your computer. 

DockingPie is compatible with incentive PyMOL builds distributed by [Schrodinger](https://pymol.org/2/ "Schrodinger website") (required PyMOL version >= 2.3.4) and open source builds (required PyMOL version >= 2.3.0).

DockingPie is distributed freely to the public, and it has been tested and runs on the Windows, macOS, and Linux versions of PyMOL.

Some incompatibilities may arise with the usage of PyMOL version 2.5.x if the "undo" function is enabled, which in PyMOL 2.5.2 still shows some shortcomings. Therefore, when the plugin is opened, the "undo" function is automatically disabled, and it is strongly suggested to keep it disabled when using the plugin.

### Download
PyMOL Software download links: [Windows](https://pymol.org/installers/PyMOL-2.5.4-Windows-x86_64.exe)  |  [Mac OS](https://pymol.org/installers/PyMOL-2.5.4_420-MacOS-py37.dmg)  | [Linux](https://pymol.org/installers/PyMOL-2.5.4_404-Linux-x86_64-py37.tar.bz2)

DockingPie plugin ZIP file: [Download](https://github.com/paiardin/DockingPie/archive/refs/heads/main.zip "DockingPie plugin ZIP file direct download") 

Download AutoDock Vina: [Windows](https://vina.scripps.edu/wp-content/uploads/sites/55/2020/12/autodock_vina_1_1_2_win32.msi)  | [Linux](https://vina.scripps.edu/wp-content/uploads/sites/55/2020/12/autodock_vina_1_1_2_linux_x86.tgz)  | [macOS](https://vina.scripps.edu/wp-content/uploads/sites/55/2020/12/autodock_vina_1_1_2_mac_64bit.tar.gz)

Download GlycoTorch Vina: [Windows](https://ericboittier.pythonanywhere.com/static/GlycoTorchVina.exe) | [Linux](https://ericboittier.pythonanywhere.com/static/GlycoTorchVina)


### Installation 

![immagine](https://github.com/glycodynamics/DockingPieTutor/blob/main/images/DockingPie_install.png)

DockingPie is installed, as any other PyMOL [1] plugin, via the PyMOL plugin manager:

* First download the latest version of the plugin ZIP file [here](https://github.com/paiardin/DockingPie/archive/refs/heads/main.zip  "DockingPie plugin ZIP file direct download") 

* Launch PyMOL and use the *Plugin* → *Plugin Manager* command from the main menu of PyMOL. The plugin manager window of PyMOL will open.

* Click on *Install New Plugin* and press the *Choose File…* button. Select the **DockingPie ZIP file** which you have downloaded before. 
You will be asked to give the path of the directory in which to install the plugin files. Just select the default option if you are unsure about what to do (the location of the plugin files does not make any difference when running the plugin).

### Configuration 

DockingPie, at the current and first release, integrates four different docking programs: RxDock [2], Vina [3], Smina [4] and ADFR [5]; several chemo-informatics python modules (i.e. AutoDockTools [6], Openbabel [7], sPyRMSD [8]) and other external tools like sdsorter [9]. The CONFIGURATION tab provides an easy way for the installation of the needed tools from within the plugin in two steps, as reported next.

![immagine](https://github.com/glycodynamics/DockingPieTutor/blob/main/images/DockingPie_Configure.png)

* Configure external tools: CONFIGURATION tab → *Configure* → *Start Download* → *Finish Download*

* Install external tools: If the needed tools are not currently installed on the user’s machine, the *Install* button is enabled and it can be used to install the external components.


# 1. AutoDock Vina: Hands-On Tutorial

### 1. Preparing System for Docking: 
**Download Structure:** Open PyMOL and download PDB ID 3UAN (File → Get PDB → Write '3UAN' → Click Download)\

**Delete Alternate Location in the structure:** Use follwoing code to delete alternate location of certain residues in PyMOL\
```
remove not alt ''+A
alter all,  alt=''
```
**Split protein and GAG molecule:**\
To dock the GAG into the protein, first save protein and GAG separately into two different entries. First select Chain A by chnaging the selection mode to chain and then clicking on chanin A and then extract 'sele' entry as new object (sele → A → Extract To Object (Obj01)).

- Rename Obj01 as receptor (Obj01 → A → Rename Object → Write name "receptor' and hit enter.

- Similarily select the GAG molecule and extract this entry by name `lig_xray`

### 2. Preparing Receptor and Ligand Input Files

- **Receptor Input File:** PyMOL → Plugin → DockingPie 1.2 → Open Panel Vina → Sub-panel Receptors → Import from PyMOL → Select receptor → Import → Check Add hydrogens, Remove Non-standard residues, Remove Water (if you did not delete them before!) →  Generate Receptor → Select Receptor → Set

- **Ligand Input File:** DockingPie 1.2 → Panel Vina → Sub-panel Ligands → Import from PyMOL → Select lig_xray → Import → Check All but Guanidium and Amide, Add hydrogen →  Generate Ligand → Select Ligand → Set

<img width="977" alt="image" src="https://user-images.githubusercontent.com/10772897/228326317-c51c952d-bd8d-4dc6-8373-c9c11cf27361.png">

### 3. Assigning Search Space for Docking: Grid Settings

- **Set Grid Box Center:** PyMOL → Plugin → DockingPie 1.2 → Panel Vina → Sub-panel Grid Settings → Import Objects from PyMOL → Selection: lig_xray\
Here we choose coordinates GAG in X-Rray structure as center of the docking box. 

- **Set Grid Box Dimensions:**\
Set the grid dimention to: All=1, x=40, y-40, z=40; and then click "Set in Docking Tab".
These numbers suggest that a box of domension 40Å x 40Å x 40Å centered at the geometric centre of the GAG in X-Rray structure has ben defined as search space for docking. Docking program will try finding optmimized binding pose of the ligand inside the definded search space only. The search space effectively restricts where the movable atoms, including those in the flexible side chains, should lie.

**Note** Plese note down the grid center coordinates and dimensions. We wil use tehse numbers later in teh tutorial to perform docking of GAG using GlycoTyrch Vina which is not supported in DockingPie 1.2 yet.

### 4. Run Docking
- DockingPie 1.2 → Panel Vina → Sub-panel Docking 
- Select "AllvsAll" in Docking Tab
- Select Available caveties: Grid center_1 
- Select Receptor(s): 01_receptor_vina
- Select Ligand(s)  : 01_lig_xray_vina
- Poses = 20 #generate 20 docking poses
- Exastiveness = 8  # Exhaustiveness of the global search. This increases the time linearly and decrease the probability of not finding the minimum exponentially.
- Energy Range = 5   #maximum energy difference between the best binding mode and the worst one displayed (kcal/mol)
- Click "Run Docking" → Start
<img width="534" alt="image" src="https://user-images.githubusercontent.com/10772897/228357313-1dfa7725-ccc9-46b4-9c3c-a1a83d524074.png">


### 5. Analyze Docking Results
- When docking run is 100% complete, a new entry "Vina" is created in PyMIL. Click "+" to expand entries under Vina. Entry Run_1_Vina contains all the docking Poses. 
- visualize the docking poses in PyMOL and compare the docking poses from the one determined in X-ray structure. 
<img width="950" alt="image" src="https://user-images.githubusercontent.com/10772897/228370232-28bc5583-befe-4d77-986b-03099f4e24a3.png">


# GlycoTorch Vina: Hands-On Tutorial

### 1. Obtaining Receptor and Ligand Input Files
- Since, GlycoTorch Vina is version of AutoDock Vina, optimized for docking of glycosaminoglycans to proteins, the input files for both programs will be same. In this case, we will copy receptor and ligand input files prepared by DockingPie plugin and use them for docking using program GlycoTorch.

- Copy file ```01_receptor_Vina.pdbqt``` and ```01_lig-xray_Vina.pdbqt``` from the DockingPie working directory or download them from here: [01_receptor_Vina.pdbqt](https://github.com/glycodynamics/DockingPieTutor/blob/main/tutorial/01_receptor_Vina.pdbqt)  and [01_lig-xray_Vina.pdbqt](https://github.com/glycodynamics/DockingPieTutor/blob/main/tutorial/01_lig-xray_Vina.pdbqt). 

- type ```pwd``` in PyMOL terminal to know the location of these files.
- **Typically the path is:** C:\ProgramData\pymol\lib\site-packages\pmg_tk\startup\DockingPie1\lib\docking_program_main\tmp\Vina_tmp\

### 2. Docking Configuration File
One can write all the input information in a text file [GTVina.conf](https://github.com/glycodynamics/DockingPieTutor/blob/main/tutorial/GTVina.conf) and use it as input to GlycoTorch Vina. For example:

```
receptor = 01_receptor_Vina.pdbqt 	# name of receptor input file 
ligand = 01_lig-xray_Vina.pdbqt    # name of the ligand input file

out = Run_1_GTVina.pdbqt     # name of the docking output file 
log = Run_1_GTVina_log.txt

center_x=11.46	                    # x, y and z coordinate of the search box 
center_y=12.49 
center_z=47.96 

size_x=40                          # Size of the search space box in Angstrom in x, y and z direction 
size_y=40 
size_z=40 

num_modes=20 	                   # number of docking solutions
exhaustiveness=8                 # exhaustiveness of the global search (roughly proportional to time) 
energy_range=5 	                 # within energy range 
cpu=8		                          # number of CPU cores used for docking 

chi_coeff=1                      # Chi coefficient energy (used in vina-carb only)
chi_cutoff=2                     # Chi cutoff energy (used in vina-carb only)
```
### 3. Run Docking
- Copy both input pdbqt files, GTVina.conf configuration files in a direcotry and then open Command Prompt
- Change direcotry to working direcotry. Write `>cd` and drag and drop the working directory in the command prompt
- Then run GlycoTorch Vina: ```GlycoTorchVina.exe --config GTVina.conf```
- Wait until the docking is done

### 4. Compare Docking results from Vina and GlycoTorch Vina

Open GlycoTorch Vina output files ```Run_1_GTVina.pdbqt``` in PyMOL and visualize the docking poses from Vina, and GlycoTorch. The highest raning pose (M1) from GlycoTorch is very close to crystal structure binding mode of GAG, whereas only the 5th ranked docking pose from Vina is close to crystal structure binding mode. This 


<img width="950" alt="image" src="https://user-images.githubusercontent.com/10772897/228370979-7f82046c-ed39-4831-9af4-afd2c895ba9a.png">


The results suggest that GlycoTorch performed better than Vina in terms of generating docking poses that are close to the crystal structure binding mode of GAG. Specifically, the highest ranked pose generated by GlycoTorch (labeled as "M1") was very close to the crystal structure binding mode, while only the 5th ranked pose generated by Vina was close to the crystal structure binding mode.

It is evident that GlycoTorch Vina may be a more accurate or effective docking program for predicting the binding mode of glycosaminoglycans (GAGs) than Vina. However, it is important to note that the performance of different docking programs can vary depending on various factors. Therefore, it may be necessary to analyze the top few docking poses and use other methods, like molecular dynamics, to further validate the results and confirm the accuracy of the docking predictions.

### Citations: 

## References

[1] DeLano, WL. (2002). “The PyMOL Molecular Graphics System on World Wide Web.” CCP4 Newsletter On Protein Crystallography

[2] DockingPie: Serena Rosignoli, Alessandro Paiardini, DockingPie: a consensus docking plugin for PyMOL (2022). [Bioinformatics, 38(17) pp. 4233–4234](https://doi.org/10.1093/bioinformatics/btac452).

[3] Ruiz-Carmona, S., Alvarez-Garcia, D., Foloppe, N., Garmendia-Doval, A. B., Juhos, S., Schmidtke, P., Barril, X., Hubbard, R. E., & Morley, S. D. (2014). rDock: a fast, versatile and open source program for docking ligands to proteins and nucleic acids. [PLoS computational biology, 10(4), e1003571. ](https://doi.org/10.1371/journal.pcbi.1003571)

[4] O. Trott, A. J. Olson, AutoDock Vina: improving the speed and accuracy of docking with a new scoring function, efficient optimization and multithreading (2010). [Journal of Computational Chemistry 31:455-461](https://onlinelibrary.wiley.com/doi/10.1002/jcc.21334)


[5] Ravindranath PA, Forli S, Goodsell DS, Olson AJ, Sanner MF. AutoDockFR: Advances in Protein-Ligand Docking with Explicitly Specified Binding Site Flexibility (2015). [PLoS Comput Biol. 11(12):e1004586.](https://doi.org/10.1371/journal.pcbi.1004586)


[6] O'Boyle, N.M., Banck, M., James, C.A. et al. Open Babel: An open chemical toolbox. [J Cheminform 3, 33 (2011).](https://doi.org/10.1186/1758-2946-3-33)

[7] Meli, R., Biggin, P.C. spyrmsd: symmetry-corrected RMSD calculations in Python. [J Cheminform 12, 49 (2020).](https://doi.org/10.1186/s13321-020-00455-2)
 
### Acknowledgments 
This tutorial is adopted from tutorial by author's of DockingPie program. 
