# DockingPie: a Docking Plugin for PyMOL

## Requirements
**Minimal requirement**: a recent version of PyMOL installed on your computer. 

DockingPie is compatible with incentive PyMOL builds distributed by [Schrodinger](https://pymol.org/2/ "Schrodinger website") (required PyMOL version >= 2.3.4) and open source builds (required PyMOL version >= 2.3.0).

DockingPie is distributed freely to the public and it has been tested and runs on Windows, macOS and Linux versions of PyMOL.

(Some incompatibilities may arise with the usage of PyMOL version 2.5.x if ‘undo’ function is enabled, which in PyMOL 2.5.2 still shows some shortcomings. Therefore, when the plugin is opened, the ‘undo’ function is automatically disabled and it is strongly suggested to keep it disabled when using the plugin.)

## Download
PyMOL Software download links: [Windows](https://pymol.org/installers/PyMOL-2.5.4-Windows-x86_64.exe)  |  [Mac OS](https://pymol.org/installers/PyMOL-2.5.4_420-MacOS-py37.dmg)  | [Linux](https://pymol.org/installers/PyMOL-2.5.4_404-Linux-x86_64-py37.tar.bz2)

DockingPie plugin ZIP file: [download from here](https://github.com/paiardin/DockingPie/archive/refs/heads/main.zip "DockingPie plugin ZIP file direct download") 


## Installation 

![immagine](https://github.com/glycodynamics/DockingPieTutor/blob/main/images/DockingPie_install.png)

DockingPie is installed, as any other PyMOL [1] plugin, via the PyMOL plugin manager:

* First download the latest version of the plugin ZIP file [here](https://github.com/paiardin/DockingPie/archive/refs/heads/main.zip  "DockingPie plugin ZIP file direct download") 

* Launch PyMOL and use the *Plugin* → *Plugin Manager* command from the main menu of PyMOL. The plugin manager window of PyMOL will open.

* Click on *Install New Plugin* and press the *Choose File…* button. Select the **DockingPie ZIP file** which you have downloaded before. 
You will be asked to give the path of the directory in which to install the plugin files. Just select the default option if you are unsure about what to do (the location of the plugin files does not make any difference when running the plugin).

## Configuration 

DockingPie, at the current and first release, integrates four different docking programs: RxDock [2], Vina [3], Smina [4] and ADFR [5]; several chemo-informatics python modules (i.e. AutoDockTools [6], Openbabel [7], sPyRMSD [8]) and other external tools like sdsorter [9]. The CONFIGURATION tab provides an easy way for the installation of the needed tools from within the plugin in two steps, as reported next.

![immagine](https://github.com/glycodynamics/DockingPieTutor/blob/main/images/DockingPie_Configure.png)

* Configure external tools: CONFIGURATION tab → *Configure* → *Start Download* → *Finish Download*

* Install external tools: If the needed tools are not currently installed on the user’s machine, the *Install* button is enabled and it can be used to install the external components.




### Installation


### Citations: 
DockingPie: Serena Rosignoli, Alessandro Paiardini, DockingPie: a consensus docking plugin for PyMOL (2022). [Bioinformatics, 38(17) pp. 4233–4234](https://doi.org/10.1093/bioinformatics/btac452).

## References

[1] DeLano, WL. (2002). “The PyMOL Molecular Graphics System on World Wide Web.” CCP4 Newsletter On Protein Crystallography

[2] Ruiz-Carmona, S., Alvarez-Garcia, D., Foloppe, N., Garmendia-Doval, A. B., Juhos, S., Schmidtke, P., Barril, X., Hubbard, R. E., & Morley, S. D. (2014). rDock: a fast, versatile and open source program for docking ligands to proteins and nucleic acids. [PLoS computational biology, 10(4), e1003571. ](https://doi.org/10.1371/journal.pcbi.1003571)

[3] O. Trott, A. J. Olson, AutoDock Vina: improving the speed and accuracy of docking with a new scoring function, efficient optimization and multithreading, Journal of Computational Chemistry 31 (2010) 455-461

[4] Koes, David Ryan et al. Lessons learned in empirical scoring with smina from the CSAR 2011 benchmarking exercise. [Journal of chemical information and modeling vol. 53,8 (2013): 1893-904. ](doi:10.1021/ci300604z)

[5] Ravindranath PA, Forli S, Goodsell DS, Olson AJ, Sanner MF. AutoDockFR: Advances in Protein-Ligand Docking with Explicitly Specified Binding Site Flexibility. [PLoS Comput Biol. 2015;11(12):e1004586.](https://doi.org/10.1371/journal.pcbi.1004586)

[6] Morris, G. M., Huey, R., Lindstrom, W., Sanner, M. F., Belew, R. K., Goodsell, D. S., & Olson, A. J. (2009). AutoDock4 and AutoDockTools4: Automated docking with selective receptor flexibility. Journal of Computational Chemistry, 30(16), 2785–2791.

[7] O'Boyle, N.M., Banck, M., James, C.A. et al. Open Babel: An open chemical toolbox. [J Cheminform 3, 33 (2011).](https://doi.org/10.1186/1758-2946-3-33)

[8] Meli, R., Biggin, P.C. spyrmsd: symmetry-corrected RMSD calculations in Python. [J Cheminform 12, 49 (2020).](https://doi.org/10.1186/s13321-020-00455-2)
 
## Acknowledgments 
This tutorial is adopted from tutorial by author's of DockingPie program. 
