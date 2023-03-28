# Tutorial: Docking of glycosaminoglcyan (GAG) substrate to 3-O-sulfotransferase (3-OST-1)

### Requirements
**Minimal requirement**: a recent version of PyMOL installed on your computer. 

DockingPie is compatible with incentive PyMOL builds distributed by [Schrodinger](https://pymol.org/2/ "Schrodinger website") (required PyMOL version >= 2.3.4) and open source builds (required PyMOL version >= 2.3.0).

DockingPie is distributed freely to the public and it has been tested and runs on Windows, macOS and Linux versions of PyMOL.

(Some incompatibilities may arise with the usage of PyMOL version 2.5.x if ‘undo’ function is enabled, which in PyMOL 2.5.2 still shows some shortcomings. Therefore, when the plugin is opened, the ‘undo’ function is automatically disabled and it is strongly suggested to keep it disabled when using the plugin.)

### Download
PyMOL Software download links: [Windows](https://pymol.org/installers/PyMOL-2.5.4-Windows-x86_64.exe)  |  [Mac OS](https://pymol.org/installers/PyMOL-2.5.4_420-MacOS-py37.dmg)  | [Linux](https://pymol.org/installers/PyMOL-2.5.4_404-Linux-x86_64-py37.tar.bz2)

DockingPie plugin ZIP file: [Download](https://github.com/paiardin/DockingPie/archive/refs/heads/main.zip "DockingPie plugin ZIP file direct download") 

Download AutoDock Vina: [Windows](https://vina.scripps.edu/wp-content/uploads/sites/55/2020/12/autodock_vina_1_1_2_win32.msi)  | [Linux](https://vina.scripps.edu/wp-content/uploads/sites/55/2020/12/autodock_vina_1_1_2_linux_x86.tgz)  | [macOS](https://vina.scripps.edu/wp-content/uploads/sites/55/2020/12/autodock_vina_1_1_2_mac_64bit.tar.gz)

Download AutoDock Vina: [Windows](https://ericboittier.pythonanywhere.com/static/GlycoTorchVina.exe) | [Linux](https://ericboittier.pythonanywhere.com/static/GlycoTorchVina)


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




# Hands-On Tutorial

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

- **Receptor Input File:** PyMOL → Plugin → DockingPie 1.2 → Open Panel Vina → Receptors → Import from PyMOL → Select receptor → Import → Check Add hydrogens, Remove Non-standard residues, Remove Water (if you did not delete them before!) →  Generate Receptor → Select Receptor → Set

- **Ligand Input File:** DockingPie 1.2 → Panel Vina → Ligands → Import from PyMOL → Select lig_xray → Import → Check All but Guanidium and Amide, Add hydrogen →  Generate Ligand → Select Ligand → Set

<img width="977" alt="image" src="https://user-images.githubusercontent.com/10772897/228326317-c51c952d-bd8d-4dc6-8373-c9c11cf27361.png">

2. Assigning Search Space for Docking: Grid Setting

- **Set Grid Box Center:** PyMOL → Plugin → DockingPie 1.2 → Panel Vina → Grid Settings → Import Objects from PyMOL → Selection: lig_xray\
Here we choose coordinates GAG in X-Rray structure as center of the docking box. 

- **Set Grid Box Dimensions:**\
Set the grid dimention to: All=1, x=40, y-40, z=40. These numbers suggest that a box of domension 40Å x 40Å x 40Å centered at the geometric centre of the GAG in X-Rray structure has ben defined as search space for docking. Docking program will try finding optmimized binding pose of the ligand inside the definded search box only. 

**Note** Plese note down the grid center coordinates and dimensions. We wil use tehse numbers later in teh tutorial to perform docking of GAG using GlycoTyrch Vina which is not supported in DockingPie 1.2 yet.


→ Import → Check Add hydrogens, Remove Non-standard residues, Remove Water (if you did not delete them before!) →  Generate Receptor → Select Receptor → Set

Import Object from PyMOL
Select lig_xray (Original Position of ligand (COM) as center of the grid)
Set x,y,z dimension to 40
Set in Docking Tab
Note down Grid Center Coordinates 




### Citations: 

## References

[1] DeLano, WL. (2002). “The PyMOL Molecular Graphics System on World Wide Web.” CCP4 Newsletter On Protein Crystallography

[2] DockingPie: Serena Rosignoli, Alessandro Paiardini, DockingPie: a consensus docking plugin for PyMOL (2022). [Bioinformatics, 38(17) pp. 4233–4234](https://doi.org/10.1093/bioinformatics/btac452).

[3] Ruiz-Carmona, S., Alvarez-Garcia, D., Foloppe, N., Garmendia-Doval, A. B., Juhos, S., Schmidtke, P., Barril, X., Hubbard, R. E., & Morley, S. D. (2014). rDock: a fast, versatile and open source program for docking ligands to proteins and nucleic acids. [PLoS computational biology, 10(4), e1003571. ](https://doi.org/10.1371/journal.pcbi.1003571)

[4] O. Trott, A. J. Olson, AutoDock Vina: improving the speed and accuracy of docking with a new scoring function, efficient optimization and multithreading, Journal of Computational Chemistry 31 (2010) 455-461

[5] Koes, David Ryan et al. Lessons learned in empirical scoring with smina from the CSAR 2011 benchmarking exercise. [Journal of chemical information and modeling vol. 53,8 (2013): 1893-904. ](doi:10.1021/ci300604z)

[6] Ravindranath PA, Forli S, Goodsell DS, Olson AJ, Sanner MF. AutoDockFR: Advances in Protein-Ligand Docking with Explicitly Specified Binding Site Flexibility. [PLoS Comput Biol. 2015;11(12):e1004586.](https://doi.org/10.1371/journal.pcbi.1004586)

[7] Morris, G. M., Huey, R., Lindstrom, W., Sanner, M. F., Belew, R. K., Goodsell, D. S., & Olson, A. J. (2009). AutoDock4 and AutoDockTools4: Automated docking with selective receptor flexibility. Journal of Computational Chemistry, 30(16), 2785–2791.

[8] O'Boyle, N.M., Banck, M., James, C.A. et al. Open Babel: An open chemical toolbox. [J Cheminform 3, 33 (2011).](https://doi.org/10.1186/1758-2946-3-33)

[9] Meli, R., Biggin, P.C. spyrmsd: symmetry-corrected RMSD calculations in Python. [J Cheminform 12, 49 (2020).](https://doi.org/10.1186/s13321-020-00455-2)
 
### Acknowledgments 
This tutorial is adopted from tutorial by author's of DockingPie program. 
