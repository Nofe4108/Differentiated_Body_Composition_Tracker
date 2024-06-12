## Differentiated_Body_Composition_Tracker
### Overview

The Differentiated Body Composition Tracker (DBCT) is a post-processing code written in Python that models the transfer of core and mantle material between colliding objects during the late stages of planet formation. The DBCT uses data collected from a REBOUND simulation in C that implements the [fragmentation module](https://github.com/ANNACRNN/REBOUND_fragmentation) and modifiable, analytical equations to calculate the final CMFs of the remaining objects. For more detailed information on the code and the model it uses, please visit Ferich et al. (in prep).

### Parameters

The DBCT allows users to change 4 parameters: core_density, mantle_density, min_ejecta_core_frac, and max_ejecta_core_frac. The first two parameters represent the densities of the core and mantle material that compose the objects in a simulation. They have default values of 7874.0 kg/m<sup>3</sup> and 3000.0 kg/m<sup>3</sup> respectively. Changing these parameters changes the size of an object's core, which affects the resulting transfer of material during a disruptive collision. The last two parameters represent the minimum and maximum fraction of core material that can be in the ejecta from a collision. These parameters will change how much core and mantle material can be transferred during a disruptive collision. Please visit Ferich et al. (in prep) for more details on how these four parameters can affect the results from the DBCT.

### Input Files

The DBCT requires three different input files: an initial composition file, a collision report from the fragmentation module for REBOUND, and a file containing information about any particles that were ejected during the course of a simulation. 

- The initial composition file should contain the hashes, masses, and initial CMFs of the objects at the start of the simulation; usually it is easiest to produce this file while creating the particles for a REBOUND simulation. 

- The collision report is produced by the fragmentation module during the course of a REBOUND simulation. The module must be slightly modified to output all the parameters required by the DBCT. Instructions for these modifications can be found in extras.txt. 

- The ejection file should contain the time of ejection and hashes of the objects that were ejected. The ejection file should be produced during the course of a REBOUND simulation but is not automatically produced by the REBOUND module. Users need to determine what constitutes an ejection in their simulation and create the code to produce the file containing objects that meet these conditions. extras.txt contains code that demonstrates one way of producing this file. It's also possible to simply remove the ejection feature from the DBCT by removing all instances of the ejection file and any variables or code that use its data. 

Examples of all three of these files can be found in the [DBCT_input](DBCT_input/) folder. These example files were created from a 10 Myr-long REBOUND simulation of a disk containing 26 Mars-sized and 260 moon-sized objects around a Sun-like star. All objects start with a uniform CMF of 0.3 and have nearly circular obits with semi-major axes that range from 0.35 AU to 4.0 AU. 

### Output Files

The DBCT returns a single file containing the hashes, masses, and CMFs of all objects that remain at the end of the simulation. An example of this file can be found in the [DBCT_output](DBCT_output/) folder. 

For questions, comments, or bugs please email fericn1@unlv.nevada.edu
